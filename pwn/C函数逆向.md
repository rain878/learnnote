# 设置缓冲区

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



# 输出函数

## put()

```c
//函数原型：
int put(int c);

put("hackme");//函数 put 会将字符 c 写入到标准输出流，并返回写入成功的字符，如果出错则返回 EOF
```

## putchar()

```c
//函数原型：
int putchar(int c);

putchar("a");	//常用于将单个字符输出到控制台或文件中
```

## printf()

```c
//函数原型：
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

# 输入函数

## gets()

```

```

# 系统调用函数
