---
title: "Day34"
date: 2021-05-10T23:36:10+08:00
lastmod: 2021-05-10
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 套壳

![](https://img.fengqigang.cn//img/20210510101446.png)





### Java 集合体系是什么样的?

两个 

Collection 集合体系

Map 集合体系

都是 Object 的子类



### Map 特点

1. Map 接口是Map 集合体系的顶级接口
2. 和 Collection 接口以及 Collection 下面子实现不同的是, Map 所存储的数据不再是单个数据的，而是 Key-value 的数据(键值对)
3. Map 的子实现有些是有序的，有些是无序的
4. Map 的子实现不允许存储重复key(重复元素的定义不同)
5. Map 有些子实现可以存储 null, 有些子实现不允许存储 null (指key值)

### Map 的 Api?

**put**

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);
        map.put("wu", 20);
        map.put("zl", 22);
        System.out.println(map);

    }
}
```



![](https://img.fengqigang.cn//img/20210510135753.png)







**clear**

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);
        map.put("wu", 20);
        map.put("zl", 22);
        System.out.println(map);

        // clear
        map.clear();
        System.out.println(map);

    }
}
```



![](https://img.fengqigang.cn//img/20210510135846.png)





**containsKey** 是否包含指定的key值 



```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);
        map.put("wu", 20);
        map.put("zl", 22);
        System.out.println(map);

        System.out.println(map.containsKey("zs"));

    }
}
```



![](https://img.fengqigang.cn//img/20210510135953.png)



**containsValue** 是否包含指定的value

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);
        map.put("wu", 20);
        map.put("zl", 22);
        System.out.println(map);

        System.out.println(map.containsValue(23));

    }
}
```



![](https://img.fengqigang.cn//img/20210510140036.png)





**equals**

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);
        HashMap map1 = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);
        map1.put("zs", 18);
        map1.put("ls", 20);
        System.out.println(map);
        System.out.println(map1);

        System.out.println(map.equals(map1));

    }
}
```



![](https://img.fengqigang.cn//img/20210510140201.png)





**get(object key)**

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        // put
        map.put("zs", 18);
        map.put("ls", 20);

        System.out.println(map.get("zs"));
    }
}
```



![](https://img.fengqigang.cn//img/20210510140307.png)






**putAll**

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);
        HashMap map1 = new HashMap<String, Integer>(2);

        //put
        map.put("zs", 18);
        map.put("ls", 20);

        // putAll
        map1.putAll(map);

        System.out.println(map);
        System.out.println(map1);
    }
}
```



![](https://img.fengqigang.cn//img/20210510140438.png)





**remove(Object key)**

根据key键值，删除keyvalue数据

```java
public class TestMap {
    public static void main(String[] args) {
        HashMap map = new HashMap<String, Integer>(2);

        //put
        map.put("zs", 18);
        map.put("ls", 20);

        //remove
        map.remove("zs");

        System.out.println(map);
    }
}
```



![](https://img.fengqigang.cn//img/20210510140543.png)



**Collection<V> values()** 返回这个map的值集

**set<K> keySet()** 返回这个map对象的键集

** set<Map.Entry<K,V>> entrySet ** 返回 这个 map 的键值对

### HashMap

1. HashMap 是 Map 接口的子实现 (存储的是 key - value 数据)

2. HashMap 表示一个 Hash 表

3. HashMap 的底层结构， 数组+ 链表+红黑树(jdk1.8 之前就是存粹的数组+链表)

4.HashMap 的效率非常高: 存储/查找

5.数组的默认初始容量 16, 数组的扩容机制 2 倍

6. HashMap 存储的Key-value 数据 ，经过散列之后 是无序的
7. HashMap 不允许存储重复元素key：（重复的定义）
8. 允许存储 null 值 (key-value 都允许为null)

![](https://img.fengqigang.cn//img/20210510172918.png)

6. 线程不安全
7. HashMap 加载因子默认是0.75, 尽量加载因子在0.5 ~ 1之间

 一个 HashMap 底层数组的扩容阈值 = 数组长度 * 加载因子

11. hash 值的计算 (h = key.hashCode()) ^(h >>> 16)

由于我们 HashMap 在做根据 hash 值 取

12. HashMap 的底层数组，是一个Node类型的数组，这个Node类型包含四个参数，分别是hash值 ，key, value, next

13. 我们最终存储到 HashMap 中的是一个结点类型, 这个结点类型包含四个

14. HashMap 的重复的定义， 首先 hash 值是否一样， hash 一样的情况下，两个key是否直接相等

15. 如果存储的数据key已经存在(key)重复了，那么会用新的value值覆盖旧value值

16. 如果我们把一份数据 key-value (已经存储到 HashMap中) 中的 Key通过引用修改，也就意味着一份key-value数据， 一旦存储到 hashmap 中就不要通过引用修改 key 了.

17. 当链表长度超过8， 达到9的时候(算上新添加的元素)， 会由链表转化为红黑树

18. 当链表长度超过8，达到9的时候(算上新添加的元素)， 如果同时数组长度小于64的时候，会有限选择扩容，而非转化为红黑树(注意: 如果扩容的时候，原本存在于x位置的元素，可能依旧存储在x, 还有可能存储到旧长度 + x的位置)

    ![](https://img.fengqigang.cn//img/20210510172114.png)

如果链表转化为红黑树，红黑树是一个特殊的二叉搜索树，需要比较大小， 在Hashmap中红黑树比较大小的方式是 hash如何计算.

19.删除有可能导致红黑色树转化为链表

![](https://img.fengqigang.cn//img/20210510173914.png)



20. 扩容也可能导致红黑树转化为, 扩容有可能导致红黑树拆成两部分

扩容有可能导致红黑树拆成两部分，在这两部分中，任意部分，如果元素数量小于等于6的话，会由红黑树转化成链表

![](https://img.fengqigang.cn//img/20210510174648.png)

![](https://img.fengqigang.cn//img/20210510174756.png)






- HashMap 的存储思想?

![](https://img.fengqigang.cn//img/20210510163610.png)













- 什么时候链表会转化成红黑树?

![](https://img.fengqigang.cn//img/20210510155627.png)



![](https://img.fengqigang.cn//img/20210510164830.png)



![](https://img.fengqigang.cn//img/20210510165242.png)

![](https://img.fengqigang.cn//img/20210510165254.png)

当链表超过8,达到9的时候(算上新添加的上的元素), 会由链表转化为红黑树

![](https://img.fengqigang.cn//img/20210510165714.png)





### 红黑树变成链表?





- 存储相同的值 

**两次存储的"zs" 值 一样， 因为他们两个hashCode值 都一样**

如果有两个元素hash值 一样，并不能完全保证他们两个一样



两个zs没法存



![](https://img.fengqigang.cn//img/20210510160015.png)



![](https://img.fengqigang.cn//img/20210510160409.png)



1. 首先判断: 已经存储到table 数组中里的i位置的元素p, 他key的hash值和新存储
2. 两份key-value数据的key是否相等， 或者相equals



- 重写 **hashCode**









**删除已经改变的位置**

![](https://img.fengqigang.cn//img/20210510162412.png)

![](https://img.fengqigang.cn//img/20210510162902.png)





红黑树不是自平衡的二叉树



数据结构， 底层结构, 实现













![](https://img.fengqigang.cn//img/20210510102243.png)


**Key-value** 数据常见:

key-value 数据非常常见

**Key-value 数据具有自我描述性, 完全可以描述对象**

- json

key-value

![](https://img.fengqigang.cn//img/20210510105619.png)






