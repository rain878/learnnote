# 设置超时

## alarm()

```c
//设置一个定时器，指定时间发送一个"sigalrm"信号给当前进程
#include <unistd.h>
unsigned int alarm(unsigned int seconds);
```

## signal()

```c
//用于设置信号处理函数，以处理接收到的信号
#include <signal.h>
void (*signal(int signum, void (*handler)(int)))(int);
//signum：整数，表示信号的编号。
//handler：函数指针，指向信号处理函数。
例子，和alarm搭配使用
#include <stdio.h>
#include <unistd.h>
#include <signal.h>
void timeout(int sig) {
    printf("Time out!\n");
}
int main() {
    alarm(5); // 5秒后发送SIGALRM信号
    signal(10, timeout); // 设置信号处理函数
    return 0;
}
```

# 缓冲区

## setbuf()

```c
//函数原型：
void setbuf(FILE *stream, char *buffer);
//例子：
setbuf(stdin,0);	//意味着当程序从标准输入流中读取数据时，数据将立即被传递给程序，而不会在缓冲区中等待
setbuf(stdout,0);	//意味着程序中输出将会立即被写入到输出设备，而不会先存储在缓冲区中等待。
```

## setvbuf()

```c
//函数原型：
int setvbuf(FILE *stream, char *buffer, int mode, size_t size);
int mode：缓冲方式，可以是以下三种值之一：
	_IOFBF：全缓冲模式（Full Buffering）对应 2
	_IOLBF：行缓冲模式（Line Buffering）对应 1
	_IONBF：无缓冲模式（No Buffering）对应 0
  
//例子
setvbuf(stdout,0,2,0);
```

## fflush()

`fflush()` 函数用于强制将流缓冲区中的数据写入文件或刷新缓冲区。

```

```

# 转换函数

## atoi()

```c
//用于将字符串转换为整数。它接受一个表示数字的字符串作为参数，并返回相应的整数值。
#include<ctype.h>
char str1[] = "123",str2[] = "-456",str3[] = "abc";
int num = atoi(str1);	// num的值将是-456
int num = atoi(str2);	// num的值将是123
int num = atoi(str3);	// num的值将是0，因为无法将字符串转换为整数

```

# IO操作

## 输出函数

### write()

```c
#include <unistd.h>
ssize_t write(int fd, const void *buf, size_t count);
//参数一：fd表示文件描述符，指定要写入数据的文件。一般是1
//参数二：buf表示要写入的数据的缓冲区的指针。
//参数三：count表示要写入的数据的字节数。
```

### put()

```c
//函数原型：
int put(int c);
put("hackme");//函数 put 会将字符 c 写入到标准输出流，并返回写入成功的字符，如果出错则返回 EOF
```

### putchar()

```c
//函数原型：
int putchar(int c);
putchar("a");	//常用于将单个字符输出到控制台或文件中
```

### printf()

```c
//函数原型：
#include<stdio.h>
int printf(const char *format, ...);
printf("hackme");
//整数类型：
%d：以十进制形式输出带符号整数。
%u：以十进制形式输出无符号整数。
%x、%X：以十六进制形式输出整数，小写或大写字母。
%o：以八进制形式输出整数。
//浮点数类型：
%f：以十进制形式输出浮点数。
%e、%E：以科学计数法形式输出浮点数，小写或大写字母。
%g、%G：根据数值的大小自动选择 %f 或 %e 格式输出，小写或大写字母。
%a、%A：以十六进制形式输出浮点数，小写或大写字母。
//字符类型：
%c：输出单个字符。
%s：输出字符串。
%p：输出指针地址。
//其他类型：
%%：输出百分号字符。
```

### sprinf()

```c
//用于将格式化的数据写入一个字符串中。
#include <stdio.h>
int sprintf(char *str, const char *format, ...);
//参数一：str指向字符数组的指针，用于存储格式化后的字符串。
//参数二：format格式化字符串，包含了要输出的内容以及格式说明符。
//参数三：...可变数量的参数，用于填充格式字符串中的格式说明符。
例子：
#include <stdio.h>
int main() {
    char str[100];
    int num = 123;
    float fnum = 3.14;
    sprintf(str, "Integer: %d, Float: %.2f", num, fnum);	// 将格式化的数据写入到字符串str中
    printf("Formatted string: %s\n", str);	// 打印格式化后的字符串
  	//结果：Formatted string: Integer: 123, Float: 3.14
    return 0;
}
```



## 输入函数

### gets()

```c
#include <stdio.h>
char *gets(char *s);
//参数一：s字符数组的指针，用于存储从标准输入中读取的数据。遇到换行符才停止读取
```

### read()

```c
#include <unistd.h>
ssize_t read(int fd, void *buf, size_t count);
//参数一：fd从哪个文件描述符中读取数据。0 表示标准输入（stdin），1 表示标准输出（stdout），2 表示标准错误（stderr）
//参数二：buf表示缓冲区，用于存储读取的数据。
//参数三：count表示要读取的字节数，即缓冲区的大小。
```



# 内存操作

## memset()

```c
// memset()是 C 语言标准库 <string.h> 中的一个函数，用于设置一块内存的内容为指定的值
void *memset(void *ptr, int value, size_t num);
//参数一：ptr指向要填充的内存块的指针。
//参数二：value为内存设置的值
//参数三：num要设置的字节数。
#include <stdio.h>
#include <string.h>
int main() {
    char buffer[50];
    memset(buffer, 'A', sizeof(buffer));
    return 0;
}
```



# 系统调用函数

## mprotect()

在Unix和类Unix操作系统中用于更改内存保护属性的系统调用。

```c
#include <sys/mman.h>
int mprotect(void *addr, size_t len, int prot);
//参数一：addr修改内存的开始指针
//参数二：len修改内存的长度（以字节为单位）
//参数三：prot修改成的属性，PROT_NONE：0，表示无权限、PROT_READ：1，表示可读权限、PROT_WRITE：2，表示可写权限、PROT_EXEC：4，表示可执行权限。
```

# 其他函数

## getegid()

```c
//用于获取调用进程的有效组ID（Effective Group ID）。它通常用于确定进程所属的用户组。
#include <unistd.h>
gid_t getegid(void);
```

## setresgid()

```c
//用于设置进程的实际、有效和保存的组ID（Real, Effective, Saved Group ID）。它允许动态地更改进程所属的组。
#include <unistd.h>
int setresgid(gid_t rgid, gid_t egid, gid_t sgid);
//rgid 表示实际组ID（Real Group ID）
//egid 表示有效组ID（Effective Group ID）
//sgid 表示保存的组ID（Saved Group ID）
```

