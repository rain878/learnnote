# 工具

## 必备

### linux环境

可以使用[ubuntu](https://ubuntu.com/download)或者[kali-linux](https://www.kali.org/get-kali/#kali-installer-images)

后门的工具都是基于linux安装，除了IDA分析工具(windows环境)

### python

下载python，尽量使用python3，下载写exp需要的pwntools库

```bash
#python安装
sudo apt install python3

#pwntools安装
python -m pip install pwntools
```

### IDA

吾爱破解下载[IDA Pro 8.3 绿色版](https://down.52pojie.cn/Tools/Disassemblers/IDA_Pro_v8.3_Portable.zip)，一款强大的反汇编工具

```bash
快捷键
  F5 #是自动进行反汇编，还原c源码
  /	#写注释
  ctrl + s	#跳准到指定数据段
  ctrl + l	#函数选择器
  x	#查看某个函数的引用
  g	#跳转到指定地址
  d	#让某一个位置变成数据
  c	#让某一个位置变成指令
  shift+F12	#查找字符串
  ctrl + shif	+ f	#过滤器，查找函数
```

右键打开程序分析，注意程序是32位还是64位

![image-20240911101129242](image/image-20240911101129242.png)

默认，选择ok即可，开始界面如下

![image-20240911101200508](image/image-20240911101200508.png)

###checksec,git,gdb,gcc 

checksec：一个检查二进制程序保护的工具

gdb：是一个功能强大的命令行调试工具，分析时需要额外插件pwndbg

```bash
sudo apt install checksec git gdb gcc 

#pwndbg安装
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
sudo ./setup.sh

#checksec使用
checksec [需要分析的软件]
```

## 选择性安装插件

### LibcSearcher 

利用LibcSearcher库，根据泄露的函数地址，匹配对应的libc版本，拿到基址就想相当于拿到其他函数地址构造payload

```python
#LibcSearcher安装
git clone https://github.com/lieanu/LibcSearcher.git
cd LibcSearcher
python setup.py install

#使用方法
from LibcSearcher import *
io = process('xxxxx')
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
......一系列操作，将got地址泄露出来......
xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
puts_got_addr = io.recv()# 接收函数的got地址,比如我这里拿到puts的地址
libc = LibcSearcher('puts',puts_got_addr)
libc_base = puts_got_addr - libc.dump('puts')
system = libc_base + libc.dump('system')
binsh = libc_base + libc.dump('str_bin_sh')
........
继续构造payload，最终调用system
```

###glibc-all-in-one

遇到ret2libc时需要用到的libc库，匹配程序接近的libc

```bash
#安装
git clone https://github.com/matrix1001/glibc-all-in-one
cd glibc-all-in-one
sudo update_list 

#用法
cat list #查看可下载的libc，需要到的libc
./download 2.23-0ubuntu3_amd64 #默认下载到glibc-all-in-one/libs里面
```

### patchelf

当程序运行在本机的libc和对应靶机上的libc不同时，我们要更换和靶机的libc版本

```bash
#安装
sudo apt install patchef

#使用
patchelf --set-interpreter ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/ld-2.23.so ./pwn	#修改ld动态链接器，修改程序的libc
patchelf --replace-needed libc.so.6 ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/libc-2.23.so ./pwn	#修改标准libc库
```

