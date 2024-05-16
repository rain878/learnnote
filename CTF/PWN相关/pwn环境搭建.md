# 工具

```sh
#checksec,git,gdb,gcc 
sudo apt install checksec git gdb gcc patchelf

#pwndbg
git clone https://github.com/pwndbg/pwndbg
cd pwndbg
sudo ./setup.sh

#glibc-all-in-one
git clone https://github.com/matrix1001/glibc-all-in-one
cd glibc-all-in-one
sudo update_list #安装
cat list #查看可下载的libc
./download 2.23-0ubuntu3_amd64 #默认下载到glibc-all-in-one/libs里面


#修改程序的libc
patchelf --set-interpreter ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/ld-2.23.so ./pwn	#修改ld动态链接器
patchelf --replace-needed libc.so.6 ~/tools/glibc-all-in-one/libs/2.27-3ubuntu1_amd64/libc-2.23.so ./pwn	#修改标准libc库
```

