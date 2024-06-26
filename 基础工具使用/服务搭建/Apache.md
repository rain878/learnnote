# 介绍

- **LAMP**: Linux (操作系统), Apache (Web服务器), MySQL (数据库服务器), PHP/Python/Perl (脚本语言)。
- **LNMP**: Linux (操作系统), Nginx (Web服务器), MySQL (数据库服务器), PHP/Python/Perl (脚本语言)。

`bin`:包含服务器的二进制可执行文件
`build`:这个目录可能用于存放构建脚本或编译生成的文件，特别是在从源代码编译HTTP服务器时。
`cgi-bin`:用于存放CGI脚本。当HTTP请求指向这个目录中的文件时，服务器将执行这些脚本，并将输出发送给客户端。
`conf`或 `conf.d`:包含服务器的配置文件，如Apache的httpd.conf，以及其他配置片段或模块特定的配置文件。
`error`:包含定义错误页面的文件，这些页面在请求发生错误时返回给客户端，例如404未找到或500服务器内部错误。
`htdocs`:Web内容的默认目录，在Apache中，默认的Web根目录通常是htdocs或www。
`icons`:包含用于Web页面的小图标，如用于目录列表的图标或错误页面的图标。
`include`:包含可以被主配置文件或其他配置文件包含的文件，以便重用配置片段。
`logs`:包含服务器生成的日志文件，如访问日志和错误日志。这些日志记录了服务器的活动和任何问题。
`man` 或 `manual`:包含服务器软件的手册页（manual pages），可以通过man命令查看。
`modules`:包含服务器的模块文件，这些模块提供了额外的功能或对特定类型的请求的处理。



# 编译安装

## ubuntu

```bash
sudo apt install build-essential libssl libssl-dev libxml2 libxml2-dev libcre3 libpcre3-dev libz-dev
sudo apt install libapr1 libapr1-dev libaprutil1 libpcre3 libpcre3-dev   #依赖
./configure --prefix=/usr/local/httpd --enable-ssl 

--enable-ssl   #启用apache的ssl模块，假如已经安装了openssl，直接使用
--with-ssl=/usr/lib/x86_64-linux-gnu   #没有安装openssl就需要指定路径

make
make install


vim /etc/systemd/system/httpd.service
###############################
[Unit]
Description=Apache HTTP Server
After=network.target

[Service]
Type=forking
ExecStart=/usr/local/apache2/bin/apache2 -DFOREGROUND
ExecReload=/usr/local/apache2/bin/apache2 -k restart
ExecStop=/bin/kill -WINCH ${MAINPID}
PrivateTmp=true

[Install]
WantedBy=multi-user.target
################################
```

# 包管理器安装

## linux



```

```



## windows





# 配置

