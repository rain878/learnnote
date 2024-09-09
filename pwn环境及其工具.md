# 工具

## python

下载python，尽量使用python3，下载写exp需要的pwntools库，和LibcSearcher库

```bash
sudo apt install python3
#pwntools安装
python -m pip install pwntools

#LibcSearcher安装
git clone https://github.com/lieanu/LibcSearcher.git
cd LibcSearcher
python setup.py install
```

## ida

一款强大的反汇编工具

##checksec,git,gdb,gcc 

```bash
sudo apt install checksec git gdb gcc 
```

## pwndbg

gdb的一个插件，可以更好的调试程序

```bash
#pwndbg
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
sudo ./setup.sh
```

## LibcSearcher 

利用LibcSearcher库，根据泄露的函数地址，匹配对应的libc版本，拿到基址就想相当于拿到其他函数地址构造payload

```python
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

##glibc-all-in-one

遇到ret2libc时需要用到的libc库，匹配程序接近的libc

```bash
git clone https://github.com/matrix1001/glibc-all-in-one
cd glibc-all-in-one
sudo update_list #安装
cat list #查看可下载的libc
./download 2.23-0ubuntu3_amd64 #默认下载到glibc-all-in-one/libs里面
```

## patchelf

当程序运行在本机的libc和对应靶机上的libc不同时，我们要更换和靶机的libc版本

```bash
sudo apt install patchef
#修改程序的libc
patchelf --set-interpreter ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/ld-2.23.so ./pwn	#修改ld动态链接器
patchelf --replace-needed libc.so.6 ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/libc-2.23.so ./pwn	#修改标准libc库
```

