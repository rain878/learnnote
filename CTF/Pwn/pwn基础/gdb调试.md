# GDB

## 介绍

​	GNU调试器（GNU Debugger）的缩写，是一个强大的命令行调试工具，用于调试C、C++等编程语言编写的程序。它可以帮助开发者诊断和修复程序中的错误，包括内存泄漏、段错误、逻辑错误等。

## 配置

```shell
set context-output /dev/pts/3	#设置输出
#当调试程序遇到system创建子线程时，gdb会退出，则可以设置
set follow-fork-mode parent
```

## 命令

```shell
r 或 run	#运行
start	#运行到gdb自己认为的入口点

b 或 break	#下断点
b main
b *0x12345678

s 或 step	#步入，进入函数
n 或 next	#单步，跳过函数
fin 或 finish	#让程序执行函数，并停止在函数返回处

x/[count][format] address	#查看地址
x/20gx 0x12345678
hexdump 0x12345678
telescope 0x12345678

stack	#查看栈
plt	#查看plt表
got	#查看got表
heap #查看堆
vis_heap_chunks #查看堆内容
parseheap #查看堆信息
bins #查看bins
regs	#查看寄存器
vmmap	#查看当前进程的内存映射信息
watch *0x408018	#关注某个内存，当对这个内存有读写操作时，断在这里

distance 0xdde0 0xddf0	#计算偏移
cyclic	#生成字符，计算偏移

set *0x7fffffffdd60=0xaabbccdd	#尽量四个字节改

exit 或 quit #退出
```
