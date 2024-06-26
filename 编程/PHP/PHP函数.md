

# 输入/输出函数

## 1.用户输入处理

`isset`

`filter_input()`

`filter_var()`

`htmlspecialchars()`

## 2.输出过滤

`htmlspecialchars()`, `strip_tags()`, `htmlentities()`

# 条件判断

## 是否为空

`isset()`函数用来检查变量是否已设置并且非**NULL**。如果变量已设置并且值不为NULL，则返回true，否则返回false

```php
$a = 1;
$b = null;
if (isset($a)) {
    echo "变量 $a 存在";
}
if (isset($a, $b)) {
    echo "变量 $a 和 $b 都存在";
} else {
    echo "至少有一个变量不存在";
}
```

`empty()`

## 判断类型

`is_string()`用于检查一个变量是否是**字符串**类型。如果是返回 true；如果不是，将返回false

```php
$var = "Hello, World!";
if (is_string($var)) {
    echo "变量 $var 是字符串类型";
} else {
    echo "变量 $var 不是字符串类型";
}
```

`in_array()`中用来检查一个值是否存在于数组中。如果存在，函数返回 `TRUE`；如果不存在，返回 `FALSE`

```php
$array = [1, 2, 3, '4', '5'];
if (in_array(4, $array)) {
    echo "4 在数组中";
} else {
    echo "4 不在数组中";
}
```



# 字符串处理函数

## 1.字符串查找和替换

 `strpos()`, `str_replace()`,

 `preg_match()`函数用于执行一个正则表达式匹配

```

```

`mb_strpos()` 函数和`mb_stripos()`在PHP中用于查找一个字符串在另一个字符串中第一次出现的位置，返回它的位置；如果没有找到，返回 `false`

```php
$position = mb_strpos("Hello World", "HELLO");
// 返回值将为 false，因为 "Hello" 和 "HELLO" 大小写不一致
$position = mb_stripos("Hello World", "HELLO");
// 返回值将为 0，因为 "HELLO" 在不区分大小写的情况下出现在 "Hello World" 的开头
$text = "Hello, 世界";
$pos = mb_strpos($text, "世");
if ($pos !== false) {
    echo "找到位置：$pos";
} else {
    echo "未找到";
}
结果：
找到位置：7
```

`strstr()`和`stristr`用于查找字符串首次出现的位置的函数。找到返回从该字符串开始到原字符串末尾的子字符串。如果未找到，它将返回 `false`

```php
// 搜索 "sub" 字符串
$part = strstr("Hello, world!", "world");
// 输出: "world!"
echo $part;
// 使用 $beforeNeedle 参数
$partBefore = strstr("Hello, world!", "world", true);
// 输出: "Hello, "
echo $partBefore;
strstr() 是大小写敏感的，而 stristr() 不区分大小写。
```



## 2.字符串长度和截取

`strlen()`, `substr()`, 

`mb_strlen()`

`mb_substr()`用于返回字符串的子字符串

```php
$str = "你好，世界！";
echo mb_substr($str, 0, 6); // 输出 "你好，世"
echo mb_substr($str, 3);    // 输出 "界！"
echo mb_substr($str, -4, 2); // 输出 "界"
```



## 3.字符串转换

 `strtolower()`, `strtoupper()`, `ucfirst()`

## 4.字符串分割和连接

 `explode()`, `implode()`, `join()`

## 5.字符串格式化

 `trim()`, `nl2br()`, `htmlspecialchars()`

# 文件处理函数

## 1.文件读写

`file_get_contents()`, `file_put_contents()`, `fopen()`, `fclose()`

## 2.文件操作

 `file_exists()`, `is_file()`, `unlink()`, `rename()`

## 3.目录操作

 `mkdir()`, `rmdir()`, `opendir()`, `closedir()`

## 4.文件路径

 `basename()`, `dirname()`, `realpath()`

## 5.文件上传处理

 `move_uploaded_file()`, `is_uploaded_file()`, `$_FILES[]`

# 数学函数

## 1.数学运算

`sqrt()`, `pow()`, `abs()`, `round()`

## 2.三角函数

`sin()`, `cos()`, `tan()`, `deg2rad()`, `rad2deg()`

## 3.随机数

 `rand()`, `mt_rand()`, `random_int()`

# 数据库函数

## 1.MySQL相关函数

 `mysqli_connect()`, `mysqli_query()`, `mysqli_fetch_assoc()`

## 2.PDO相关函数

 `PDO::__construct()`, `PDO::query()`, `PDOStatement::fetch()`

# 数组处理函数

## 1.数组遍历

 `foreach()`, `array_walk()`, `array_map()`

## 2.数组排序

 `sort()`, `asort()`, `ksort()`

## 3.数组合并和分割

 `array_merge()`, `array_slice()`, `explode()`

## 4.数组信息

`count()`, `array_key_exists()`, `array_search()`

# 时间和日期函数

## 1.日期格式化

 `date()`, `strftime()`, `strtotime()`

## 2.日期计算

`strtotime()`, `date_add()`, `date_sub()`

## 3.时区设置

`date_default_timezone_set()`, `gmdate()`, `mktime()`

# 错误处理函数

## 1.错误报告

`error_reporting()`, `ini_set()`, `set_error_handler()`

## 2.异常处理

`try {} catch {}`, `throw new Exception()`, `set_exception_handler()`

# 其他常用函数

## 1.网络通信

`curl_init()`, `file_get_contents()`, `stream_socket_client()`

## 2.图像处理

`imagecreatefromjpeg()`, `imagecopyresized()`, `imagepng()`,`exif_imagetype()`

## 3.编码及加解密

`password_hash()`, `password_verify()`, `md5()`, `sha1()`,`json_decode`,`base64_decode`,``

## 4.执行系统外部命令

`exec()`,`passthru()`,`system()`,`shell_exec()`