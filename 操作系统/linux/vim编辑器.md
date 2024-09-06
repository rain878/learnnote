# 介绍

Vim（Vi IMproved）是一款功能强大的文本编辑器，是Unix和类Unix操作系统下的一款经典编辑器，也在其他操作系统上得到广泛使用。Vim是从Unix上的另一款编辑器Vi发展而来，因此它保留了Vi的很多特性，并在此基础上添加了许多新功能。

# 配置

## 全局配置

```shell
sudo vim /etc/vim/vimrc
set expandtab       #将Tab键转换为空格
set tabstop=2       #设置Tab键的宽度为4个空格
set shiftwidth=2    #设置自动缩进的空格数为4
set number          #设置行号
set mouse           #启用鼠标
set autoindent		  #自动换行
```



## 用户配置

# 三个模式

## 正常模式

```shell
i	#当前位置插入
a	#光标后插入
I	#行首插入
A #行尾插入
o	#换行插入
O	#上方一行插入
x	#删除光标所在位置的字符
dd	#删除当前行
yy	#复制当前行
p	#粘贴
u	#撤销操作
Ctrl + r	#重新上一次操作，返回撤销
```

## 可视模式

摁 " v " 即可进入可视模式，对选中的范围的文本进行操作

## 命令行模式

```shell
#摁 ":" 即可进入命令行
:wq	#保存退出
:q!	#强制退出
:set nu	#显示行号
```

## 插入模式

进入插入模式，就相当于文本操作