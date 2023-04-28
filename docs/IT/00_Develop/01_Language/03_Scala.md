# Scala

# 变量定义

```scala
val msg = "hello world" //不可变

var a: Long = 1L //可变，类型可以显式声明可以自动推断
```

# 函数

```scala
def max(x: Int, y: Int): Int = {
	if (x > y) x //函数运行的最后一行为返回值
	else y
}


def deleteIndicesIfExist(baseFile: File, suffix: String = ""): Unit = {
	//函数参数suffix设置了默认值，调用时可以不传这个参数
	//Unit表示没返回（void）
	...
}
```

# 元组

元组是承载数据的容易，一旦被创建就不可再修改。每个元素可以是不同的类型。

```scala
val a = (1, 2.3, "hello", List(1, 2, 3))

a._1 //访问第一个元素
```

# 循环

元组是承载数据的容易，一旦被创建就不可再修改。每个元素可以是不同的类型。

```scala
val list = List(1, 2, 3, 4, 5);

for (e <- list) println(e) //命令式

list.foreach(e => println(e)) //函数式

list.foreach(println)
```

# case类

与普通类是类似的，更适合用来表示不可变的数据。会为所有字段定义Getter方法。

```scala
case class Point(x: Int, y: Int) //默认写法，不可修改xy

case class Point(var x: Int, var y: Int) //可以修改xy
```

# 模式匹配

Java中switch只能匹配数值或字符串，Scala中match可以匹配任意类型。

```scala
def describe(x: Any) = x match {
	//Any类型相当于Java里的Object
	case 1 => "One"
	case false => "False"
	case "hi" => "hi"
	case Nil => "..."
	case e: IOException => "..." //冒号后为进入分支的具体条件
	case s: String if s.length > 10 => "..."
	case _ => "..." //default
}
```

# Option对象

与Java中Optional类似，表示一个容器里面可能装了值也可能没有装任何值。

```scala
val keywords = Map("scala" -> "option", "java" -> "optional")

keywords.get("java") //获取key为java的值，存在，返回Some(optional)
//Option[String] = Some(optional)

keywords.get("C") //不存在，返回None
//Option[String] = None

//但是外面包的都是Option


//Option经常与模式匹配一同使用，区分有值和没值的情况（直接拿到里面的东西了）
def display(game: Option[String]) = game match {
	case Some(s) => s
	case None => "unknown"
}

display(Some("abc")) //abc
display(None) //unknoen
```




