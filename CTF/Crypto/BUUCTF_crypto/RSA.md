# 环境

来自[RSA](https://buuoj.cn/challenges#RSA)，RSA加密算法是一种非对称加密技术

```
在一次RSA密钥对生成中，假设p=473398607161，q=4511491，e=17
求解出d作为flga提交

flag{125631357777427553}
```

# wp

## python

```python
import libnum
#两个质数
p = 473398607161
q = 4511491
E = 17  #所选公钥
T = (p-1)*(q-1) #这个是求出私钥的条件
D = libnum.invmod(E,T)  #求出私钥
print(D)
```

