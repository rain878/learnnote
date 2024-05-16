# 安装

# 启动

```bash
#添加环境变量
vim ~/.bashrc 
exprot
#启动
./bin/flume-ng agent --conf conf/ --name a1 --conf-file job/flume-netcat-logger.conf
./bin/flume-ng agent -c conf/ -n a1 -f job/flume-dir-hdfs.conf 
```

## 配置

## 端口监听配置

`/flume/job`目录下`flume-netcat-logger.conf`配置文件

```shell
# 当前Agent起名a1
a1.sources = r1 #接收者
a1.sinks = k1 #发送者
a1.channels = c1  #缓冲区
#配置接收
a1.sources.r1.type = netcat #设置接收类型netcat网络端口
a1.sources.r1.bind = localhost  #接收地址
a1.sources.r1.port = 44444  #接收端口
#配置发送者
a1.sinks.k1.type = logger #配置控制台logger类型
#配置缓冲区
a1.channels.c1.type = memory  #缓冲区类型
a1.channels.c1.capacity = 1000  #缓冲区大小
a1.channels.c1.transactionCapacity = 100  #缓冲区接收到的100个就提交事务
#发送者->缓冲区->接收者->控制台(其他)
a1.sources.r1.channels = c1 #接收者和缓冲区进行连接
a1.sinks.k1.channel = c1 #发送者和缓冲区进行连接
```

## 文件监听配置

`/flume/job`目录下`flume-file-hdfs.conf`配置文件

```bash
#当前Agent起名a1
a1.sources = r1
a1.sinks = k1
a1.channels = c1
#配置接收
a1.sources.r1.type = exec	#监听文件变化使用exec
a1.sources.r1.command = tail -F /export/data/flumedata/mail.log	#监听文件地址
#配置发送者
a1.sinks.k1.type = hdfs #发送目的地
a1.sinks.k1.hdfs.path = hdfs://node1:8020/flume/%Y%m%d/%H	#发送目的地具体URL
a1.sinks.k1.hdfs.filePrefix = logs-	#上传文件的前缀
a1.sinks.k1.hdfs.round = true	#是否按照时间滚动文件夹
a1.sinks.k1.hdfs.roundValue = 1	#多少时间单位创建一个新的文件夹
a1.sinks.k1.hdfs.roundUnit = hour	#重新定义时间单位
a1.sinks.k1.hdfs.useLocalTimeStamp = true	#是否使用本地时间戳
a1.sinks.k1.hdfs.batchSize = 100	#积攒多少个 Event 才 flush 到 HDFS 一次
a1.sinks.k1.hdfs.fileType = DataStream	#设置文件类型，可支持压缩
a1.sinks.k1.hdfs.rollInterval = 30	#多久生成一个新的文件,30秒后临时文件变正式文件
a1.sinks.k1.hdfs.rollSize = 134217700	#设置每个文件的滚动大小
a1.sinks.k1.hdfs.rollCount = 0	#文件的滚动与 Event 数量无关
#配置缓冲区
a1.channels.c1.type = memory #缓冲区类型
a1.channels.c1.capacity = 1000 #缓冲区大小
a1.channels.c1.transactionCapacity = 100 #缓冲区接收到的100个就提交事务
#发送者->缓冲区->接收者->控制台(其他)
a1.sources.r1.channels = c1	#接收者和缓冲区进行连接
a1.sinks.k1.channel = c1	#发送者和缓冲区进行连接
```

`/flume/job`目录下`flume-dir-hdfs.conf`配置文件

```shell
# 命名组件
a1.sources = r1
a1.sinks = k1
a1.channels = c1
# 配置接收
a1.sources.r1.type = spooldir
a1.sources.r1.spoolDir = /export/data/upload
a3.sources.r3.fileSuffix = .COMPLETED	#临时文件以.completed结尾
a1.sources.r1.ignorePattern = ([^ ]*\.tmp)	# 忽略所有以.tmp结尾的文件，不上传
# 配置发送
a1.sinks.k1.type = hdfs
a1.sinks.k1.hdfs.path = hdfs://node1:8020/flume/upload/%Y%m%d/%H
a1.sinks.k1.hdfs.filePrefix = upload-	# 上传文件的前缀
a1.sinks.k1.hdfs.round = true	# 是否按照时间滚动文件夹
a1.sinks.k1.hdfs.roundValue = 1	# 多少时间创建一个新的文件夹
a1.sinks.k1.hdfs.roundUnit = hour	# 定义时间单位
a1.sinks.k1.hdfs.useLocalTimeStamp = true	# 是否使用本地时间戳
a1.sinks.k1.hdfs.batchSize = 100	# 多少个event才flush到HDFS
a1.sinks.k1.hdfs.fileType = DataStream	# 设置文件类型，支持压缩格式
a1.sinks.k1.hdfs.rollInterval = 30	# 多久生成一个新的文件（单位为秒）
a1.sinks.k1.hdfs.rollSize = 134217700	# 设置每个文件的滚动大小
a1.sinks.k1.hdfs.rollCount = 0	# 设置滚动与event数量无关
#配置缓冲区
a1.channels.c1.type = memory	# 配置channel
a1.channels.c1.capacity = 1000
a1.channels.c1.transactionCapacity = 100
#发送者->缓冲区->接收者->控制台(其他)
a1.sources.r1.channels = c1	#接收者和缓冲区进行连接
a1.sinks.k1.channel = c1	#发送者和缓冲区进行连接
```

