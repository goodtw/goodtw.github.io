# 一、Java基础
## 概念
面向对象
## JDK JRE  JVM
JDK：java工具包
JRE：java 运行环境
JVM：java虚拟机
## 四大基本特性
抽象 封装 集成 多态
### 重载与重写的区别
重写是子类重新定义了父类的方法，方法签名与父类是一致的。重载是同一类中多个方法名相同但是参数不同的方法
## 七大设计原则
SOLID原则
迪米特法则
组合优于继承原则
## 接口与抽象类的区别 

## String和StringBuilder、StringBuffer的区别？
String 是final类型的，一旦创建不可以更改
StringBuilder 是java5后有的，所有方法都没有synchronized关键字修饰，所以很高效，但是非线程安全的；
StringBuffer 与StringBuilder相反
## 设计模式
### 单例模式
饿汉单例：
懒汉单例：

### 工厂模式
?
## 策略模式
？
# 二、集合（以JDK1.8为例）
## 集合分类
Collection 是结合顶层的跟接口
List 可重复的有序集合，可以根据索引找值，似一个长度动态变换的数组 
Set 不可重复的集合
Map 键值对，每个key最多只能映射到一个value
一些其它的接口有Queue、Dequeue、SortedSet、SortedMap和ListIterator
Iterator 可以用来遍历list和set，只支持前向；ListIterator只可以遍历List，但是支持前向和后向
### 为何Map接口不继承Collection接口？
Map提供的是键值对映射，Collection是一组数据，数据结构不同，且违反了接口分离原则
类间的依赖关系应该建立在最小的接口上；目的是解耦，从而工艺重构和维护，让客户依赖的接口尽可能小





# JUC-java多线程
## 快速失败(fail-fast)和安全失败(fail-safe)的区别是什么？
快速失败是，当你在迭代一个集合时，另一个线程正在修改你访问的集合，就是抛出一个ConcurrentModification异常。JU包下的都是快速失败的；
安全失败是，当你在迭代集合是时候去底层集合做一个copy，当你在修改上层集合的时候，底层不受影响，不会抛出ConcurrentModification异常。JUC包下的都是安全失败的；




