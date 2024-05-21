[TOC]



# Spark基础常识

Spark是Apache基金会维护的一款基于内存的分布式计算(分析)引擎(框架)

Spark由Scala语言编写，支持Scala、Java、python、R等编程语言

Spark各个模块介绍

1. `Spark Core`：是提供了Spark最基础核心的功能
2. `Spark SQL`： 用于处理结构化和半结构化数据的组件（模块）
3. `Spark Streaming`：针对实时数据进行流式计算的组件
4. `Spark MLib`： 机器学习算法库
5. `Spark GraphX`：图计算的框架和算法库

Spark优缺点

- 优点：并行计算，扩展性，高性能，速度快，易用性
- 缺点：学习成本高，需要较高的硬件资源，集成工具少，内存消耗大

------

# Spark的部署方式

## 1.本地方式

便于开发、调试、学习、测试，节省资源，将Spark应用程序和资源一起打包在本地运行

## 2.Standalone模式

适用于单机环境，不需要依赖其他的集群管理器，方便开发和测试，Master负责管理集群中的资源分配和任务调度，Executor负责执行用户提交的Spark应用程序spark-submit命令可提交应用程序，driver负责分发带代码和依赖到集群

## 3.(Cluster)集群模式（Yarn，Mesos，K8s模式）

需要依赖其他的集群管理器（Yarn、Mesos、K8S），使用Yarn模式安装Spark，需要配置hadoop组件有ResourceManager、NodeManager。Spark的应用程序运行在Spark集群中。作为生产环境进行部署使用

## 4.客户模式(Client)

Spark的应用程序是在客户端上运行，于集群进行通讯

# Scala相关知识

scala中

- var定义变量
- val定义常量
- def定义方法
- class定义类
- trait定义特质
- case class定义样例类
- extends继承类
- =>表示函数

## scala中的集合类型

- 数组`(Array)`可变无序
  - 创建数组：`val ary = Array(12,45,33)`

- 列表`(List)`有序不变
  - 创建空列表：`val list=List()`
  - 添加列表：`val otherlist="apache"::list`
  - List(1,2,3,4,5,6).foldLeft(0) 求结果 0+1+2+3+4+5+6=21
- 元组 `(Tuple)`不可变不重复
  - 创建元组：`val tuple = ("bigdata",123,2.1)`

- 映射`(Map)`默认不可变
  - 创建键值对：`val str = Map("zzz"->"123","aaa"->"321")`

- 集合`(Set)` 无序不可重复，默认不可变
  - 创建集合：`var myset = Set("aaa","bbb")`

- 迭代器`(Iterator)`不是集合，是访问集合的方法
- 序列类`(Seq)`用于按顺序访问集合中的元素

## 面向对象编程

类`(class)`

- 定义一个类，两个变量：`class A(val b:String,val c:Int){}`

对象`(object)`

特质`(trait)`

构造函数`(this)`：在类定义中定义一个名为this的方法

伴生对象：一个包含于类同名的对象，伴生类和伴生对象必须在同一个文件内
- 伴生类：一个于对象同名的类，伴生类和伴生对象必须在同一个文件内

匹配模式：一种匹配值的方式

------

# Spark RDD相关知识

RDD：分布式弹性数据集，是一种数据类型。

RDD分布式转换算子、行动算子

转换算子

- `map`：对RDD的每个元素应用函数、返回一个新的RDD
- `filter`：返回一个新的RDD（新的RDD是原RDD的子集），包含应用函数后返回值为true的原始元素，不会触发shuffle排序
- `flagMap`：每个输入元素可以映射到0或多个输入元素
- `mapPartitions`
- `mapPartitionsWithIndex`
- `sample`
- `union`
- `intersection`
- `distinct`
- `groupByKey`
- `reduceByKey`
- `aggregateByKey`
- `sortByKey`
- `sortBy`
- `join`
- `cogroup`
- `cartesian`
- `pipe`
- `coalesce`减少 RDD 的分区数到指定值
- `repartition`RDD元素中根据某些条件进行重新分区

行动算子

- `reduce`：聚合RDD中的所有元素，先聚合分区内数据，在聚合分区间数据
- `collect`：将RDD转换成数组
- `count`：将返回RDD中数据的个数
- `first`：将返回RDD中的第一个元素
- `take`：将返回RDD中的n个元素
- `fold`：根据RDD中的元素，进行累加计算
- `countByKey`：统计每种Key的个数
- `saveAsTextFile`：将RDD保存到文件系统中
- `foreach`：对RDD中元素进行遍历
- `max`
- `min`
- `sum`

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

读取JSON文件：`Spark.read.json()`  或者 `spark.read.format("json")`

将DataFrame保存数据库：`DataFrame.write.format("mysql")`

将DataFrame保存到数据库中用`DataFrame.write()`

将RDD写入写入到HDFS：`rdd.saveAsTextFile("hdfs://path/to/output")`

从HDFS中读取一个文件并创建RDD：`val rdd = sc.textFile("hdfs://path/to/file")`

执行原生SQL语句：spark.sql("原生语句")

临时试图

- 创建或替换临时试图：createOrReplaceTempView
- 创建全局临时试图：createGlobalTemView
- 创建临时试图：createTempView





用户自定义函数：UAF，UDAF

DataFrame和Dataset相关函数

- count() ：计算行的总数
- sum() ：求某一列的总和
- max()：求某一列的最大值
- select()：对指定列数据进行查询
- filter()：对指定列数据进行**过滤**
- groupBy()：对指定规则进行分组
- orderBy()：对指定列进行排序
- join()：对两个DataFrame(Dataset)进行连接
- distinct()：对指定列的数据进行**去重**

# Spark Streaming

是实时数据的流式计算，在实时数据处理和交互式查询上支持实时数据处理，

spark Streaming 数据处理的基本单元是：**DStream**

DStream是流式处理的**输入数据流**

checpoint 的目的是计算累积的结果，**避免数据丢失**，与之使用的函数，updataStateByKey，reduceByKeyAndWindow

transform只有转换的作用

`foreachRDD`将实时数据流转换为 DataFrame 或 DataSet，转换和输出的作用

Spark Streaming的程序必须要有输出语句：print foreachRDD saveAsTextFiles

使用窗口操作来计算近30分钟的数据，窗口长度：30分钟，滑动间隔：30分钟

```scala
//代码题：RDD转换Dataset
case class People(val name:String,val age:Int)
def main(args: Array[String]): Unit = {
  val spark:SparkSession=SparkSession.builder().master("local[*]").appName("SparkSQL").getOrCreate()
  val sc: SparkContext = spark.sparkContext
  val rdd:RDD[(String,Int)]=sc.makeRDD(List(("张三",16),("李四",15)))
  import spark.implicits._ //导入隐式转换
  val ds:Dataset[People] = rdd.map{
    case (name,age)=>People(name,age)
  }.toDS()
  ds.show()
}
//RDD转DataFrame
case class People(name: String, age: Int)
def main(args: Array[String]): Unit = {
  val spark:SparkSession=SparkSession.builder().master("local[*]").appName("SparkSQL").getOrCreate()
  val sc: SparkContext = spark.sparkContext
  val rdd: RDD[(String, Int)] = sc.makeRDD(List(("张三", 16), ("李四", 15)))
  import spark.implicits._ //导入隐式转换
  val df: DataFrame = rdd.map {
    case (name, age) => People(name, age)
  }.toDF()
  df.show()
}
//Dataset转DataFrame
case class People(name: String, age: Int)
def main(args: Array[String]): Unit = {
  val spark:SparkSession=SparkSession.builder().master("local[*]").appName("SparkSQL").getOrCreate()
  import spark.implicits._ //导入隐式转换
  val ds: Dataset[People]=spark.createDataset(Seq(People("Alice", 30),People("Bob", 25),People("Charlie", 35)))
  val df: DataFrame = ds.toDF()
  df.show()
}
//DataFrame转Dataset
case class People(name: String, age: Int)
def main(args: Array[String]): Unit = {
  val spark:SparkSession=SparkSession.builder().master("local[*]").appName("SparkSQL").getOrCreate()
	import spark.implicits._ //导入隐式转换
  val df:DataFrame=spark.createDataFrame(Seq(("Alice", 30),("Bob", 25),("Charlie",35))).toDF("name","age")
  val ds: Dataset[People] = df.as[People]
  ds.show()
}
//代码题：SparkRDD读取文件以逗号拆分单词，将结果转换成字符串进行输出。
def main(args: Array[String]): Unit = {
    val conf = new SparkConf().setAppName("WordCount").setMaster("local[*]")
    val sc = new SparkContext(conf)
    val lines = sc.textFile("input.txt")
    val words = lines.flatMap(line => line.split(","))
    val result = words.collect().mkString(", ")
    println(result)
    sc.stop()
  }
//SparkRDD 给出一段单词，以空格拆分单词，将结果转换成字符串进行输出。
def main(args: Array[String]): Unit = {
  val sparkconf = new SparkConf().setAppName("RDDToString").setMaster("local[*]")
  val sc = new SparkContext(sparkconf)
  val rdd: RDD[String] = sc.makeRDD(List("Hello Spark", "Hadoop Hbase", "Scala Python"))
  //val result: String = rdd.reduce((str1, str2) => str1 + ", " + str2)
  val res:RDD[String]=rdd.flatMap(s=>{
    s.split(" ")
  })
  println(result)
  sc.stop()
}
//用Spark读取一个文本文件并创建一个RDD
def main(args: Array[String]): Unit = {
  val conf = new SparkConf().setAppName("ReadTextFile").setMaster("local[*]")
  val sc = new SparkContext(conf)
  val file = "input/file.txt"
  val rdd: RDD[String] = sc.textFile(file)
  rdd.take(5).foreach(println)
  sc.stop()
}
//将一个RDD中的元素进行分组，并返回每个分组中的最大值  二选一，建议第二句
val rdd2 = rdd.groupBy(x=>x)mapValues(_.max)
val rdd2 = rdd.flatMap(_.spilt(" ")).groupBy(x=>x).mapValues(_.max)

val data = sc.makeRDD(Seq((1,2),(3,4),(5,6),(7,8)))
val res = data.reduce((x,y)=>(X._1+y._1,x._2+y._2))
res = (16,20)//1+3+5+7 = 16  2+4+6+8 =2

//处理数据进行扁平化
def main(args:Array[String]):Unit={
  val sparkConf = new Sparkconf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(sparkConf)
  val rdd:RDD[List[Int]] = sc.makeRDD(List(List(1,2),List(2,3)))
  val res:RDD[Int] = rdd.flatMap(
    list=>{list}
  )
  res.collect().foreach(println)
  sc.stop()
}
//计算所有分区最大值求和（分区内取最大值，分区间最大值求和）
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd:RDD[Int]=sc.makeRDD(List(1,2,3,4),2)
  val res1:RDD[Array[Int]]=rdd.glom()
  val maxres:RDD[Int]=res1.map(array=>{array.max})
  sc.stop()
}
//将一串单词进行首字母分组
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd:RDD[String]=sc.makeRDD(List("hello","spark","scalc"m"hadoop"),2)
  val res:RDD[String]=rdd.groupBy(_.charAt(0))
  res.collect().foreach(println)
	sc.stop()
}
//将rdd1和rdd2进行连接
def main(args:Array[String]):Unit+{
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd1 = sc.makrRDD(List((1,"A"),(2,"B")))
  val rdd2 = sc.makeRDD(List((1,"C" ),(3,"D")))
  val res = rdd1.join(rdd2)
  Res = (1,("A","C"))
}

//外部存储创建RDD
def fileCreateRDD(sprakContext: SparkContext): Unit = {
  val conf = new SparkConf().setMaster("local[*]").setAppName("Spark")  //准备环境
  val sc = new SparkContext(conf)  //让SparkContext去加载配置
  val rdd4:RDD[String] = sprakContext.textFile("input/1.txt")
  rdd4.collect().foreach(println)
}

//将一个RDD中的元素进行分组，并返回每个分组中的最大值
def main(args: Array[String]): Unit = {
  val conf = new SparkConf().setMaster("local[*]").setAppName("Spark")  //准备环境
  val sc = new SparkContext(conf)  //让SparkContext去加载配置
  val rdd:RDD[Int] = sc.makeRDD(Array(10, 20, 30, 40, 50))
  val rdd1 = rdd.groupBy(x=>y).mapValues(_.max)
  val rdd2 = rdd.flatMap(_.split(" ")).groupBy(x=>y).mapValues(_.max)
  sc.stop()
}

//统计包含"A”字符的单词
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd = sc.makeRDD(List("Hadoop","Scala","Python"))
  val res = rdd.filter(_.contains("a")).count
  res.collect.foreach(println)
}
//将两个进行join连接
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd1 = sc.makeRDD(List((1,"A"),(2,"B")))
  val rdd2 = sc.makeRDD(List((1,"C"),(3,"D")))
  val res = rdd1.join(rdd2)
  //res = (1,("A","C"))
  println(res)
  sc.stop()
}
//求分组内的和
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val data = sc.makeRDD(List((1,2),(3,4),(5,6),(7,8)))
	val res = data.reduce((x, y) => (x._1 + y._1, x._2 + y._2))
  //res = (16,20) 1+3+5+7=16,2+4+6+8=20
  println(res)
  sc.stop()
}
//将两个join
def main(args:Array[String]):Unit={
  val conf = new SparkConf().setMaster("local[*]").setAppName("spark")
  val sc = new SparkContext(conf)
  val rdd1 =sc.makeRDD(Seq((1,2),(3,4),(3,6)))
  val rdd2 = sc.makeRDD(Seq((3,9)))
  val res = rdd1.join(rdd2)
  print(res.collect().mkString(","))
  sc.stop()
}
```

