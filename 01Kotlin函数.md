## kotlin 函数

### 1.函数定义
关键字fun用来生命一个函数
参数的类型写在变量名称后面
函数的返回值类型也写在方法名后面，这与Java的定义是不同的
函数可以定义在文件的最外层，不需要放在类中
```kotlin
fun funName(para1 : Type, ...) : Type {
  someCode
}
```
下面我们看下main函数的写法
```kotlin
fun main(args: Array<String>) {
  println("HelloWorld")
}
```
### 2.函数返回值

2.1 无返回值  
使用Unit来标识，上述的main方法缺省了Unit，完整的写法如下：
```kotlin
fun main(args: Array<String>) : Unit {
  println("HelloWorld")
}
```
2.2 显示声明返回值类型  
如下定义了一个返回值为Int的函数：
```kotlin
fun sum(a: Int, b: Int): Int {
    return a + b
}
```   
2.3 隐式返回值类型  
请先看下如下代码，是不是感觉有点陌生。
```kotlin
fun sum(a: Int, b: Int) = a + b
```   
表达式函数体：
a + b在kotlin中被称为表达式；上述代码的函数体只有一个表达式，这样就可以去掉花括号和return语句， 这种更简单的编写方式就叫做表达式函数体。

类型推导  
对于上诉的表达式函数体并没有指定返回值类型，但是Kotlin作为静态类型语言，编译器会分析作为函数体的表达式，并把他的类型作为函数的返回类型，这个过程被称作类型推导
### 3.函数参数  
3.1 具名参数  
给函数的实参附上参数名
```kotlin
//函数定义
fun sum(a: Int, b: Int) = a + b
//函数调用
sum(a = 1, b = 2)
```
优点就是当你调用多参数的函数时，可以明确的看出各个参数的意义  

3.2 变长参数
vararg 关键字，用于标识参数长度可变化
```kotlin
//函数定义
fun testVararg(vararg ints: Int) {
    for (v in vars) {            
      println(v)
   }
 }
//函数调用
hello(1,2,3,4,5)
```
* 因为在kotlin里有具名参数，所以可以不为最后一个参数，可以在参数列表里的任意位置（Java里只能是最后一个参数）
* 如果传参数时有歧义，则需要使用具名参数
* Kotlin和Java另一个区别在于，需要传入的参数已经包装在数组中时调用的语法。在Java中可以直接把包装好的数组传入被调用函数中，在Kotlin中需要你显式的解包数组。从技术角度来说这个功能称为展开运算符，在你使用的时候只不过需要在数组前加一个 * 号，如下所示：
```kotlin
//函数定义
fun testVararg(vararg ints: Int) {
    val list = listOf("args: ", * args)  //展开运算符展开数组内容
    println(list)
 }
```
3.3 带默认值参数
* 为函数参数指定默认值
* 可以为任意位置的参数指定默认值
* 传参时，如果有歧义，需要使用具名参数

```kotlin
//函数定义
fun world(double: Double = 3.0, vararg ints: Int, string: String) {
     println(double)
     ints.forEach(::println)
     println(string)
 }
//函数调用
world(ints = *intArrayOf(1, 2, 3, 4, 5), string = "world")
第一个参数指定的默认参数，调用时可以省略不传

fun world(double: Double, vararg ints: Int, string: String = "world")
world(3.0, *array)
```
如果默认参数在最后一个，调用时不传也不会产生歧义
