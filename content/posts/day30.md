---
title: "Day30"
date: 2021-05-06T23:31:19+08:00
lastmod: 2021-05-06
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 集合类的分类?

- Collection
    - List (线性表子接口)
        - **ArrayList**: 1
        - LinkedList: 2
        - Vector -> Stack
    - Queue (队列子接口)
        - Deque
        - BlockingQueue
    - Set (集合子接口)
        - HashSet: 2
        - LinkedHashSet: 3
        - TreeSet:　3
- Map (Key-value)
    - **HashMap**: 1
    - LinkedHashMap： 3
    - TreeMap： 3

### 如何解释一个集合类（HashMap）的特点, 要解释那些东西?

1.  这个集合类是谁的子类/接口
    
2.  这个集合类表示是的是一种什么数据结构
    
3.  这个集合类他的底层结构是什么(数组，链表，数组+链表)
    
4.  如果底层结构是数组，谈数组的默认初始容量，数组的扩容机制
    
5.  这个集合类是否有序(位序)
    有序: **添加的位置是不是可以预期的**
    
6.  这个集合类是否允许存储重复元素(二叉搜索树不允许有重复元素)
    
7.  这个集合类是否允许存储null
    
8.  这个集合类是否线程安全
    

### 为什么需要集合类？

很多情况下，我们需要对一组对象进行操作

很可能事先并不知道到底有多少对象

为了解决这个问题，**java** 就提供了集合类供我们使用

### 集合类有什么特点?

a. 只能存储引用数据类型: (集合类是个数据容器, 用了泛型，泛型只能是引用类型)

b. 可以自动地调整自己的大小: (实现了扩容机制)

![](https://img.fengqigang.cn//img/20210505173337.png)

### 数组和集合类都是容器，它们有什么不同?

a. 数组可以存储基本数据类型，集合不可以

b. 数组的长度是固定的，集合可以自动调整自己的大小

c. 数组的效率高，相对来说集合效率比较低

d. 数组没有API, 集合有丰富的API

### 什么是逻辑结构和物理结构?

**逻辑结构** : 描述数据元素间的逻辑关系

**物理结构**: 存储结构或者映像

- 顺序映像:

借助的是存储器中的相对位置来表示数据元素之间的逻辑关系

- 非顺序映像:

借助元素存储地址的"指针"， 来表示数据元素的逻辑关系

### **Collection** 有什么特点?

1.  Collection 是 Collection 集合体系的顶级接口
    
2.  一些 **collection** 的子实现是有序的，而另一些 **collection** 的子实现则是无序的
    
3.  一些 **collection** 的子实现是允许存储重复元素的，而另一些 **collection** 的子实现则是不允许存储重复元素的(==, 地址，compareble 自然排序)
    
4.  一些 **Collection** 的子实现是允许存储 null, 而另一些 **Collection** 的子实现是不允许存储null
    

### **Collection** 中有哪些API?

**add**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        System.out.println(collection);
    }
}
```

![](https://img.fengqigang.cn//img/20210506104153.png)

**size**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        System.out.println(collection);
        System.out.println(collection.size());
    }
}
```

![](https://img.fengqigang.cn//img/20210506104235.png)

**addAll**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");


        LinkedList<String> collection1 = new LinkedList<>();
        collection1.add("ww");
        collection1.addAll(collection);

        System.out.println(collection);
        System.out.println(collection1);
    }
}
```

![](https://img.fengqigang.cn//img/20210506104502.png)

**clear**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");


        System.out.println(collection);
        collection.clear();
        System.out.println(collection);
        System.out.println(collection.isEmpty());

    }
}
```

![](https://img.fengqigang.cn//img/20210506104611.png)

**contains**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");


        System.out.println(collection.contains("ls"));

    }
}
```

![](https://img.fengqigang.cn//img/20210506104708.png)

**containsAll**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        ArrayList<String> collection1 = new ArrayList<>();
        collection1.add("zs");
        collection1.add("ls");

        System.out.println(collection.containsAll(collection1));

    }
}
```

![](https://img.fengqigang.cn//img/20210506193810.png)

**remove**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection1 = new ArrayList<>();
        collection1.add("zs");
        collection1.add("ls");

        System.out.println(collection1);
        collection1.remove("zs");
        System.out.println(collection1);
    }
}
```

![](https://img.fengqigang.cn//img/20210506193957.png)

**removeAll**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        ArrayList<String> collection1 = new ArrayList<>();
        collection1.add("zs");
        collection1.add("ls");

        collection.removeAll(collection1);
        System.out.println(collection);
    }
}
```

![](https://img.fengqigang.cn//img/20210506194145.png)

**retainAll**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        ArrayList<String> collection1 = new ArrayList<>();
        collection1.add("zs");
        collection1.add("ls");

        collection.retainAll(collection1);
        System.out.println(collection);
    }
}
```

![](https://img.fengqigang.cn//img/20210506194508.png)

**toArray** 不常用

返回一个数组： 包含所有Collection集合类的元素

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        Object[] objects = collection.toArray();
        for (int i = 0; i < objects.length; i++) {
            System.out.println(objects[i]);
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210506194744.png)

**T\[\] toArray(T\[\] a)**

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        Object[] strs = new Object[10];

        strs[0] = 1;
        strs[1] = 1;
        strs[2] = 1;
        strs[3] = 1;
        strs[4] = 1;
        strs[5] = 1;
        strs[6] = 1;
        strs[7] = 1;
        strs[8] = 1;
        strs[9] = 1;

        System.out.println("toArray前:");

        for (int i = 0; i < strs.length; i++) {
            System.out.println(strs[i]);
        }

        System.out.println("toArray后:");

        Object[] strings = collection.toArray(strs);
        for (int i = 0; i < strings.length; i++) {
            System.out.println(strings[i]);
        }
    }
}
```

它的最后一个元素会被置换转 **null**

### Iterator

```java
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        Iterator<String> iterator = collection.iterator();


        System.out.println("后面是否还有元素可以遍历? " + iterator.hasNext());
        System.out.println("输出遍历的结果" + iterator.next());
        System.out.println("输出遍历的结果" + iterator.next());
        iterator.remove();

        System.out.println(collection);
    }
}
```

![](https://img.fengqigang.cn//img/20210506200521.png)

1.  谈理论的时候，我们认为的遍历的位置指向，是在两个元素之间

![](https://img.fengqigang.cn//img/20210506200614.png)

2.  遍历的起始位置是在第一个元素之前
3.  在遍历之前是不可以删除的，因为remove删除的是刚刚遍历过的元素(**删除不能连续进行，刚刚遍历的元素只有一个**)
4.  为什么Iterator是个接口? 

```
Iterator<String> iterator = collection.iterator();
返回的对象， 是 Iterator 的子实现，并且是具体collection 子类的内部类(内部类比较适合访问 collection 子类 的数据)
```

### Foreach 循环

增强 for 循环， 加强的 for 循环

对于 Collection 集合类，虽然它提供了 Iterator 方法用来遍历，性能优于 toArray 的

但是在实际工作中没有人使用iterator 迭代，通常都是使用 Foreach循环

![](https://img.fengqigang.cn//img/20210506112739.png)

![](https://img.fengqigang.cn//img/20210506113029.png)

### ConcurrentModificationException

并发修改异常

颗粒度比较细

Iterator 迭代就是依赖于源数据进行的，我们希望在我们迭代的过程中别人不要来修改这个源集合数据，如果非要修改的，让我自己来修改

1.  在多线程的情况下，一个线程在用 iterator 遍历， 另一个在修改，由于原集合类或标记 modCount 这个参数(修改次数) 会增加，会导致在 iterator 迭代的时候如下不相等
    ![](https://img.fengqigang.cn//img/20210506114934.png)
    
2.  在单线程情况下，如果 interator 对象已经产生：意味着如下参数已经同步
    

![](https://img.fengqigang.cn//img/20210506115019.png)

```
public class TestCollection {
    public static void main(String[] args) {
        ArrayList<String> collection = new ArrayList<>();
        collection.add("zs");
        collection.add("ls");
        collection.add("wu");
        collection.add("zl");

        for(String s : collection){
           collection.add("lb");
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210506202039.png)

意味着增强的 for 循环在便利的过程中，也不能调用原集合类的方法修改

![](https://img.fengqigang.cn//img/20210506141808.png)

对于数组（数组在 java 中是一个非常特殊的存在，）也可以使用 Foreach 循环， 但是它和iterator 迭代没有任何关系，数组的增强的for循环会编译成普通的fori循环

### 接口存在有什么意义?

1.  实现多继承
    
2.  提供 规范 和 约束
    

![](https://img.fengqigang.cn//img/20210506112147.png)


