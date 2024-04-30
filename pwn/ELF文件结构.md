# ELF文件

## ELF三种形式

- 可重定位目标文件：hello.o
- 可执行文件：hello
- 共享文件：hello.so、libc.so.6文件

## 文件结构

ELF 文件头（ELF Header）：

> ​	 ELF 文件的开头包含一个文件头，它包含了描述 ELF 文件结构的信息，如文件类型、目标体系结构、入口地址等。ELF 文件头的大小是固定的，通常为 52 字节。

程序头表（Program Header Table）： 

> ​	程序头表是一个可选的部分，用于描述 ELF 文件在内存中的装载方式。它包含了各个段在内存中的位置和大小等信息。对于可执行文件来说，程序头表是必需的，而对于共享对象文件和可重定位文件来说，程序头表可以为空。

节头表（Section Header Table）：

> ​	 节头表包含了描述 ELF 文件中各个节（Section）的信息，如名称、偏移量、大小等。节头表是可选的，有些 ELF 文件中可能没有节头表。对于可执行文件来说，节头表通常包含了代码段、数据段等信息。

动态表（Dynamic Table）：



符号表（Symbols Table）:

> 



节（Section）：

> ​	 节是 ELF 文件的实际内容，它包含了各种数据和代码。常见的节包括代码段、数据段、符号表、字符串表等。节的类型和内容根据文件的用途和类型而不同。

# 查看ELF文件相关命令

## objdump

```shell
objdump
```



## readelf

```shell
readelf -h pwn	#查看ELF头
readelf -l pwn	#查看program headers
readelf -S pwn	#查看section headers
readelf -SW pwn	# -W 参数可以对齐，方便查看
```



## ldd

```shell
#用于显示一个可执行文件或者共享库所依赖的动态链接库
ldd pwn
```

## nm

```shell
nm pwn
```

# 动态链接下的ELF

在 ELF 运行时，当第一次执行 puts 函数时，程序会经过以下几个步骤：

1. 调用 puts 函数： 

   > ​	程序中的某个部分需要调用 puts 函数来输出字符串。

2. 查找 PLT 表：

   > ​	由于 ELF 文件中的函数调用通常是动态链接的，因此程序需要在 PLT（Procedure Linkage Table）表中查找 puts 函数的地址。PLT 表是一个特殊的数据结构，用于实现延迟绑定（Lazy Binding），即直到第一次调用函数时才解析函数地址。

3. PLT 表中的跳转指令：

   > ​	PLT 表中的条目通常是一系列跳转指令，用于实现动态链接。当程序第一次调用 puts 函数时，会跳转到 PLT 表中相应条目的位置。

4. 动态链接器的介入： 

   > ​	当程序执行到 PLT 表中的跳转指令时，控制权会被转移到动态链接器（如 ld.so）中。动态链接器负责解析 puts 函数的地址，并将其替换到 PLT 表中的相应条目中。

5. 调用 puts 函数：

   > ​	PLT 表中的跳转指令已经被动态链接器修改为 puts 函数的实际地址，因此控制权会跳转到 puts 函数的入口点，开始执行 puts 函数。

6. 后续调用： 

   > ​	在程序的后续执行过程中，由于 puts 函数的地址已经被缓存到了 PLT 表中，因此程序会直接跳转到 puts 函数的入口点，而不再需要经过动态链接器的介入。
