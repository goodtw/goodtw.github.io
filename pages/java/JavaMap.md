# 1、JavaMap总结
#### HashMap和Hashtable有什么区别？
相同点：
HashMap 与HashTable都实现了Map， Cloneable, Serializable 接口，都是键值对的数据结构，且都是采用拉链法实现的
且都在JU包下，利用modCount 实现fail_fast机制，?
不同点：
(1) 继承类 ：HashMap  继承的是AbstractMap类，利用迭代器遍历 ;HashTable 继承的是Dictionary类，支持枚举遍历
(2) 线程安全： HashTable继承是所有的方法都是同步的，是线程安全的 ；HashMap是线程不安全的
(3)对null值的处理不同: HashMap 在key为null时，会在table[0]存储其键值对 ; HashTable 在key为null时，会抛NullPointerException异常
(4)遍历方式：HashMap 只支持Iterator遍历; HashTable 支持 Iterator遍历和Enumeration遍历
(5)通过Iterator迭代器遍历时，遍历的顺序不同: HashMap 从前到后 ;HashTable从后到前
(6)容量的初始值 和 增加方式都不一样: HashMap默认的容量大小是16；增加容量时，每次将容量变为“原始容量x2”; Hashtable默认的容量大小是11；增加容量时，每次将容量变为“原始容量x2 + 1”。
(7)添加key-value时的hash值算法不同：HashMap添加元素时，是使用自定义的哈希算法 ;  Hashtable没有自定义哈希算法，而直接采用的key的hashCode()。
```java
static int hash(int h) {
    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```
尽管如此，依然不建议使用HashTable，因为 1）是遗留类，内部很多没有优化 2）在多线程情况下，推荐使用ConcurrentHashMap

#### HashMap和WeakHashMap有什么区别？

#### 如何决定选用HashMap还是TreeMap？
对于元素的插入、删除和定位使用HashMap更好，要是对于有序数组的遍历，TreeMap更好

# 2、JavaMap
## HashMap的工作原理
HashMap 是一个“链表散列” ，首先是一个数组，数组的每一个值都是一个链表；
在put操作时，先会根据key调用hashCode()方法 ，获取hash值作为bucket位置来存储Entry对象，去找链表中正确的节点
当两个对象hash值相同时，即bucket位置相同，会发生‘碰撞’，要想取到准确的值，需要调用eauqls方法
map.get(null)==0? 看源码
```java
public class HashMap<K,V> extends AbstractMap<K,V>
    implements Map<K,V>, Cloneable, Serializable {
       transient Node<K,V>[] table;
       //根据entrySet()获取HashMap的“键值对”的Set集合
        transient Set<Map.Entry<K,V>> entrySet;

        transient int size;

        transient int modCount;
    
        int threshold;

        final float loadFactor;

   static class Node<K,V> implements Map.Entry<K,V> {
        final int hash;
        final K key;
        V value;
        Node<K,V> next;
        }
}
```
### 1、基本特性
实现 Map<K,V>, Cloneable, Serializable接口,实现map
### 2、数据结构
 HashMap是通过"拉链法"实现的哈希表。
它包括几个重要的成员变量：table, size, threshold, loadFactor, modCount。
　　table是一个Entry[]数组类型，而Entry实际上就是一个单向链表。哈希表的"key-value键值对"都是存储在Entry数组中的。 
　　size是HashMap的大小，它是HashMap保存的键值对的数量。 
　　threshold是HashMap的阈值，用于判断是否需要调整HashMap的容量。threshold的值="容量*加载因子"，当HashMap中存储数据的数量达到threshold时，就需要将HashMap的容量加倍。
　　loadFactor就是加载因子。 
　　modCount是用来实现fail-fast机制的。

### 3、核心方法
>遍历方法
```java
//(1)遍历键值对
  for(Iterator iter =  map.entrySet().iterator(); iter.hasNext();){
            iter.next();
        }
//(2)编辑key集合
  for (Iterator keyIter=map.keySet().iterator();keyIter.hasNext();){
            keyIter.next();
        }
//遍历值集合
 for (Iterator valueIter=map.values().iterator();valueIter.hasNext();){
            valueIter.next();
        }  
```

## Hashtable的工作原理

```java
public class Hashtable<K,V>
    extends Dictionary<K,V>
    implements Map<K,V>, Cloneable, java.io.Serializable {

    private transient Entry<?,?>[] table;
    
    private transient int count;

    private int threshold;

    private float loadFactor;

    private transient int modCount = 0;

}
```
### 1、基本特性
和HashMap一样，Hashtable 也是一个散列表，它存储的内容是键值对(key-value)映射。
Hashtable 继承于Dictionary，实现了Map、Cloneable、java.io.Serializable接口。
Hashtable 的函数都是同步的，这意味着它是线程安全的。它的key、value都不可以为null。此外，Hashtable中的映射不是有序的。
Hashtable 的实例有两个参数影响其性能：初始容量 和 加载因子。容量 是哈希表中桶 的数量，初始容量 就是哈希表创建时的容量。注意，哈希表的状态为 open：在发生“哈希冲突”的情况下，单个桶会存储多个条目，这些条目必须按顺序搜索。加载因子 是对哈希表在其容量自动增加之前可以达到多满的一个尺度。初始容量和加载因子这两个参数只是对该实现的提示。关于何时以及是否调用 rehash 方法的具体细节则依赖于该实现。
通常，默认加载因子是 0.75, 这是在时间和空间成本上寻求一种折衷。加载因子过高虽然减少了空间开销，但同时也增加了查找某个条目的时间（在大多数 Hashtable 操作中，包括 get 和 put 操作，都反映了这一点）。

### 2、数据结构

### 3、核心方法
>遍历方法
```java
 //(1)遍历集合
        for (Iterator iter = hashtable.entrySet().iterator(); iter.hasNext(); ) {
            iter.next();
        }
        //(2)遍历key集合
        for (Iterator keyIter = hashtable.keySet().iterator(); keyIter.hasNext(); ) {
            keyIter.next();
        }
        //(3)遍历value集合
        for (Iterator valueIter = hashtable.values().iterator(); valueIter.hasNext(); ) {
            valueIter.next();
        }
        //(4)通过Enumeration遍历Hashtable的键
        Enumeration enumeration = hashtable.keys();
        while (enumeration.hasMoreElements()) {
            enumeration.nextElement();
        }
        //(5)通过Enumeration遍历Hashtable的值
        Enumeration valueEnum = hashtable.elements();
        while (valueEnum.hasMoreElements()) {
            valueEnum.nextElement();

        }
```


## TreeMap的工作原理
```java
public class TreeMap<K,V>
    extends AbstractMap<K,V>
    implements NavigableMap<K,V>, Cloneable, java.io.Serializable
{
    private final Comparator<? super K> comparator;

    private transient Entry<K,V> root;

    private transient int size = 0;

    private transient int modCount = 0;
}
```
### 1、基本特性
实现 NavigableMap<K,V>, Cloneable, java.io.Serializable 接口
### 2、数据结构
 TreeMap的本质是R-B Tree(红黑树)，它包含几个重要的成员变量： root, size, comparator。
　　root 是红黑数的根节点。它是Entry类型，Entry是红黑数的节点，它包含了红黑数的6个基本组成成分：key(键)、value(值)、left(左孩子)、right(右孩子)、parent(父节点)、color(颜色)。Entry节点根据key进行排序，Entry节点包含的内容为value。 
　　红黑数排序时，根据Entry中的key进行排序；Entry中的key比较大小是根据比较器comparator来进行判断的。
　　size是红黑数中节点的个数。
### 3、核心方法
>遍历方法

## WeakHashMap的工作原理
```java
public class WeakHashMap<K,V>
    extends AbstractMap<K,V>
    implements Map<K,V> {
    private static final int DEFAULT_INITIAL_CAPACITY = 16;

    private static final int MAXIMUM_CAPACITY = 1 << 30;
    
    private static final float DEFAULT_LOAD_FACTOR = 0.75f;

    Entry<K,V>[] table;

    private int size;

    private int threshold;

    private final float loadFactor;

    private final ReferenceQueue<Object> queue = new ReferenceQueue<>();
    
    int modCount;
}
```
### 1、基本特性
实现map接口 ，继承 AbstractMap
和HashMap一样，WeakHashMap 也是一个散列表，它存储的内容也是键值对(key-value)映射，而且键和值都可以是null。
不过WeakHashMap的键是“弱键”。在 WeakHashMap 中，当某个键不再正常使用时，会被从WeakHashMap中被自动移除。更精确地说，对于一个给定的键，其映射的存在并不阻止垃圾回收器对该键的丢弃，这就使该键成为可终止的，被终止，然后被回收。某个键被终止时，它对应的键值对也就从映射中有效地移除了。
这个“弱键”的原理呢？大致上就是，通过WeakReference和ReferenceQueue实现的。 WeakHashMap的key是“弱键”，即是WeakReference类型的；ReferenceQueue是一个队列，它会保存被GC回收的“弱键”。实现步骤是：
(01) 新建WeakHashMap，将“键值对”添加到WeakHashMap中。 实际上，WeakHashMap是通过数组table保存Entry(键值对)；每一个Entry实际上是一个单向链表，即Entry是键值对链表。
(02) 当某“弱键”不再被其它对象引用，并被GC回收时。在GC回收该“弱键”时，这个“弱键”也同时会被添加到ReferenceQueue(queue)队列中。
(03) 当下一次我们需要操作WeakHashMap时，会先同步table和queue。table中保存了全部的键值对，而queue中保存被GC回收的键值对；同步它们，就是删除table中被GC回收的键值对。
这就是“弱键”如何被自动从WeakHashMap中删除的步骤了。

和HashMap一样，WeakHashMap是不同步的。可以使用 Collections.synchronizedMap 方法来构造同步的 WeakHashMap。
### 2、数据结构
(01) WeakHashMap继承于AbstractMap，并且实现了Map接口。
(02) WeakHashMap是哈希表，但是它的键是"弱键"。WeakHashMap中保护几个重要的成员变量：table, size, threshold, loadFactor, modCount, queue。
　　table是一个Entry[]数组类型，而Entry实际上就是一个单向链表。哈希表的"key-value键值对"都是存储在Entry数组中的。 
　　size是Hashtable的大小，它是Hashtable保存的键值对的数量。 
　　threshold是Hashtable的阈值，用于判断是否需要调整Hashtable的容量。threshold的值="容量*加载因子"。
　　loadFactor就是加载因子。 
　　modCount是用来实现fail-fast机制的
　　queue保存的是“已被GC清除”的“弱引用的键”。
### 3、核心方法
>遍历方法



