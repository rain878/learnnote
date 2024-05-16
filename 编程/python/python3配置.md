# 安装

# 配置

```shell
#pip更改源，法一
pip config set global.index-url https://mirror.baidu.com/pypi/simple
#法二
/home/rain/.config/pip/pip.conf #当存在多个pip的时候，可能是这个路径
mkdir ~/.pip/
vim ~/.pip/pip.conf #linux用conf结尾，windows用.ini
加入
[global]
index-url = https://mirror.baidu.com/pypi/simple

#国内源
https://pypi.tuna.tsinghua.edu.cn/simple	#清华源
https://pypi.mirrors.ustc.edu.cn/simple	#中科大镜像
https://mirrors.aliyun.com/pypi/simple/	#阿里镜像
https://pypi.hustunique.com/	#华中科大镜像
https://mirror.baidu.com/pypi/simple	#百度镜像
```

