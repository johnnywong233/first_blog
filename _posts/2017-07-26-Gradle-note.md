### Groovy基础
- 分号可不写；
- 变量定义最好使用关键字def；
- 函数定义时，参数的类型也可以不指定，函数的返回值也可以是无类型的，无类型的函数定义，必须使用def关键字，若指定函数返回类型，则可不必加def关键字来定义函数；
- 组件化、插件化、配置集成等都是基于JavaBean，groovy中getter/setter可不写；
- return可以不写，把方法执行过程中的最后一句代码作为其返回值；
- 括号是可以省略的：
```groovy
task invokeMethod << {
    method1(1,2)
    method1 1,2

}
def method1(int a,int b){
    println a+b
}
```
- 单引号和双引号都可以定义一个字符串常量（Java里单引号定义一个字符），不同的是单引号标记的是纯粹的字符串常量，
而不是对字符串里的表达式做运算，但是双引号可以。一个美元$符号紧跟着一对花括号，花括号里放表达式，比如```${name},${1+1}```等等，只有一个变量时可省略花括号，比如```$name```。
单引号中的内容严格对应Java中的String，不对$符号进行转义，双引号的内容中有$的话，则它会$表达式先求值，三个引号中的字符串支持随意换行。
- 集合List
Groovy中定义List：
```groovy
task printList << { 
    def numList =[1,2,3,4,5,6]
    println numList.getClass().name
    println numList[1]//访问第二个元素
    println numList[-1]//访问最后一个元素
    println numList[-2]//访问倒数第二个元素
    println numList[1..3]//访问第二个到第四个元素
}
```
Groovy为List提供each方法来迭代，该方法接受一个闭包作为参数，可以访问List里的每个元素。
```groovy
task printList << {
    def numList =[1,2,3,4,5,6]
    println numList.getClass().name

    println numList[1]//访问第二个元素
    println numList[-1]//访问最后一个元素
    println numList[-2]//访问倒数第二个元素
    println numList[1..3]//f访问第二个到第四个元素

    numList.each {
        println it
    }
}
```
- 集合Map
定义；访问采用```map[key]```或```map.key```的方式都可以。采用each方法迭代时，被迭代的元素是一个Map.Entry的实例。
key必须是字符串，value可以是任何对象。key可以用''或""包起来，也可以不用引号包起来，默认被处理成字符串
```groovy
task printlnMap << {  
    def map1 =['width':1024,'height':768]
    println map1.getClass().name

    println map1['width']
    println map1.height
    
    map1.each {
            println "Key:${it.key},Value:${it.value}"
        }
}
```
- 集合Range，范围，它其实是List的一种拓展。
```def aRange = 1..5```，Range类型的变量，由begin值+两个点+end值表示
```def aRangeWithoutEnd = 1..<5```,不包含最后一个元素
- 代码块可作为参数传递
代码块，花括号包围的代码，即闭包，Groovy是允许其作为参数传递的；如果方法的最后一个参数是闭包，可以放到方法外面。
```groovy
def aClosure = {
    String param1, int param2 ->  //箭头前面是参数定义，后面是代码  
    println"this is code" //返回值,也可以使用return，和Groovy中普通函数一样  
}
```
Closure的定义格式是:
```groovy
def xxx = {paramters -> code}  //或者  
def yyy = {code}  //这种case不需要->符号
```
闭包定义好后，要调用它的方法就是：闭包对象.call(参数),或者更像函数指针调用的方法：闭包对象(参数)  
比如：
```groovy
aClosure.call("this is string",100)//or
aClosure("this is string", 100)  
```
如果闭包没定义参数的话，则隐含有一个参数it，代表闭包的参数,和this的作用类似。
比如：
```groovy
def greeting = { "Hello, $it!" }
assert greeting('Patrick') == 'Hello, Patrick!'
```
等同于：
```groovy
def greeting = { it -> "Hello, $it!" }
assert greeting('Patrick') == 'Hello, Patrick!'
```
但是，如果在闭包定义时，采用下面这种写法，则表示闭包没有参数！
```groovy
def noParamClosure = { -> true }
```
此时就不能给noParamClosure传参！
```groovy
noParamClosure ("test")  //报错
```
- 

### Gradle
构建，即build/make，根据输入信息然后干一堆事情，最后得到几个产出物（Artifact）。最简单的构建工具就是make。make就是根据Makefile文件中写的规则，执行对应的命令，然后得到目标产物。很难在xml中描述if{某条件成立，编译某文件}/else{编译其他文件}这样有不同条件的任务。

常用命令：
- gradle projects查看工程信息
- gradle tasks查看任务信息
- gradle task-name执行任务，比如gradle clean是执行清理任务，和make clean类似；gradle properties用来查看所有属性信息。

Gradle工作流程

![](https://github.com/johnnywong233/first_blog/raw/gh-pages/_posts/img/gradle_task.png)

三个阶段：
- 首先是初始化阶段，执行settings.gradle等
- Initialization phase的下一个阶段是Configuration阶段。
- Configuration阶段的目标是解析每个project中的build.gradle。在这两个阶段之间，可以通过API来添加一些定制化的Hook。
- Configuration阶段后，整个build的project以及内部的Task关系就确定。Configuration会建立一个有向图来描述Task之间的依赖关系。可以添加HOOK，即当Task关系图建立好后，执行一些操作。
- 最后一个阶段就是执行任务。后面还可以加Hook。

[文档](https://docs.gradle.org/current/dsl/)

Gradle主要有三种对象，和三种不同的脚本文件对应，在gradle执行时，会将脚本转换成对应的对端：
- Gradle对象：执行gradle xxx或者什么的时候，gradle会从默认的配置脚本中构造出一个Gradle对象。在整个执行过程中，只有这么一个对象。Gradle对象的数据类型就是Gradle。一般很少去定制这个默认的配置脚本。
- Project对象：每一个build.gradle会转换成一个Project对象。
- Settings对象：每一个settings.gradle都会转换成一个Settings对象。