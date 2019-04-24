# 1、JavaSet总结

# 2、JavaSet
 HashSet依赖于HashMap，它实际上是通过HashMap实现的。HashSet中的元素是无序的。
 TreeSet依赖于TreeMap，它实际上是通过TreeMap实现的。TreeSet中的元素是有序的。
## HashSet的工作原理
HashSet 是一个没有重复元素的集合。
它是由HashMap实现的，不保证元素的顺序，而且HashSet允许使用 null 元素。
HashSet是非同步的。
```java
public class HashSet<E>
    extends AbstractSet<E>
    implements Set<E>, Cloneable, java.io.Serializable
{
    static final long serialVersionUID = -5024744406713321676L;

    private transient HashMap<E,Object> map;

    // Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();
    }
```
### 1、基本特性
继承AbstractSet类，实现Set, Cloneable, java.io.Serializable接口
### 2、数据结构
基于HshMap的，key是目标值，value是PRESENT
### 3、核心方法
?
>遍历方法
```java
        //(1) Iterator遍历
        for (Iterator keyIter = hashSet.iterator(); keyIter.hasNext(); ) {
            keyIter.next();
        }
        //(2)toArray,不推荐！此方法需要先将Set转换为数组
        String[] arr = (String[]) hashSet.toArray(new String[0]);
        for (String str : arr) {
            System.out.printf("for each : %s\n", str);
        }
```

## TreeSet的工作原理
TreeSet是有序的并且没有重复元素的集合
```java
public class TreeSet<E> extends AbstractSet<E>
    implements NavigableSet<E>, Cloneable, java.io.Serializable
{
    /**
     * The backing map.
     */
    private transient NavigableMap<E,Object> m;

    // Dummy value to associate with an Object in the backing Map
    private static final Object PRESENT = new Object();
    }
```
### 1、基本特性
继承AbstractSet ，实现 NavigableSet<E>, Cloneable, java.io.Serializable接口

### 2、数据结构
TreeSet中含有一个"NavigableMap类型的成员变量"m，而m实际上是"TreeMap的实例"。
### 3、核心方法
>遍历方法
```java
        //(1) Iterator遍历
        for (Iterator keyIter = treeSet.iterator(); keyIter.hasNext(); ) {
            keyIter.next();
        }
        //(2) Iterator遍历
        for (Iterator keyIter = treeSet.descendingIterator(); keyIter.hasNext(); ) {
            keyIter.next();
        }
        //(2)toArray,不推荐！此方法需要先将Set转换为数组
        String[] arr1 = (String[]) treeSet.toArray(new String[0]);
        for (String str : arr1) {
            System.out.printf("for each : %s\n", str);
        }
```