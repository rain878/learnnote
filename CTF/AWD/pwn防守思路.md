# pwn防守思路

分两种有源码的防守，一种是没有源码的防守，一般比赛给的都是没有源码的

## 思路一

一些awd比赛，一般拿到服务器用户权限都是比较低的，只能给程序打补丁

### 找到危险函数

例如存在system的无关调用，存在'"/bin/sh"的字符串等

![image-20240911084312717](image/image-20240911084312717.png)

nop掉

![image-20240911084458188](image/image-20240911084458188.png)

![image-20240911084519686](image/image-20240911084519686.png)

shift+F12进入字符串列表，把主要的/bin/sh也给nop掉

![image-20240911084919349](image/image-20240911084919349.png)

保存修改好的程序导出，替换到服务器上的pwn题，并查看是否能够正常使用

![image-20240911084702209](image/image-20240911084702209.png)

## 思路二

把存在栈溢出的read函数等，定义的buf只有128字节，但是读取了200个字节，我们需要限制掉

![image-20240911090737779](image/image-20240911090737779.png)

找到相关位置，把200改成128（80h）以内都行，注意进制转换

![image-20240911091012308](image/image-20240911091012308.png)

![image-20240911091428876](image/image-20240911091428876.png)

然后保存，导出

## 思路三

使用一些第三方综合性工具[AoiAWD](https://github.com/DasSecurity-HatLab/AoiAWD)，AoiAWD 是一个专为AWD模式设计的开源项目，它是一个轻量级的EDR系统

安装[参考](https://www.cnblogs.com/mays0u1/p/14393260.html)，AoiAWD安装本机，搭建之后，把编译好的文件上传到比赛服务器运行

```bash
#安装php
sudo apt install php7.2-dev php-pear
sudo vim /etc/php/7.2/cli/php.ini
添加extension=mongodb.so，
设置这两个为Off（phar.readonly = Off 和phar.require_hash = Off）别忘了去掉前面的分号，保存退出

#安装node.js
curl -fsSL https://deb.nodesource.com/setup_22.x -o nodesource_setup.sh
chmod 777 nodesource_setup.sh
sudo ./nodesource_setup.sh
sudo apt-get install nodejs

#安装AoiAWD
git clone https://github.com/DasSecurity-HatLab/AoiAWD.git
sudo apt install mongodb-server  #安装mongodb

#在./AioAWD目录下
cd Frontend
npm install
npm run build
#构建AoiAWDcore
cd AoiAWD
rm -rf src/public/*
cp -r ../Frontend/dist/* src/public/
php compile.php

#安装inotifywait
mkdir inotifywait   
cd inotifywait      
wget http://github.com/downloads/rvoicilas/inotify-tools/inotify-tools-3.14.tar.gz   
tar zxf inotify-tools-3.14.tar.gz   
cd inotify-tools-3.14/
./configure && make && make install 

#构建TapeWorm
cd TapeWorm
php compile.php
构建成功后得到tapeworm.phar

#构建RoundWorm
cd RoundWorm
make
构建成功会得到roundworm

#构建Guardian
cd Guardian
php compile.php
构建成功后得到guardian.phar

#启动AoiAWD
cd AoiAWD        #当前目录AoiAWD/AoiAWD
./aoiawd.phar

#搭建完后把刚刚那些文件夹中的生成的文件例如xxx.phar等发送到提供给我们的靶机上去，然后记得赋予权限，ip是云服务器ip，端口就是默认8023
chmod +x tapeworm.phar
chmod +x roundworm
chmod +x guardian.phar
./tapeworm.phar -d 目录 -s ip:port
./roundworm  -w 目录 -s ip -p port
./guardian.phar -i 目录 -s ip:port
#参数说明：
    ip：我们部署AoiAWD的主机的ip
    port：默认指定8023
    目录：根据功能选择目录
  功能：
    Guardian: PWN行为探针，我指定的是WEB目录，无法指定根目录（无权限）
    TapeWorm: Web行为探针，指定WEB的目录
    RoundWorm: 系统进程与文件系统行为探针，这个不知道为什么可以指定根目录，会阻塞执行
```

