# 环境

来自[Alice与Bob](https://buuoj.cn/challenges#Alice%E4%B8%8EBob)

```
密码学历史中，有两位知名的杰出人物，Alice和Bob。他们的爱情经过置换和轮加密也难以混淆，即使是没有身份认证也可以知根知底。就像在数学王国中的素数一样，孤傲又热情。下面是一个大整数:98554799767,请分解为两个素数，分解后，小的放前面，大的放后面，合成一个新的数字，进行md5的32位小写哈希，提交答案。 注意：得到的 flag 请包上 flag{} 提交

flag{d450209323a847c8d01c6be47c81811a}
```

# wp

## python

```python
import sympy
import hashlib
# 先分解的出两个素数
number = 98554799767
factors = sympy.factorint(number)
print(factors)
# 使用md5加密
number='101999966233'
md5_hash=hashlib.md5()
md5_hash.update(number.encode('utf=8'))
flag=md5_hash.hexdigest()
print(flag)
```