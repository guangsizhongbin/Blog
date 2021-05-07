---
title: "Day31"
date: 2021-05-07T23:31:41+08:00
lastmod: 2021-05-07
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### List的特点

1. List 的是 Collection 的子接口

2. List 是 Collection 的一个 **线性表** 子接口  -> (有序, 有下标操作)

3. 有序

4. 允许重复元素存在

5. 允许 null


### API?

**add**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zl");
        System.out.println(list);
    }
}
```

![](https://img.fengqigang.cn//img/20210507141726.png)



**addAll**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zl");

        ArrayList<String> list1 = new ArrayList<>();
        list1.add("zs");
        list1.add("ls");
        list1.add("wu");
        list1.add("zl");

        System.out.println(list.addAll(list1));
        System.out.println(list);
    }

}
```



![](https://img.fengqigang.cn//img/20210507141906.png)

**add**(index)

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zl");

        ArrayList<String> list1 = new ArrayList<>();
        list1.add("1");
        list1.add("2");
        list1.add("3");
        list1.add("4");

        System.out.println(list.addAll(1, list1));
        System.out.println(list);
    }

}
```

![](https://img.fengqigang.cn//img/20210507142008.png)



**get**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zl");

        System.out.println(list.get(0));
    }
}
```

![](https://img.fengqigang.cn//img/20210507142053.png)



**indexOf**

```
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zl");

        System.out.println(list.indexOf("zs"));
    }
}
```

![](https://img.fengqigang.cn//img/20210507142137.png)





**lastIndexOf**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add("ls");

        System.out.println(list.lastIndexOf("zs"));
    }
}
```

![](https://img.fengqigang.cn//img/20210507142246.png)



**remove**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add("ls");

        System.out.println(list.remove(0));
        System.out.println(list);
    }
}
```

![](https://img.fengqigang.cn//img/20210507142338.png)



**toArray()**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add("ls");

        Object[] objects = list.toArray();
        for (int i = 0; i < objects.length; i++) {
            System.out.println(objects[i]);
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210507142456.png)



**iterator**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add("ls");

        Iterator<String> iterator = list.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210507142555.png)

**listIterator**

```java
public class TestLink {
    public static void main(String[] args) {
        ArrayList<String> list = new ArrayList<>();

        list.add("zs");
        list.add("ls");
        list.add("wu");
        list.add("zs");
        list.add("ls");

        ListIterator<String> iterator = list.listIterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210507142712.png)



### ListIterator

public interface ListIterator<E> extends Iterator<E>

1. 他是个接口， 他是 Iterator 的子接口
2. ListIterator , 在 Iterator 的基础上，提供了向前遍历的接口

![](https://img.fengqigang.cn//img/20210507110928.png)

![](https://img.fengqigang.cn//img/20210507111017.png)

![](https://img.fengqigang.cn//img/20210507111202.png)

![](https://img.fengqigang.cn//img/20210507111349.png)

![](https://img.fengqigang.cn//img/20210507111543.png)

**逆序遍历**

![](https://img.fengqigang.cn//img/20210507111808.png)

**sublist** 是一个视图方法, 只是维护了标记

![](https://img.fengqigang.cn//img/20210507111914.png)

### 什么是视图方法（sublist）?

 a view of the portion 

**虚表(视图)**: 虚拟表，维护一个标记表(手机)， 指向一个实际存储数据的表



![](https://img.fengqigang.cn//img/20210507114513.png)





集合类的视图方法，实际上还是原集合类的数据，视图方法返回的对像实际上持有的仅仅是



![](https://img.fengqigang.cn//img/20210507113820.png)



![](https://img.fengqigang.cn//img/20210507113843.png)



### 一个接口与接口的关系?

一个接口是另一个接口的增强

### 一个子类与子类的关系?

一个子类是想实现另一个子类





