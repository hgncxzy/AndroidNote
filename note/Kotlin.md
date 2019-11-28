## The basics

### 语句结构

一行一个语句（先不纠结语句与表达式的区别），不用加分号，不用打分号，光这个就可以节省多少时间呢？是不是感觉人生都浪费在了分号上面。如果想在一行写多个语句，前面的要加上分号。

缩进规则与Java一致，用四个空格，也可以用tab，或者不加缩进，只要没人打你。

语句块需要加上花括号{}。总之，语句结构与Java很类似。

### 变量

用var来声明变量，用val来声明常量，因为Kotlin是静态强类型语言（也就是说每个变量在编译的时候必须知道类型）声明时需要带上类型，方法是在变量名的后面加冒号，空格跟上类型名字，与Pascal差不多。如果声明时直接定义，则可以不用指定类型，编译器会根据定义表达式来推测它的类型。示例：

```kotlin
var str: String
val i: Int
var str = "Hello, world"
```

### 语句和表达式

主要想说一下语句和表达式的区别，简单来说就是表达式是有值的，可以放在变量赋值的右边，而语句是没有值的，不能放在赋值的右边

### 基本运算

不多说了，跟Java一样

### 注释

这个跟Java也一样：
 // 单行注释
 /* */  多行注释 /** */ documentation

### 函数

以fun关键字来定义一个函数格式为：*fun 函数名(参数): 返回类型 {函数体}*，如:

```kotlin
fun foo(name: String): Int {
   return name.length()
}
```

命名参数和默认值，调用函数时可以把参数的名字带上，以增加可读性。声明函数时可以用默认值 ，以更好的支持函数的重载。如：

```kotlin
fun foo(name: String, number: Int = 42, toUpper: Boolean = false): String {}
```

使用时，可以指定参数的名字：

```kotlin
foo("a)
foo("b", number = 1)
foo("c", toUpper = true)
foo(name = "d", number = 2, toUpper = false)
```

表达式体如果一个函数体内只有一个表达式，且有返回值时，那么，可以直接把返回值放在函数 的后面，如：

```kotlin
fun foo(name: String): String = name.toUpperCase()
```

甚至还可以把返回类型的声明给省略掉，如：

```kotlin
fun foo(name: String) = name.toUpperCase()
```

跟Java不一样的是，Kotlin的函数可以声明为toplevel也就是跟class一个级别，也就是说不必非放在类里面，也就是说跟C和C++是类似的。此外，还可以函数赋值给一个变量，这个变量就像其他变量一样。

### 类与对象

#### 类的声明与对象创建

用class来声明一个类型，用:来继承父类或者实现接口，不需要使用new来创建对象：

```kotlin
class Person {
   var name: String
   var age: Int
}
```

假如，一个类，是空的，没有内容，那么花括号{}是可以省略的：

```kotlin
class Person
```

创建对象：

```kotlin
var someone = Person()
```

#### Primary constructor

构造方法，有所谓的primary constructor，可以直接写在类名的后面：

```kotlin
class Person constructor(name: String)
```

一般情况下，constructor 可以省略掉：

```kotlin
class Person(name: String)
```

初始化块因为primary constructor不能包含代码，所以，想要做些初始化工作就可以放在初始化块里面(initializer block)，也可以在定义属性时直接使用：

```kotlin
class Person(name: String) {
    var firstName: String = name
    init {
        println("First initializer block that prints ${name}")
    }
}
```

一般情况下，如果声明的属性变量在primary constructor中都有赋值（通过initializer block）的话，可以有更简洁的表达方式：

```kotlin
class Person(var name: String, var age: Int)
```

这相当于：

```kotlin
class Person(theName: String, theAge: Int) {
   var name: String = theName   var age: Int = theAge
}
```

如果primary construct前面要声明属性，或者有annotation的话，关键字constructor不能省略：

```kotlin
class Person public @Inect constructor(var name: String)
```



#### Secondary constructor

如果primary constructor不能满足需求怎么办呢？还可以声明其他constructor，所谓的secondary constructor:

```kotlin
class Person {
   var name: String constructor(name: String）{
       this.name = name
   }
}
```

是不是看起来舒服一些，因为跟Java一样了，可以把primary constfuctor和second constructor联合起来一起用：

```kotlin
class Person(var name: String) {
    constructor(name: String, parrent: Person) : this(name) {
        parrent.addChild(this)
    }
}
```

这里要把 secondary construct 尽可能delegate到 primary constructor，这里的 delegate 的意思就是 primary constructor会在 second constructor 之前 执行，还有就是 initiailzer block 都是在 primary construct 中执行的，这就能保证 initiliazer block 在 second constructor 之前执行。即使没有显示的声明 primary constructor，编译器还是会生成一个默认的 primary constructor 以及把 secondary constructor 默认的 delegate 到 primary constrcutor 上面。也就是说，会保证 primary constructor 以及 initializer block 执行在 second constructor 前面：

```kotlin
class Constructors {
    init {
        println("Initializer block")
    }

    constructor(i: Int) {
        println("second constructor")
    }
}

fun main(args: Array<String>) {
    val c = Constructors(3)
}
```

输出：

```kotlin
Initializer block
second constructor
```

#### 属性和访问方法

Kotlin会为声明的属性生成默认的setter和getter：

```kotlin
class Person(var name: Strring, var age: Int)

val p = Person("Kevin", 24)
p.getName() // 返回"Kevin"
p.setAge(32) // age变成了32
```

如果想自定义setter和getter，也是可以的：

```kotlin
class Person {
    var name: String
        set(n: String) {
            if (n == null || n == "") {
                name = "Unkown"
            } else {
                name = n
            }
        }
        get() {
            if (name == "Unkwon") {
                return "Nobody"
            }
            return name
        }
}
```

#### 定义类的方法

跟声明普通函数一样，只不过是放在了类里面：

```kotlin
class Person(val name: String, val age: Int) {
    fun report() = "My name is $name, and I'm $age"
}
```

如果，要覆写父类的方法，需要使用在方法声明时加上override关键字。

```kotlin
class Doggy(val name: String) : Animal {
    override fun yell() = "Barking from $name"
}
```

#### 访问权限

访问权限也跟Java类似分为public，protected，private以及internal，前三个意义也都一样，只不过默认值不一样，在Java里，如果对成员没有指明，则是package scope，也就是同一个package可以访问，但是Kotlin默认是public的。

internal是module内部可见，有点类似于Java中的package，但是module定义跟package不一样，module是一组编译在一起的Kotlin文件，它跟编译打包有关系，简单的理解它的范围要比package要大。

还有就是类，默认是不可被继承的，相当于final class。如果想要允许继承就要在声明类的时候加上open。

### 字串

概念就不说了，大部分与Java一模一样的，像支持的方法等。唯一需要说的就是字串模板，就是说把其他类型转化为字串时，有较Java更为方便的方式：直接用$来把变量嵌入到字串之中，如：

```kotlin
val msg = "Error 1"
val count = 32
print("We got message $msg") //等同于"We got message " + msg
print("Total is $count") // Total is 32
```

### lambda表达式

首先要介绍一个概念，高阶函数，其实就是把另外函数当作参数的函数，或者说产生一个函数，也即把函数作为返回值 的函数。前面说过，函数是一级对象，可以像常规变量一样来使用，所以，就能把函数作为参数或者返回值来使用高阶函数。lambda表达式就是为高阶函数更方便使用而生的。

#### lambda 表达式

作为新时代的编程语言，都会支持函数式编程，而lambda表达 式又是函数式编程里面必不可少的一份子。其实啥是lambda表达式呢？说的简单点就是没有名字的函数，非常简短的，通常都是一两句话的没有名字的函数。就是长这个样子{A, B -> C}，这里面A，B是参数，C是表达式，如：

```kotlin
val sum = { x: Int, y： Int -> x + y }
```

其中，参数的类型是可以省略的，因为编译器能从上下文中推测出来:
 max(strings, { a, b -> a.length < b.length }
 表达式部分，可以不止一个，最后一个表达式作为返回值。

当把一个lambda表达作为最后一参数，传给某个函数时，可以直接把lambda表达式写在参数的外面，比如：

```kotlin
val product = items.fold(1) { acc, e -> acc * e }
```

而当lambda是唯一的参数时，也可以把参数的括号省略掉：

```kotlin
run { println("Hello, world") }
```

还有就是，如果lambda表达中只有一个参数，那么参数也可以省略，直接写表达式:

```kotlin
eval{ x * x }
```

#### 函数类型

前面提到了函数是可以像普通变量一样使用的一级类，也就是说它是一个类型。它的具体形式是: (A, B)->C，其中括号内的是参数，C是返回类型，如：

```kotlin
val sum: (Int, Int)->Int = { x, y -> x + y }
val square: (Int)->Int = { x -> x * x }
```

为啥要提一下函数类型呢，因为有时需要声明高阶函数：

```kotlin
fun walk(f: (Int)->Int)
fun run(f: ()->Unit)
```

Unit是一个特殊的返回值，相当于void，意思就是此函数没有返回值。

### 集合

其实大部分跟Java是一样的。只不过有一些函数式的操作，要多注意使用，从而让代码更简洁，如：

- 遍历
- 过滤
- 映射
- 排序
- 折叠
- 分组
- 归类

这些操作，对于大家应该都不难理解，就不一一解释了，来段代码就知道了：

```kotlin
fun collectionTests() {
    val list = listOf("Apple", "Google", "Microsoft", "Facebook", "Twitter", "Intel", "QualComm", "Tesla")
    // 遍历，以进行某种操作
    list.forEach{ println(it) }
    //按条件进行过滤，返回条件为true的
    val short = list.filter { it.length < 6 }
    println(short) // [Apple, Intel, Tesla]
    // 把列表元素映射成为另外一种元素
    val lenList = list.map{ it.length }
    println("Length of each item $lenList") //Length of each item [5, 6, 9, 8, 7, 5, 8, 5]
    // 按某种条件进行排序
    val ordered = list.sortedBy { it.length }
    println("Sorted by length $ordered") // Sorted by length [Apple, Intel, Tesla, Google, Twitter, Facebook, QualComm, Microsoft]
    // 折叠，用累积的结果继续遍历
    val joint = list.fold("", {partial, item -> if (partial != "")  "$partial, $item" else item })
    println("Joint list with comma $joint") // Joint list with comma Apple, Google, Microsoft, Facebook, Twitter, Intel, QualComm, Tesla
    //分组，用某种条件 把列表分成两组
    val (first, second) = list.partition { it.length < 6 }
    println("Length shorter than 6 $first") // Length shorter than 6 [Apple, Intel, Tesla]
    println("Longer than 6 $second") // Longer than 6 [Google, Microsoft, Facebook, Twitter, QualComm]
    // 归类，按某种方法把元素归类，之后变成了一个Map
    val bucket = list.groupBy { it.length }
    println("$bucket is a map now") //{5=[Apple, Intel, Tesla], 6=[Google], 9=[Microsoft], 8=[Facebook, QualComm], 7=[Twitter]} is a map now
}
```

### null处理

为了有效的减少空指针异常，Kotlin加入了Nullable类型，核心的原理是这样的：声明类型的时候要明确的告诉编译器，这个变量是否可能为null，如果可能为null，那么可以赋null给这个变量，并且在使用此变量时必须检查是否为null；假如这个变量不可能为null，那么是不可以赋null给此变量的。也就是说，编译器会帮忙做一些检查，以减少NullPointerException的发生。

#### Nullable变量

默认的变量声明都是不可为null的，如:

```kotlin
var safe: String
safe = null // 会有compile error
```

要想允许变量为null，要在类型后面加一个问号，以告诉编译器这是一个nullable类型：

```kotlin
var danger: String?
danger = null // OKay
```

使用时，nullable 不能直接使用，必须检查是否为null:

```kotlin
safe.length // okay
danger.length // compile error, danger could be null
```

#### 检查Nullable的真伪

可以用传统方式：

```kotlin
val len = if (danger != null) danger.length else -1
```

##### Safe call

既然有Nullable类型，自然就有配套的方式来更方便的使用它：

```kotlin
val len = danger?.length
```

如果danger是null就返回null，否则返回长度，注意它的返回值是一个Int?（又是一个Nullable类型)。这个还能链起来：

```kotlin
bob?.department?.head?.name
```

如果任何一环为null，则直接返回null。是不是感觉省了好多if (a == null)判断。

##### Elvis operator

假如不能接受safe call返回的null，咋办呢？想提供默认值的呢？也有方式：

```kotlin
val len = danger?.length
println(len ?: -1)
```

稍有点绕哈，首先，danger?.length返回一个Int?吧，那么?:的作用就是如果len是null，那么就返回-1,否则返回它的值。

整理自 https://www.jianshu.com/p/a63c38ad80a5

## 学习文档

- [kotlin 官方实例](https://play.kotlinlang.org/byExample/overview)

- [A family of small Kotlin libraries for delightful Android development](https://github.com/LouisCAD/Splitties)

- [Kotlin教程](https://www.runoob.com/kotlin/kotlin-tutorial.html)

- [Kotlin系列之let、with、run、apply、also函数的使用](https://blog.csdn.net/u013064109/article/details/78786646)

  

