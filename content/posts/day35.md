---
title: "Day35"
date: 2021-05-11T23:25:23+08:00
lastmod: 2021-05-11
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

day35_linkedHashMap

### LinkedHashMap的特点

1.  LinkedHashMap 是 HashMap 一个子类
    
2.  LinkedHashMap 基本上完全复用了 HashMap 的底层结构， 参数，方法
    
3.  LinkedHashMap的特点基本遵从于 HashMap
    
4.  LinkedHashMap 底层在 HashMap 的基础上(数组 + 链表 + 红黑树) 额外维护了一个双向链表: 这个双向链表用来记录存储
    

### LinkedHashMap 如何额外维护一个双向链表?

![](https://img.fengqigang.cn//img/20210511103031.png)

![](https://img.fengqigang.cn//img/20210511105633.png)

### 构造方法?

1.  默认的构造方法

![](https://img.fengqigang.cn//img/20210511113350.png)

2.  accessOrder(如果我们给accessOrder 设置为真，那么我们如果访问了这个LinkedHashMap中的某一个Key-value数据，那么这份Key-value数据就会在双向链表中的位置移到最后， 它在红黑树上的位置不变)
    ![](https://img.fengqigang.cn//img/20210511113612.png)

### API

![](https://img.fengqigang.cn//img/20210511113931.png)

### TreeMap 有什么特点?

1.  TreeMap 是 Map 一个子实现
2.  描述数据结构是树/二叉搜索树/红黑树
3.  底层是链表
4.  TreeMap 大小有序(中序遍历是有序的)
5.  不允许重复的 key
6.  不允许null键
7.  线程不安全
8.  Treemap 的重复的定义: 大小比较结果是0, 自然顺序/比较器
9.  如果我们希望在TreeMap中存储数据 ，key-value, 我们可以有两个选择：

- 让key本身可以比较(继承Comparabe接口实现 compareTo 方法)（但会让代码看一起来不清爽）
- 不想让 key 本身实现 Comparable 接口实现, 手动用比较器实现

```java
public class DemoTreeMap {
    public static void main(String[] args) {

        TreeMap<User3, Integer> map = new TreeMap<>();

        map.put(new User3("zs", 18), 1);
        map.put(new User3("ls", 18), 1);
    }
}

class User3 {
    private String name;
    private int age;

    public User3(String name, int age) {
        this.name = name;
        this.age = age;
    }
}
```

![](https://img.fengqigang.cn//img/20210511154153.png)

因为TreeMap的底层是一个红黑树, 其结点需要实现比较

**比较器实现（new Comparator）**

```java
public class DemoTreeMap {
    public static void main(String[] args) {

        TreeMap<User3, Integer> map = new TreeMap<>(new Comparator<User3>() {
            @Override
            public int compare(User3 o1, User3 o2) {
                int com = o1.getName().compareTo(o2.getName());
                com = com == 0 ? o1.getAge() - o2.getAge() : com;
                return com;
            }
        });

        map.put(new User3("zs", 18), 1);
        map.put(new User3("ls", 18), 1);
        System.out.println(map);
    }
}

class User3 {
    private String name;
    private int age;

    public User3(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

![](https://img.fengqigang.cn//img/20210511165940.png)

TreeMap(Map &lt;? extends K, ? extends V&gt; m)

TreeMap(SortedMap&lt;k, ? extends V&gt;m)

### API

1.  Map.Entry&lt;K,V&gt; ceilingEntry(K key)
    返回一个大于等于指定key的一份key-value数据

![](https://img.fengqigang.cn//img/20210511150605.png)

2.  K ceilingKey(K key)
    返回大于等于key的指定key的key
    ![](https://img.fengqigang.cn//img/20210511150711.png)
    
3.  Comparator&lt;? super K&gt; comparator() 获得这个treeMap()的比较器
    

![](https://img.fengqigang.cn//img/20210511150802.png)

**复用比较器**

![](https://img.fengqigang.cn//img/20210511150855.png)

4.  containsKey and containsValue

![](https://img.fengqigang.cn//img/20210511151000.png)

5.  descendingKeySet() 键的逆序

![](https://img.fengqigang.cn//img/20210511151044.png)

6.  descendingMap() 返回逆序视图

![](https://img.fengqigang.cn//img/20210511151123.png)

7.  entrySet （获得所有key-value数据）

![](https://img.fengqigang.cn//img/20210511151248.png)

8.  firstEntry(): 返回最小的键值对, (大小根据自然顺序或比较器自己定义的)

![](https://img.fengqigang.cn//img/20210511151340.png)

9.  firstKey()

![](https://img.fengqigang.cn//img/20210511151512.png)

10. floorEntry(K key): 返回一个小于等于给定key的一个键值对

![](https://img.fengqigang.cn//img/20210511151637.png)

11. K floorKey(K key) 返回小于等于给定键的最大值

![](https://img.fengqigang.cn//img/20210511151714.png)

12. get

![](https://img.fengqigang.cn//img/20210511151726.png)

13. headMap(k tokey): 不包含等于

![](https://img.fengqigang.cn//img/20210511151755.png)

![](https://img.fengqigang.cn//img/20210511151802.png)

14. headMap(K tokey) 包含等于

![](https://img.fengqigang.cn//img/20210511151909.png)

15. higerEntry

![](https://img.fengqigang.cn//img/20210511151947.png)

16. higherkey

![](https://img.fengqigang.cn//img/20210511152011.png)

17. Set <k>keySet() 返回键集</k>

![](https://img.fengqigang.cn//img/20210511152056.png)

18. collection <v>values()</v>

![](https://img.fengqigang.cn//img/20210511152123.png)

19. lastEntry()

![](https://img.fengqigang.cn//img/20210511152139.png)

20.lastKey()

21. lowerEntry(K key)

![](https://img.fengqigang.cn//img/20210511152222.png)

22. nabigableKeySet()

返回键集

![](https://img.fengqigang.cn//img/20210511152308.png)

23.pollFirstEntry

![](https://img.fengqigang.cn//img/20210511152432.png)

24.subMap(左闭右开), 可传布尔值

![](https://img.fengqigang.cn//img/20210511152546.png)

25. tailMap

![](https://img.fengqigang.cn//img/20210511152704.png)

### Hashtable 与 HashMap 有什么区别?

1.  产生
    Hashtable 是1.0产生的
    HashMap 是1.2产生的
    
2.  线程安全问题:
    

HashMap 线程不安全
HashTable 线程安全

3.  底层结构

HashMap 底层是数组 + 链表 + 红黑树(jdk1.8)
Hashtable 底层是数组+ 链表 -> 和jdk1.8之前的 hashmap 是一样的

4.  数组默认初始容量以及扩容机制

HashMap： 默认初始是16， 扩容机制是2倍
HashTable: 默认初始是11， 扩容机制(2倍+1)

5.  Hash值, 散列

HashMap: (h=key.hashCode) ^ (h >>> 16)

hash & (length - 1)

HashTable:

int hash = key.hashCode();
int index = (hash & 0x7FFFFFFF) % tab.length;

6.  能不能存储 null

HashMap: 可以存储 null 以及 null 值

Hashtable: 不可以存储 null 键 也不可以存储 null 值

### HashMap 与 ConcurrentHashMap 区别?

### Propertories ?

Propertories 是 Hashtable 的一个子类，

持久化:

代码在运行的过程中(内存), 有可能产生一些数据 ，这个数据有时候我们希望立马存在本地磁盘文件上.

![](https://img.fengqigang.cn//img/20210511162204.png)

![](https://img.fengqigang.cn//img/20210511162416.png)

**如果在使用 Properities 时候， 不要使用从 Hashtable 那继承来的方法，为啥? 因为持久化的时候要求数据 key-value都必须字符串**

### 两种文件格式?

- xml

![](https://img.fengqigang.cn//img/20210511163950.png)

- Properties

![](https://img.fengqigang.cn//img/20210511164039.png)

json 数据是当下时代不同端数据交互的一个普遍格式 90%

上一个时代(5年之前), 数据交互格式 xml 格式还是比较多

现在 xml 格式经常用于配置文件

### 类的分类?

1.  工具类: utils 类
    
2.  Bean 类: 与现实的东西相对应
    

### 什么是解耦?

把一些强相关性的东西拆开，变成弱相关的东西.


