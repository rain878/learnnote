# 数据类型

## 标量类型

### 字符串`(String)`

```php
<?php 
$txt1="Hello world!";
$txt2="What a nice day!";
var_dump($txt1);
echo $txt1;
echo $txt1 . " " . $txt2; //使用.把两个字符串连接起来
?>
```

### 整性`(Integer)`

```php
<?php 
$x = 5985;
var_dump($x);
echo $x;
?>
```

### 浮点型`(Float)`

```php
<?php 
$x = 10.125;
$a = 2.1e3;
var_dump($x);
echo $x;
?>
```

### 布尔值`(Boolean)`

```php
<?php 
$x = true;
var_dump($x);
echo $x;
?>
```

## 复合类型

### 数组`(Array)`

```php
<?php 
$x = array(1,2,3,4);
$y = array("key1"=>"value1","key2"=>"value2")
var_dump($x);
var_dump($y);
echo $x;
echo $y;
?>
```

### 对象`(Object)`

```php
class MyClass {
    public $property;
    function __construct($property) {
        $this->property = $property;
    }
}
$objectVar = new MyClass("example");
```

## 特殊类型

### 资源`(Special Types)`

```php
<?php 
$a = fopen("file.txt", "r");
?>
```

### NULL

```php
<?php 
$a = NULL;
?>
```

# 变量

变量以 $ 符号开始，后面跟着变量的名称

变量名必须以字母或者下划线字符开始

变量名只能包含字母、数字以及下划线（A-z、0-9 和 _ ）

变量名不能包含空格

变量名是区分大小写的（$y 和 $​Y 是两个不同的变量）

```php
<?php
$txt="Hello world!";
$x=5;
$y=10.5;
?>
```

## 作用域

### 全局作用域（Global Scope）

```php
<?php
$x=5;
$y=10;
function myTest()
{
    global $x,$y; //变量前面加global
    $GLOBALS['y']=$GLOBALS['x']+$GLOBALS['y']; //或者这样
    $y=$x+$y;
}
myTest();
echo $y; // 输出 15
?>
```



### 局部作用域（Local Scope）

```php
<?php
function myTest($x)
{
    echo $x;
}
myTest(5);
?>
```



### 静态作用域（Static Scope）

```php
<?php
function myTest()
{
    static $x=0;
    echo $x;
    $x++;
    echo PHP_EOL;    // 换行符
}
myTest();
myTest();
myTest();
?>
```



# 超级全局常量

```php
$GLOBALS
$_SERVER
$_REQUEST
$_POST
$_GET
$_FILES
$_ENV
$_COOKIE
$_SESSION
```

# 常量

## 自定义常量

常量名通常是大写字母。

可以包含字母和下划线，但不能以数字开头。

```php
define("name", "张三");	//普通常量
echo name; // 输出"张三"
//类常量
class student{
  const name = "张三";
}
echo student::name;
```

## 内置常量

### 核心 PHP 常量

```php
echo PHP_VERSION; // 输出 PHP 版本号，例如 "8.1.0"
echo PHP_MAJOR_VERSION; // 输出主版本号，例如 "8"
echo PHP_MINOR_VERSION; // 输出次版本号，例如 "1"
echo PHP_RELEASE_VERSION; // 输出发布版本号，例如 "0"
echo PHP_OS; // 输出操作系统名称，例如 "Linux"
echo PHP_SAPI; // 输出服务器 API 类型，例如 "apache2handler"
echo PHP_EOL; // 输出行结束符，例如 "\n" 或 "\r\n"
```

### 文件路径和目录常量

```php
echo __FILE__; // 输出文件的完整路径和文件名
echo __DIR__; // 输出文件的目录路径
echo __LINE__; // 输出当前行号
```

## 魔法常量

```php
echo __FILE__; // 输出文件的完整路径和文件名
echo __DIR__; // 输出文件的目录路径
echo __LINE__; // 输出当前行号
echo __FUNCTION__; // 输出当前函数的名称
echo __CLASS__; // 当前类的名称（包含命名空间）
echo __METHOD__; // 当前类的方法名称（包含类名）
echo __TRAIT__; // 当前trait的名称
echo __NAMESPACE__; // 当前命名空间的名称
```

### 其他内置常量

```php
echo DEFAULT_INCLUDE_PATH; // 输出默认的 include 路径
echo PEAR_INSTALL_DIR; // 输出 PEAR 的安装目录
echo PEAR_EXTENSION_DIR; // 输出 PEAR 扩展的安装目录
echo PHP_EXTENSION_DIR; // 输出 PHP 扩展的安装目录
echo PHP_BINDIR; // 输出 PHP 可执行文件的安装目录
echo PHP_LIBDIR; // 输出 PHP 的库文件目录
echo PHP_DATADIR; // 输出 PHP 数据文件目录
echo PHP_SYSCONFDIR; // 输出 PHP 配置文件目录
echo PHP_LOCALSTATEDIR; // 输出 PHP 本地状态文件目录
echo PHP_CONFIG_FILE_PATH; // 输出 php.ini 文件的搜索路径
```

# 类型比较

## 松散比较和严格比较`(==,===)`

```php
<?php
if(42 == "42") {
    echo '1、值相等';
}
if(42 === "42") {
    echo '2、类型相等';
} else {
    echo '3、类型不相等';
}
?>
```

# 运算符

## 1.算术运算符

```php
$a = 5;
$b = 3;
echo $a + $b; // 输出 8
echo $a - $b; // 输出 2
echo $a * $b; // 输出 15
echo $a / $b; // 输出 1.6667
echo $a % $b; // 输出 2
echo $a ** $b; // 输出 125
```

## 2.赋值运算符

```php
$a = 5;
$a += 3; // 等价于 $a = $a + 3;
echo $a; // 输出 8
$a -= 2; // 等价于 $a = $a - 2;
echo $a; // 输出 6
$a *= 2; // 等价于 $a = $a * 2;
echo $a; // 输出 12
$a /= 3; // 等价于 $a = $a / 3;
echo $a; // 输出 4
$a %= 3; // 等价于 $a = $a % 3;
echo $a; // 输出 1
```

## 3.比较运算符

```php
$a = 5;
var_dump($a == 5); // 输出 bool(true)
var_dump($a === 5); // 输出 bool(true)
var_dump($a === "5"); // 输出 bool(false)
var_dump($a != 3); // 输出 bool(true)
var_dump($a <> 3); // 输出 bool(true)
var_dump($a !== "5"); // 输出 bool(true)
var_dump($a < 5); // 输出 bool(false)
var_dump($a > 3); // 输出 bool(true)
var_dump($a <= 5); // 输出 bool(true)
var_dump($a >= 3); // 输出 bool(true)
//组合比较，如果左边小于右边，返回-1；如果相等，返回0；如果大于，返回1
echo $a <=> 5; // 输出 0
```

## 4.逻辑运算符

```php
var_dump($a == 5 && $b == 3); // 输出 bool(true)
var_dump($a == 5 || $b == 4); // 输出 bool(true)
var_dump(!$a); // 输出 bool(false)
var_dump($a == 5 xor $b == 3); // 输出 bool(false)
```

## 5.位运算符

```php
$a = 6; // 110
$b = 3; // 011
echo $a & $b; // 输出 2 (010)
echo $a | $b; // 输出 7 (111)
echo $a ^ $b; // 输出 5 (101)
echo ~$a; // 输出 -7
echo $a << 1; // 输出 12 (1100)
echo $a >> 1; // 输出 3 (011)
```

## 6.字符串运算符

```php
$str1 = "Hello";$str2 = "World";
echo $str1 . " " . $str2; // 输出 "Hello World"
$str1 .= " World"; // 连接赋值
echo $str1; // 输出 "Hello World"
```

## 7.数组运算符

```php
$array1 = array("a" => "apple", "b" => "banana");
$array2 = array("b" => "blueberry", "c" => "cherry");
$result = $array1 + $array2;
print_r($result); // 输出 Array ( [a] => apple [b] => banana [c] => cherry )
var_dump($array1 == $array2); // 输出 bool(false)
var_dump($array1 === $array2); // 输出 bool(false)
var_dump($array1 != $array2); // 输出 bool(true)
var_dump($array1 <> $array2); // 输出 bool(true)
var_dump($array1 !== $array2); // 输出 bool(true)
```

## 8.执行运算符

```php
$output = `ls -l`;
echo "<pre>$output</pre>";
```

## 9.错误控制运算符

```php
$file = @file('non_existent_file.txt'); // 如果文件不存在，不会抛出错误
```

## 10. 递增/递减运算符

```php
$a = 5;
echo ++$a; // 输出 6
echo $a++; // 输出 5，$a 变为 6
echo --$a; // 输出 5
echo $a--; // 输出 5，$a 变为 4
```

## 11.三元运算符

```php
$a = 5;
$b = 10;
$result = ($a > $b) ? $a : $b;
echo $result; // 输出 10
```

## 12. 空合并运算符

```php
$username = $_GET['user'] ?? 'nobody';
echo $username; // 如果 `$_GET['user']` 不存在，输出 'nobody'
```

