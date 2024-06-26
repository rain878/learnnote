# 安装

## windows

下载[windows版php](https://windows.php.net/download/)解压直接使用

## linux

### 第一种

使用包管理器直接下载

```bash
sudo apt install php php-fpm
sudo yum install php php-fpm
```



### 第二种

下载[php](https://www.php.net/downloads)源码

```bash
wget https://www.php.net/distributions/php-8.3.8.tar.gz
tar -xzvf php-8.3.8.tar.gz
#安装依赖
sudo apt install pkg-config libxml2 libxml2-dev sqlite3 libsqlite3-dev
./configure --prefix=/usr/local/php --enable-fpm --with-fpm-user=www-data --with-fpm-group=www-data
make
make test  #测试
make install 
```



