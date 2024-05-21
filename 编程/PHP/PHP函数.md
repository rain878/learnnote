

# 输入/输出函数

## 1.用户输入处理

`filter_input()`

``filter_var()`

 `htmlspecialchars()`

## 2.输出过滤

`htmlspecialchars()`, `strip_tags()`, `htmlentities()`

# 字符串处理函数

## 1.字符串查找和替换

 `strpos()`, `str_replace()`, `preg_match()`

## 2.字符串长度和截取

 `strlen()`, `substr()`, `mb_strlen()`

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

`imagecreatefromjpeg()`, `imagecopyresized()`, `imagepng()`

## 3.加密解密

`password_hash()`, `password_verify()`, `md5()`, `sha1()`