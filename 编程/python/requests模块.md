# 介绍

文档[requests](https://requests.readthedocs.io/projects/cn/zh-cn/latest/)，因为requests模块属于第三方模块，不是在标准库当中，需要额外安装

```python
pip install requests
```

# 快速入门

## 发送请求

```python
import requests
url = 'https://www.baidu.com'
requests.get(url)  #发送get请求
requests.post(url,data={'key':'value'})  #发送post请求
requests.put(url, data = {'key':'value'})  #发送put请求
requests.delete(url)  #发送delete请求
requests.head(url)  #发送head请求
requests.options(url)  #发送options请求
```

### 发送自定义的请求

```python
import requests
url = 'https://www.baidu.com'
header={
  'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0'
}
res=requests.get(url,headers=header)
```

### 发送带参数的请求

```python
import requests
url = 'https://search.bilibili.com/all?'
header={
  'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0',
  'Cookie':"buvid3=8DC54EE7-9F47-4C8A-0275-438E0529042006018infoc; b_nut=1718355406; _uuid=AD1032C9A-225A-C2D1-DD1E-D241022C41661007072infoc; enable_web_push=DISABLE; header_theme_version=CLOSE; buvid_fp=8181944eb777aa081b7879089cdf5b90; buvid4=5D43A75C-9958-52B7-6242-ACB3D30718FF21530-024061111-ql%2FfORr6MV3gJM22xOEcug%3D%3D; home_feed_column=5; browser_resolution=1453-751; SESSDATA=1f96a7a7%2C1734782297%2C1b551%2A61CjDDlC_viUI-X1JP5RGfVuc-ggT_xsbezegyfRGGXFPkZw6rXjGXE3fz6uCNUFps3G4SVmk2MEZORFhoaFM4R2xvWTdkMEVZeEdxMEJ…eUserID__ckMd5=0b89bd3de8e4dc31; CURRENT_FNVAL=4048; rpdid=|(u)YYu)uJ)R0J'u~u)JllR)l; CURRENT_QUALITY=116; fingerprint=8181944eb777aa081b7879089cdf5b90; buvid_fp_plain=undefined; bp_t_offset_357530304=946780623635218432; hit-dyn-v2=1; LIVE_BUVID=AUTO4717188880736965; bili_ticket=eyJhbGciOiJIUzI1NiIsImtpZCI6InMwMyIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MTk0ODk1MDcsImlhdCI6MTcxOTIzMDI0NywicGx0IjotMX0.jmCw3ihal9_j4GTv905Uh4lpm4Oep7YODGG65GoQH50; bili_ticket_expires=1719489447; b_lsid=327CC194_1904D13CEE7; sid=7v779uo6"
}
kw={
  'keyword':'requests'
}
res=requests.get(url,headers=header,params=kw)
```

### 发送带cookie的请求

```python
import requests
url = 'https://search.bilibili.com/all?'
header={
  'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:127.0) Gecko/20100101 Firefox/127.0',
  'Cookie':"buvid3=8DC54EE7-9F47-4C8A-0275-438E0529042006018infoc; b_nut=1718355406; _uuid=AD1032C9A-225A-C2D1-DD1E-D241022C41661007072infoc; enable_web_push=DISABLE; header_theme_version=CLOSE; buvid_fp=8181944eb777aa081b7879089cdf5b90; buvid4=5D43A75C-9958-52B7-6242-ACB3D30718FF21530-024061111-ql%2FfORr6MV3gJM22xOEcug%3D%3D; home_feed_column=5; browser_resolution=1453-751; SESSDATA=1f96a7a7%2C1734782297%2C1b551%2A61CjDDlC_viUI-X1JP5RGfVuc-ggT_xsbezegyfRGGXFPkZw6rXjGXE3fz6uCNUFps3G4SVmk2MEZORFhoaFM4R2xvWTdkMEVZeEdxMEJ…eUserID__ckMd5=0b89bd3de8e4dc31; CURRENT_FNVAL=4048; rpdid=|(u)YYu)uJ)R0J'u~u)JllR)l; CURRENT_QUALITY=116; fingerprint=8181944eb777aa081b7879089cdf5b90; buvid_fp_plain=undefined; bp_t_offset_357530304=946780623635218432; hit-dyn-v2=1; LIVE_BUVID=AUTO4717188880736965; bili_ticket=eyJhbGciOiJIUzI1NiIsImtpZCI6InMwMyIsInR5cCI6IkpXVCJ9.eyJleHAiOjE3MTk0ODk1MDcsImlhdCI6MTcxOTIzMDI0NywicGx0IjotMX0.jmCw3ihal9_j4GTv905Uh4lpm4Oep7YODGG65GoQH50; bili_ticket_expires=1719489447; b_lsid=327CC194_1904D13CEE7; sid=7v779uo6"
}
res=requests.get(url,headers=header)
```



## 获取响应

```python
import requests
url = 'https://www.baidu.com'
res=requests.get(url)
#Requests 会基于 HTTP 头部对响应的编码作出有根据的推测，有时候会乱码，就需要手动设定编码格式
res.encoding='utf8'
print(res.encoding)  #查看编码
print(res.text)  #打印源码的str类似数据
print(res.content)  #打印源码的bytes类型数据，后续可以使用decode指定编码进行解码
print(res.content.decode())
```

### 常见的响应参数

```python
import requests
url = 'https://www.baidu.com'

# 发送请求
x = requests.get(url)

print(x.url)  #响应url
print(x.status_code)  #状态码
print(x.request.headers)  #响应对象的请求头
print(x.headers)  #响应头
print(x.reason) #响应状态的描述
print(x.apparent_encoding) #响应的编码
```