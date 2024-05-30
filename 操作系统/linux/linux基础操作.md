# 包管理命令

## apt

Debian系Linux发行版的软件包管理工具

## yum

Red Hat系Linux发行版的软件包管理工具

## pacman

Arch Linux系统中用于管理软件包的命令行工具

## rpm

Red Hat系Linux发行版的低级软件包管理工具

## dpkg

Debian系Linux发行版的低级软件包管理工具

# 文件和文本管理

## 创建、删除和操作文件和目录的命令

### ls

```bash
ls  #查看目录
ls -l  #查看所有文件详细信息
ls -a  #查看隐藏文件
ls -h  #显示文件大小
ls -R  #递归列出
ls -t  #按修改时间排序
ls -S  #按文件大小排序
ls -i  #查看文件的索引节点
```

### touch

```bash
touch 1.txt  #创建文件，文件存在，则更新访问时间和修改时间
touch -a 1.txt  #仅修改访问时间
touch -m 1.txt  #仅修改修改时间
touch *.log  #批量修改文件时间戳
```

### rm

```bash
rm 1.txt  #删除文件
rm -f 1.txt  #强制删除文件
rm -i 1.txt  #交互式删除
rm -r /tools/  #递归删除所有目录和文件
rm -d /tools  #删除指定空目录
rm -v 1.txt  #详细模式
rm file\ with\ spaces.txt  #文件名包含特殊字符或空格，可以使用引号或反斜杠进行转义
```

### mkdir

```bash
mkdir tools  #创建文件夹
mkdir -p tools/hello  #递归创建
mkdir -v tools #详细信息
mkdir -m 755 tools  #创建并设置权限

```

### rmdir

```bash
rmdir tools #只能删除空目录
rmdir -p tools/hello  #递归创建
rmdir -v tools #详细信息
```

### cp

```bash
cp 1.txt 2.txt  #复制文件
cp -r tools new_tools  #复制目录以及目录下所有文件
cp -i 1.txt 2.txt  #交互式复制
cp -v 1.txt 2.txt  #详细信息
cp -p 1.txt 2.txt  #保留文件属性
cp -a tools new_tools  #归档模式，递归复制目录，并尽可能保留文件的属性
cp -u 1.txt 2.txt  #仅当源文件比目标文件更新时，或目标文件不存在时，才执行复制操作。
cp -l 1.txt 2  #创建硬链接
cp -s 1.txt 2  #创建符号链接
```

### mv

```bash
mv 1.txt 2.txt  #移动文件或者重命名
mv -i 1.txt 3.txt  #交互式移动
mv -v 1.txt 3.txt  #详细信息
mv -f 1.txt 3.txt  #强制移动

```



## 查看文件内容命令

### cat

```bash
cat 1.txt  #文件的内容显示在终端上
cat >或者>> 1.txt  #从终端输入内容，ctrl+d 结束输入
cat -n 1.txt  #显示行号
cat -b 1.txt  #只显示有内容的行号
cat -E 1.txt  #行尾显示$
cat -T 1.txt  #显示制表符
```



### more

`more`命令适用于查看普通文本文件，但对于非常大的文件，可能会影响系统性能。对于大型日志文件等，建议使用`less`命令进行查看，因为`less`具有更好的性能和更多的功能

```bash
more 1.txt  #逐页显示内容，提供交互式滚动和搜索
more +10 1.txt  #从第10行开始查看
more -2 1.txt  #以每页两行显示
enter  #查看下一行
空格键  #查看下一页
/  #搜索
q  #退出
```



### less

```bash
less -N 1.txt  #显示行号
less -F 1.txt  #内容能在一屏显示完毕，则立即退出
less -i 1.txt  #在搜索文本时，忽略大小写
less -S 1.txt  #在显示文件内容时，折叠长行以适应终端宽度
空格键  #向下滚动一页
b键  #向上滚动一页
/  #搜索文本，输入搜索关键字后按Enter键开始搜索，n键查找下一个匹配项
q键  #退出查看
```



### head

### tail

### strings

`strings`命令用于从二进制文件中提取和显示可打印的字符串。

```bash
strings -n 6 filename  #指定最短的字符串长度。默认值是4个字符
strings -t x filename  #指定显示偏移量的格式。format可以是o（八进制）、x（十六进制）或d（十进制）
strings -e l filename  #指定字符编码。可以是b（字节）、l（小端）、B（大端）
strings -o filename  #显示每个字符串在文件中的位置（以十进制表示）
strings -f filename1 filename2  #在输出每个字符串之前打印文件名（当处理多个文件时很有用）
```



## 编辑文件命令

### nano

### vim

### sed

### awk

### cut

### sort

```bash
sort -b filename  #忽略每行前面的空白字符进行排序
sort -f filename  #忽略大小写进行排序
sort -n filename  #按数值顺序进行排序，而不是按字典顺序
sort -r filename  #按相反顺序排列结果
sort -k 2 filename  #指定按照哪一个字段进行排序，字段从1开始
sort -t ',' -k 2 filename  #指定字段分隔符，默认是空白字符
sort -u filename  #在排序后去除重复行
sort filename -o outputfile  #将排序结果输出到指定文件uniq -c filename

```



### uniq

```bash
uniq -c filename  #在每行前显示该行出现的次数
uniq -d filename  #只输出重复出现的行
uniq -u filename  #只输出不重复的行
uniq -i filename  #在比较时忽略大小写
uniq -s N filename  #在比较时忽略每行前N个字符
uniq -f N filename  #在比较时忽略每行前N个字段
uniq -w N filename  #只比较每行的前N个字符


#去除重复行
sort data.txt | uniq
#计数重复行
sort data.txt | uniq -c
#仅显示重复行
sort data.txt | uniq -d
#仅显示不重复行
sort data.txt | uniq -u

```



### tr

`tr`命令是一个用于转换或删除文本中的字符的命令行工具。`tr`命令读取标准输入，并将其输出到标准输出，执行字符替换、压缩、删除等操作

```bash
tr -d SET1
tr -s SET1
tr -c SET1 SET2
#将小写字母转换为大写字母
echo "hello world" | tr 'a-z' 'A-Z'
#删除字符串中的所有小写字母
echo "hello world 123" | tr -d 'a-z'
#将连续重复的空格压缩为一个空格
echo "hello    world" | tr -s ' '
#将非字母字符转换为换行符
echo "hello 123, world!" | tr -c 'a-zA-Z' '\n'

```



### wc

### xxd

`xxd`命令是一个在Linux和Unix系统上用来创建二进制文件的十六进制表示的工具。它也可以将十六进制表示还原为二进制文件

```bash
xxd [options] [input-file [output-file]]
xxd example.txt  #将其转换为十六进制表示
xxd -r example.txt  #将十六进制表示还原为二进制文件
xxd -p example.txt  #生成纯十六进制格式
xxd -r -p example.phex example_reconstructed.txt  #将纯十六进制格式还原为二进制文件
xxd -c 8 example.txt  #每行显示8个字节
xxd -g 4 example.txt  #每组显示4个字节
xxd -s 128 example.txt  #从偏移量128字节开始显示
xxd -l 32 example.txt  #仅显示前32个字节
```



### base64

```bash
base64 example.txt  #对其内容进行编码
base64 -d encoded.txt  #对其内容进行解码
base64 -w 0 example.txt  #对文件进行编码并禁用换行
base64 --input example.txt --output encoded.txt  #对文件进行编码并将结果保存到另一个文件
base64 --decode --input encoded.txt --output decoded.txt  #对文件进行解码并将结果保存到另一个文件
```



## 查找文件和目录命令

### find

```bash
find /tools  #查找指定目录，列出所有
find /tools -name ".txt"  #指定文件名
find /tools -type f  #指定文件类型
    f：普通文件（Regular file）
    d：目录（Directory）
    l：符号链接（Symbolic link）
    c：字符设备文件（Character special file）
    b：块设备文件（Block special file）
    p：命名管道（Named pipe）
    s：套接字（Socket）
    
find /tools -size  #指定大小
    n[cwbkMG]：表示精确匹配指定大小的文件。
    +n[cwbkMG]：表示匹配大于指定大小的文件。
    -n[cwbkMG]：表示匹配小于指定大小的文件。
    c：字节（bytes）
    w：2 字节的字（words）
    b：512 字节的块（blocks）
    k：千字节（kilobytes）
    M：兆字节（megabytes）
    G：吉字节（gigabytes）

find /tools -mmite 1  #指定天修改时间(文件内容最后一次修改)
find /tools -amite 1  #指定天访问时间
find /tools -cmite 1  #指定天更改时间(文件元数据如权限，所有者等，最后一次更改)

find /tools -mmin 10  #指定分钟

find /tools -perm 755  #指定权限
find /tools -uers rain  #指定所属者
find /tools -group rain  #指定所属组
find /tools -exec command {} \;  #对匹配的每个文件执行指定的命令，{}会被当前文件替换。
find /tools -maxdepth 2 #限制搜索的目录深度。
```



### grep

### locate

### which

### whereis

## 文件权限和属性管理命令

### chmod

### chown

### chgrp

## 解压缩文件命令

linux下的压缩后缀文件`.tar`、`.gz`、`.bz2`、`.xz`、`.zip`、`.7z`、`.tar.gz或者.tgz`、`.tar.bz2或者.tbz2`、`.tar.xz或者.txz`、`.rar`

### tar

`tar` 命令是一个用于在 Linux 和 Unix 系统上创建和管理文件归档的工具。`tar` 原本是 "tape archive" 的缩写，但它不仅用于磁带备份，也用于任何形式的归档和压缩文件管理

```bash
    -c：创建一个新的归档。
    -v：详细模式，显示处理的文件。
    -f：指定归档文件的名称。
    -t：列出归档内容而不提取。
    -x：从归档中提取文件。
    -z：使用 gzip 压缩归档。
    -j：使用 bzip2 压缩归档。
    -J：使用 xz 压缩归档。
    -C：将文件提取到指定目录
    --exclude：在创建归档时排除特定文件或目录
    --remove-files：在归档后删除源文件
    
tar -tcf archive.tar  #列出归档内容
tar -cvf archive.tar directory/  #压缩成.tar
tar -czvf archive.tar.gz directory/  #压缩成.tar.gz
tar -cjvf archive.tar.bz2 directory/  #压缩成.tar.bz2
tar -cJvf archive.tar.xz directory/  #压缩成.tar.xz

tar -xvf archive.tar  #解压.tar
tar -xzvf archive.tar.gz  #解压.tar.gz
tar -xjvf archive.tar.bz2  #解压.tar.bz2
tar -xJvf archive.tar.xz  #解压.tar.xz

tar -xvf archive.tar -C /path/to/directory  #指定目录
```

### gzip

`gzip` 是一种广泛使用的文件压缩工具，它使用 DEFLATE 算法来压缩单个文件。它的目标是减少文件的大小，以节省存储空间或加快网络传输速度

```bash
gzip file.txt  #压缩，同时删除源文件
gzip -k file.txt #压缩或解压，同时保留原始文件
gunzip file.txt.gz 或者 gzip -d file.gz  #解压
gzip -1 file.txt    # 最快的压缩速度，压缩率最低
gzip -9 file.txt    # 最慢的压缩速度，压缩率最高
gzip -l file.txt.gz  #使用 -l 选项查看 .gz 文件的压缩信息
gzip -v file.txt  #压缩文件并显示详细信息
zcat file.txt.gz  #使用 zcat 命令查看 .gz 文件内容，而不解压文件
gzip -f file.txt  #强制压缩
```

### bzip2

`bzip2` 是一种用于压缩和解压文件的工具，它使用 Burrows-Wheeler 压缩算法，通常比 `gzip` 提供更高的压缩率，但速度较慢

```bash
bzip2 file.txt  #压缩，同时删除源文件
bzip2 -k file.txt  #压缩或解压，同时保留源文件
bunzip2 file.txt.bz2 或者 bzip2 -d file.txt.bz2  #解压
bzip2 -1 file.txt    # 最快的压缩速度，压缩率最低
bzip2 -9 file.txt    # 最慢的压缩速度，压缩率最高
bzip2 -v file.txt  #查看压缩文件信息
bzcat file.txt.bz2  #使用 bzcat 命令查看 .bz2 文件内容，而不解压文件
bzip2 -f file.txt  #强制压缩
bzip2 -t file.txt.bz2  #测试压缩文件的完整性
bzip2 -q file.txt  #静默模式，不输出警告信息
bzip2 -s file.txt  #减少内存使用，适合小内存系统
```

### zip

```bash
zip -r archive.zip directory/  #压缩
unzip archive.zip  #解压
```

### 7z

```bash
7z a archive.7z directory/  #压缩
7z x archive.7z  #解压
```

### xz

```bash
xz file.txt  #压缩
unxz file.txt.xz 或者 xz -d file.txt.xz  #解压
```



## 文件格式转换

### dos2unix

### unix2dos

## 符号链接和硬链接命令

### ln



# 进程管理命令

# 用户管理命令

# 网络管理命令

# 系统信息命令

