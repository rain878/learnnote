```shell
#导入到HDFS
sqoop import \
--connect jdbc:mysql://127.0.0.1:3306/student \
--username root \
--password Niit@123 \
--table product \
--m 1 \
--target-dir /product

#导出到MySql数据
sqoop export \
--connect jdbc:mysql://127.0.0.1:3306/student?characterEncoding=utf-8 \
--username root \
--password Niit@123 \
--table product \
--export-dir /product

#job相关
sqoop job \
--create job1 \
-- import \
--connect jdbc:mysql://127.0.0.1:3306/student \
--username root \
--password Niit@123 \
--table product \
--m 1 \
--target-dir /job_result

sqoop job --list
sqoop job --show job1
sqoop job --exec job1
sqoop job --delete job1
#sqoop免密登录
sqoop job \
--create job1 \
-- import \
--connect jdbc:mysql://127.0.0.1:3306/student \
--username root \
--table product \
--m 1 \
--password-file /passwd/mysqlpasswd
--target-dir /job_result
```

