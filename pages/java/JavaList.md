# 1、JavaList总结
 架构与概念
![Image text](../../../resources/images/java_list_jiagou.jpg)
转载于[https://www.cnblogs.com/skywang12345/p/3308900.html](https://www.cnblogs.com/skywang12345/p/3308900.html)

(01) List 是一个接口，它继承于Collection的接口。它代表着有序的队列。
(02) AbstractList 是一个抽象类，它继承于AbstractCollection。AbstractList实现List接口中除size()、get(int location)之外的函数。
(03) AbstractSequentialList 是一个抽象类，它继承于AbstractList。AbstractSequentialList 实现了“链表中，根据index索引值操作链表的全部函数”。

(04) ArrayList, LinkedList, Vector, Stack是List的4个实现类。
　　ArrayList 是一个数组队列，相当于动态数组。它由数组实现，随机访问效率高，随机插入、随机删除效率低。
　　LinkedList 是一个双向链表。它也可以被当作堆栈、队列或双端队列进行操作。LinkedList随机访问效率低，但随机插入、随机删除效率低。
　　Vector 是矢量队列，和ArrayList一样，它也是一个动态数组，由数组实现。但是ArrayList是非线程安全的，而Vector是线程安全的。
　　Stack 是栈，它继承于Vector。它的特性是：先进后出(FILO, First In Last Out)。
特点与应用场景

## Array和ArrayList有何区别？什么时候更适合用Array？
== 1 ==
(1)Array可以承接基本类型和对象，ArrayList只可以承接对象
(2)Array是指定大小的，ArrayList是不固定大小的，
(3)ArrayList 功能更多，removeAll addAll Iterator
== 2 ==
(1)列表的大小应固定，更多的是进行存储和遍历时
(2)基本类型数据，尽管collection里有自动装箱和开箱操作，但是效率依然会慢
(3)使用多为数组
## ArrayList和Vector有何异同点？
相同点：
(1)两者都是基于索引的，内部都一个数组支持
(2)两者维护插入的顺序，可以根据插入顺序访问元素
(3)两个都在JC包下，都是fail-fast机制
(4)两个都允许null值，都可以根据索引值对元素随机访问
不同点：
1）Vector 是同步的，线程安全的所以效率相对较慢 ；ArrayList是非同步的，基于ArrayList同步的是CopyOnWriteArrayList；
2）Arraylist更加通用
# 2、JavaList
## ArrayList的工作原理
ArrayList是基于数组实现的，是一个动态数组

```java
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    private static final long serialVersionUID = 8683452581122892189L;
    private transient Object[] elementData;
    private int size;
}
```
### 1、基本特性
继承AbstractList ，
实现RandomAccess接口，支持随机访问
实现Cloneable接口，即覆盖了函数clone()，支持克隆
实现java.io.Serializable接口，支持序列化
### 2、数据结构
模型：数组+容量
构造器有三种：支持初始容量0的List，指定容量的List,

### 3、核心方法
>copy方法：
```java
public static native void arraycopy(Object src,  int  srcPos,
                                        Object dest, int destPos,
                                        int length);
```

>扩容方法：
>(01) ArrayList 实际上是通过一个数组去保存数据的。当我们构造ArrayList时；若使用默认构造函数，则ArrayList的默认容量大小是10(JDK1.8时是0，第一次初始化时，容量是10，比10小的时候，依然为10；比10大时，每次扩为上一次的1.5倍；)。
>(02) 当ArrayList容量不足以容纳全部元素时，ArrayList会重新设置容量：新的容量=上一次的1.5倍。直至到最大值内存溢出抛异常
>(03) ArrayList的克隆函数，即是将全部元素克隆到一个数组中。
>(04) ArrayList实现java.io.Serializable的方式。当写入到输出流时，先写入“容量”，再依次写入“每一个元素”；当读出输入流时，先读取“容量”，再依次读取“每一个元素”。
```java
 private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```
>3种遍历方式
```java
//（1）迭代器遍历
for(Iterator iter = list.iterator(); iter.hasNext();)
    iter.next();
//for i
list.get(i)

//for each遍历
for(Object obj:list)
```


## Vector的工作原理
Vector与ArrayList类似，在其基础上新增了一个 capacityIncrement 属性，用来控制动态数组的增长量
```java
public class Vector<E>
    extends AbstractList<E>
    implements List<E>, RandomAccess, Cloneable, java.io.Serializable
{
    protected Object[] elementData;

    protected int elementCount;

    protected int capacityIncrement;
}

```

### 1、基本特性
继承AbstractList ，
实现RandomAccess接口，支持随机访问
实现Cloneable接口，即覆盖了函数clone()，支持克隆
实现java.io.Serializable接口，支持序列化
### 2、数据结构
模型：数组+容量+增长系数
(01) elementData 是"Object[]类型的数组"，它保存了添加到Vector中的元素。elementData是个动态数组，如果初始化Vector时，没指定动态数组的大小，则使用默认大小10。随着Vector中元素的增加，Vector的容量也会动态增长，capacityIncrement是与容量增长相关的增长系数，具体的增长方式，请参考源码分析中的ensureCapacity()函数。
(02) elementCount 是动态数组的实际大小。
(03) capacityIncrement 是动态数组的增长系数。如果在创建Vector时，指定了capacityIncrement的大小；则，每次当Vector中动态数组容量增加时，增加的大小都是capacityIncrement。

构造器有三种：支持初始容量0的List，指定容量的List,

### 3、核心方法
>扩容方法
```java
 private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + ((capacityIncrement > 0) ?
                                         capacityIncrement : oldCapacity);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```
>遍历方式
```java
//(01) 第一种，通过迭代器遍历。即通过Iterator去遍历。
for(Iterator iter = list.iterator(); iter.hasNext();)
    iter.next();

//(02) 第二种，随机访问，通过索引值去遍历。由于Vector实现了RandomAccess接口，它支持通过索引值去随机访问元素。
Integer value = null;
int size = vec.size();
for (int i=0; i<size; i++) {
    value = (Integer)vec.get(i);
}

//(03) 第三种，另一种for循环。如下：
Integer value = null;
for (Integer integ:vec) {
    value = integ;
}

//(04) 第四种，Enumeration遍历。如下：
Integer value = null;
Enumeration enu = vec.elements();
while (enu.hasMoreElements()) {
    value = (Integer)enu.nextElement();
}

```

## LinkedList的工作原理
```java
public class LinkedList<E>
    extends AbstractSequentialList<E>
    implements List<E>, Deque<E>, Cloneable, java.io.Serializable
{
    transient int size = 0;
    transient Node<E> first;
    transient Node<E> last;
    //othrts
    }
```
### 1、基本特性
继承AbstractSequentialList
实现List接口，可以进行队列操作
实现Cloneable接口，覆盖了函数clone()，支持克隆
实现Serializable接口，支持序列化
实现Deque ，可作为双端队列使用
LinkedList 是一个继承于AbstractSequentialList的双向链表。它也可以被当作堆栈、队列或双端队列进行操作。
### 2、数据结构
?
### 3、核心方法
支持FIFO 与LIFO
>遍历方法
```java
//（1）迭代器遍历
for(Iterator iter = list.iterator(); iter.hasNext();)
    iter.next();

//（2）for i
int size = list.size();
for (int i=0; i<size; i++) {
    list.get(i);
}

//（3）for each遍历
for(Object obj:list){
   ;
}

//（4）
while(list.pollFirst() != null)
        ;
    //(05) 通过pollLast()来遍历LinkedList
 while(list.pollLast() != null)
        ;
    //(06) 通过removeFirst()来遍历LinkedList
    try {
        while(list.removeFirst() != null)
            ;
    } catch (NoSuchElementException e) {
    }
    //(07) 通过removeLast()来遍历LinkedList

    try {
        while(list.removeLast() != null)
            ;
    } catch (NoSuchElementException e) {
    }
```

## Stack的工作原理

```java
public
class Stack<E> extends Vector<E> {}
```
### 1、基本特性
继承自vector ,后进先出
### 2、数据结构
继承自vector ,Stack也是通过数组实现的，而非链表。
### 3、核心方法
push pop peek

