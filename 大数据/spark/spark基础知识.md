[TOC]



# Spark基础常识

Spark是Apache基金会维护的一款基于内存的分布式计算(分析)引擎(框架)

Spark由Scala语言编写，支持Scala、Java、python、R等编程语言

Spark各个模块介绍

1. Spark Core：是提供了Spark最基础核心的功能
2. Spark SQL： 用于处理结构化和半结构化数据的组件（模块）
3. Spark Streaming：针对实时数据进行流式计算的组件
4. Spark MLib： 机器学习算法库
5. Spark GraphX：图计算的框架和算法库

Spark优缺点

- 优点：并行计算，扩展性，高性能，速度快，易用性
- 缺点：学习成本高，需要较高的硬件资源，集成工具少，内存消耗大

------

# Spark的部署方式

1. 本地方式

   便于开发、调试、学习、测试，节省资源，将Spark应用程序和资源一起打包在本地运行

2. Standalone模式

   适用于单机环境，不需要依赖其他的集群管理器，方便开发和测试，Master负责管理集群中的资源分配和任务调度，Executor负责执行用户提交的Spark应用程序

3. 集群模式（Yarn，Mesos，K8s模式）

   需要依赖其他的集群管理器（Yarn、Mesos、K8S），使用Yarn模式安装Spark，需要配置adoop组件有ResourceManager、NodeManager。Spark的应用程序运行在Spark集群中。作为生产环境进行部署使用

   - 客户模式：Spark的应用程序是在客户端上运行，于集群进行通讯

------

# Scala相关知识

scala中

- var定义变量
- val定义常量
- def定义方法
- class定义类
- trait定义特质
- case class定义样例类
- extends继承类
- ->表示函数

scala中的集合：

- 数组
- List（有序且重复）
  - 如何创建一个空集合：val list=List()
  - List(1,2,3,4,5,6).foldLeft(0) 求结果 0+1+2+3+4+5+6=21
- 元组 不能修改，获取数据用的序号
- Map 键值对new Map()
- Set 无序且不可重复的集合
- 定义构造函数：在类定义中定义一个名为this的方法
- 定义一个类，该有两个成员变量：class A(val b:String,val c:Int){}
- 伴生对象：一个包含于类同名的对象，伴生类和伴生对象必须在同一个文件内
  - 伴生类：一个于对象同名的类，伴生类和伴生对象必须在同一个文件内
- 匹配模式：一种匹配值的方式

------

# Spark RDD相关知识

RDD：分布式弹性数据集，是一种数据类型。

RDD分布式转换算子、行动算子

转换算子

​	map：对RDD的每个元素应用函数、返回一个新的RDD

​	filter：返回一个新的RDD（新的RDD是原RDD的子集），包含应用函数后返回值为true的原始元素，不会触发shuffle排序

​	flagMap：每个输入元素可以映射到0或多个输入元素

​	reduceBykey：适用于键值对的RDD，返回一个新的RDD，其中每个键的值是应用函数聚合的结果

​	join：对于两个键值对RDD，返回一个新的RDD，包含两个RDD中键相同的元素的组合

​	distinct：返回一个新的RDD，对原RDD中的数据进行去重

​	repartitions：返回一个新的RDD，可以将RDD中的元素根据某些条件进行重新分区

​	union：对源RDD和参数RDD求并集，返回一个新的RDD

​	intersection：对源RDD和参数RDD求交集，返回一个新的RDD

​	substract：对源RDD和参数RDD求差集，返回一个新的RDD

​	sortBy：根据指定的规则对数据源中的数据进行排序，默认是升序，返回一个新的RDD

​	zip：相同位置的数据拉取到一块

​	groupBy：将数据根据指定的规则进行分组，返回一个新的RDD

​	reduce：聚合RDD中的所有元素，先聚合分区内数据，在聚合分区间数据

​	collect：将RDD转换成数组

​	count：将返回RDD中数据的个数

​	first：将返回RDD中的第一个元素

​	take：将返回RDD中的n个元素

​	fold：根据RDD中的元素，进行累加计算

​	countByKey：统计每种Key的个数

​	saveAsTextFile：将RDD保存到文件系统中

​	foreach：对RDD中元素进行遍历

## 计算题

用Spark读取一个文本文件并创建一个RDD

```scala
val rdd = sparkContext(sc).textFile(path)
```

将一个RDD中的元素进行分组，并返回每个分组中的最大值

```scala
val rdd2 = rdd.groupBy(x=>y).mapValues(_.max)
val rdd2 = rdd.flatMap(_.split(" ")).groupBy(x=>y).mapValues(_.max)
```

将两个进行join连接

```scala
val rdd1 = sc.makeRDD(List((1,"A"),(2,"B")))
val rdd2 = sc.makeRDD((1,"C"),(3,"D"))
val res = rdd1.join(rdd2)	//将rdd1和rdd2进行连接
res = (1,("A","C"))
```

求分组内的和

```scala
val data = sc.makeRDD(List((1,2),(3,4),(5,6),(7,8)))
val res = data.reduce((x,y)=>(x._1 + y_.1, x._2 + y._2))
res = (16,20)//1+3+5+7=16,2+4+6+8=20
```

将两个

```scala
val rdd1 = sc.makeRDD(List((1,2),(3,4),(3,6)))
val rdd2 = sc.makeRDD(List((3,9)))
val res = rdd1.join(rdd2)
print(res.collect().mkString(","))
```

统计包含“A”字符的单词

```scala
val rdd = sc.makeRDD(List("Hadoop","Scala","Python"))
val res = rdd.filter(_.contains("a")).count
res = 2
```

## 代码题

​	SparkRDD，以逗号拆分单词，将结果转换成字符串进行输出

```scala
val sparkConf = new SparkConf.setMaster("local[*]").setAppName("Spark")
val sc = new SparkContext(sparkConf)
```

------

# SparkSQL

SparkSQL：用于处理结构化和半结构化数据的模块

数据类型：DataFrame、Dataset

DataFrame和Dataset之间相差了一个样例类的封装

DataFrame和Dataset都是分布式数据表

RDD、DataFrame、Dataset三者的转换

​	RDD 转 DataFrame：toDF()

​	RDD 转 Dataset：RDD[].toDS

​	DataFrame 转 RDD：(内容).rdd(内容).toDF()

​	DataFrame 转 Dataset：as[]

​	Dataset 转 RDD：(内容).rdd

​	Dataset 转 DataFrame：(内容).toDF()

读取JSON文件：Spark.read.json()  或者 spark.read.format("json")

将DataFrame保存数据库：DataFrame.write.format("mysql")

临时试图

- 创建或替换临时试图：createOrReplaceTempView
- 创建全局临时试图：createGlobalTemView
- 创建临时试图：createTempView

执行原生SQL语句：spark.sql("原生语句")

用户自定义函数：UAF，UDAF

DataFrame和Dataset相关函数

- count()	计算行的总数
- sum() ：求某一列的总和
- max()：求某一列的最大值
- select()：对指定列数据进行查询
- filter()：对指定列数据进行过滤
- groupBy()：对指定规则进行分组
- orderBy()：对指定列进行排序
- join()：对两个DataFrame(Dataset)进行连接
- distinct()：对指定列的数据进行去重

代码题：RDD转换Dataset

```scala
case class People(val name:String,val address:String)
val sparkConf = new SparkConf().setMaster("local[*]").setAppName("spark")
val spark = SparkSession.builder().config(sparkConf).getOrCreate()
import spark.implicts
```

------

# Spark Streaming

是实时数据的流式计算，在实时数据处理和交互式查询上支持实时数据处理，

spark Streaming 数据处理的基本单元是：DStream

DStream是流式处理的输入数据流

checpoint 的目的是计算累积的结果，避免数据丢失，与之使用的函数，updataStateByKey	reduceByKeyAndWindow

将实时数据DStream转换成Dataset或者DataFrame或者RDD

transform只有转换的作用

foreachRDD转换和输出的作用

Spark Streaming的程序必须要有输出语句：print foreachRDD saveAsTextFiles

使用窗口操作来计算近30分钟的数据，窗口长度：30分钟，滑动间隔：30分钟

代码题：转换 transform

```scala
val sparkConf = new SparkConf().setMaster("local[*]").setAppName("spark")
val ssc = new StreamingContext(sparkConf,Seconds(3))
```
