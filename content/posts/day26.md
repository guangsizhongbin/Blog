---
title: "Day26"
date: 2021-04-29T23:33:10+08:00
lastmod: 2021-04-29
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 如何定义一个双链表?

**定义结点**

一般有:

**pre** , **value** , **next**

**结点**

```java
    class Node {
        String value;
        Node next;
        Node pre;

        public Node(Node pre, String value, Node next) {
            this.value = value;
            this.next = next;
            this.pre = pre;
        }
    }
```

**链表**

```java
    class Node {
        String value;
        Node next;
        Node pre;

        public Node(Node pre, String value, Node next) {
            this.value = value;
            this.next = next;
            this.pre = pre;
        }
    }
```

### 双链表如何根据内容增加?

- 链表为空
- 链表非空

```java
    public boolean add(String str) {
        // 判断链表是否为空
        if (size == 0) {
            head = new Node(null, str, null);
            end = head;
            size++;
        } else {
            // 链表不为空
            end.next = new Node(end, str, null);
            end = end.next;
            size++;
        }
        return true;
    }

```

### 双链表中如何根据内容删除?

- 判断链表是否为空, 为空抛出异常
- 非空
    - 判断是否是第一个位置
    - 判断删除的是否是最后一个位置

```java
        public boolean remove(String str) {
        // 判断链表为空
        if (size == 0) throw new RuntimeException("Link is empty");
        // 判断要删除的元素是否为null
        if (str == null) {
            // 头结点就是null
            if (null == head.value) {
                // 只有一个元素
                if (size == 1) {
                    // 头结点和尾结点均指向空
                    head = null;
                    end = null;
                    size--;
                    return true;
                } else {
                    // 不只有一个元素
                    head = head.next;
                    size--;
                    return true;
                }
            }
            // null 不是头结点
            // 指向 头结点后的元素
            Node mid = head.next;
            while (mid != null && mid.value != null) {
                mid = mid.next;
            }
            //  1. mid == null, 没找到
            if (mid == null) return false;
            //  2. mid.value == null 找到了
            //  2. 判断删除的元素是否是最后一个元素
            //  2.1 删除的元素是最后一个元素(mid 就是要删除的元素)
            if (mid == end) {
                end = mid.pre; // end 往前移
                end.next = null; // end 后变成null
                size--;
                return true;
            }
            //  2.2 删除的元素不是最后一个元素(mid 就是要删除的元素)
            mid.next.pre = mid.next.next;
            mid.pre.next = mid.next;
            size--;
            return true;
        } else {
            // 链表不为空
            // 1. 删除的是第一个位置
            if (head.value.equals(str)) {
                head = head.next;
                head.pre = null;
                size--;
                return true;
            } else {
                // 2. 删除的是不是第一个位置
                Node mid = head.next;
                while (mid != null && !mid.value.equals(str)) {
                    mid = mid.next;
                }
                // 1. mid == null;
                if (mid == null) return false;
                // 2. mid.value.equals(str)
                // 2.1 删除的不是最后一个元素
                // 2.2 删除的是最后一个元素
                if (mid == end) {
                    end = mid.pre;
                    end.next = null;
                    size--;
                    return true;
                } else {
                    mid.next.pre = mid.pre;
                    mid.pre.next = mid.next;
                    size--;
                    return true;
                }
            }
        }
    }

```

### 如何使双链表根据内容查找?

```java
    public boolean contains(String str) {
        // 1. 链表是否为空
        if (isEmpty()) throw new RuntimeException("linked is empty");
        // 2. 链表不为空
        // 2.1 判断是null
        if (str == null) {
            Node mid = head;
            while (mid != null && mid.value != null) {
                mid = mid.next;
            }
            // 2.1.1 mid == null 没找到
            if (mid == null) return false;
            // 2.1.2 mid.value == null 找到了, mid就是
            return true;
        } else {
            // 2.2 判断的不是null
            Node mid = head;
            while (mid != null && !str.equals(mid.value)) {
                mid = mid.next;
            }
            // 2.2.1 mid == null 没找到
            if (mid == null) return false;
            // 2.2.2 mid.value == str ， 找到了, mid 就是
            return true;
        }
    }

```

### 双链表如何实现根据内容替换?

```java
    public boolean set(String oldValue, String newValue) {
        // 1. 链表为空
        if (size == 0) throw new RuntimeException("Link is Empty");
        // 2. oldValue 为null
        if (oldValue == null) {
            // mid 为目标结点
            Node mid = head;
            while (mid != null && mid.value != null) {
                mid = mid.next;
            }
            // 2.1 mid == null
            if (mid == null) return false;
            // 2.2 mid.value == null
            mid.value = newValue;
            return true;
        } else {
            // 3. oldValue 非null
            // mid 为目标结点
            Node mid = head;
            while (mid != null && mid.value != oldValue) {
                mid = mid.next;
            }
            // 3.1 mid == null
            if (mid == null) return false;
            // 3.2 mid.value == null
            mid.value = newValue;
            return true;
        }
    }

```

### 双链表如何根据下标做添加？

- 添加的为头位置
    - 链表为空
    - 链表非空
- 添加的不是头结点
    - 判断添加的位置()
    - 从后往前，还是从前往后
        - 最后一个结点的判断

```java
    public boolean add(int index, String str) {
        // 1. 判断下标是否越界 (头, 尾+1)
        if (index < 0 || index > size) throw new IllegalArgumentException("size " + size);
        // 2.1 添加的位置在头部
        if (index == 0) {
            if (isEmpty()) {
                // 链表为空
                head = new Node(null, str, head);
                size++;
                return true;
            } else {
                // 链表非空
                Node node = new Node(null, str, head);
                head.pre = node;
                head = node;
                size++;
                return true;
            }
        } else {
            // 2.2 添加的位置不在头部
            // 2.2.1 添加的位置在尾部
            if (index == size) {
                end = new Node(end, str, null);
                size++;
                return true;
            }
            // 2.2.2 添加的位置不在尾部
            if (index < (size / 2)) {
                // 2.2.2.1 判断它是在前半部分
                Node mid = head;
                int num = 0;
                while (num < index) {
                    mid = mid.next;
                    num++;
                }
                // num == index;
                Node node = new Node(mid, str, mid.next);
                node.pre.next = node;
                node.next.pre = node;
                size++;
                return true;
            } else {
                // 2.2.2.1 判断它是在前半部分
                Node mid = end;
                int num = size;
                while (num > index) {
                    mid = mid.pre;
                    num--;
                }
                // num == index;
                Node node = new Node(mid, str, mid.next);
                node.pre.next = node;
                node.next.pre = node;
                size++;
                return true;
            }
        }
    }

```

### 双链表根据下标做删除?

- index 判断
- 链表为空判断
- 删除的是头结点
    - size 为 1
    - 非1
- 删除的不是头结点
    - 查找元素
        - 判断是否为尾结点
        - 不是尾结点

```java
    public String remove(int index) {
        // 判断index是否合法
        if (index < 0 || index >= size) throw new IllegalArgumentException("size :" + size);
        // 判断链表是否为空
        if (isEmpty()) throw new RuntimeException("linked is empty");

        // 要返回的oldValue
        String oldValue = "";

        // 判断删除的元素是否是第1个
        if (index == 0) {
            // 判断其后还有没有元素
            if (size == 1) {
                oldValue = head.value;
                head = null;
                end = null;
                size--;
            } else {
                // 其后还有元素
                oldValue = head.value;
                head = head.next;
                head.pre = null;
                size--;
            }
        } else {
            // 删除的元素不是第1个元素
            // 判断是否为最后一个元素
            if (index == size - 1) {
                // 是最后一个元素
                oldValue = end.value;
                end = end.pre;
                end.pre = null;
                size--;
            } else {
                // 判断其是前一半还是后一半
                if (index < (size / 2)) {
                    int flag = 1;
                    Node mid = head.next;
                    while (flag < index - 1) {
                        mid = mid.next;
                        flag++;
                    }
                    oldValue = mid.next.value;
                    mid.next = mid.next.next;
                    mid.next.pre = mid.pre;
                    size--;
                } else {
                    int flag = size - 2;
                    Node mid = end;
                    while (flag > index - 1) {
                        mid = mid.pre;
                        flag--;
                    }
                    oldValue = mid.next.value;
                    mid.next = mid.next.next;
                    mid.next.pre = mid.pre;
                    size--;
                }
            }
        }
        return oldValue;
    }

```

###　双链表如何根据下标查找?

```java
    public String get(int index) {
        if (index < 0 || index >= size) throw new IllegalArgumentException("size = " + size);

        Node mid = null;
        if (index > (size / 2)) {
            // 靠后
            mid = end;
            int tag = size - 1;
            while (tag != index) {
                mid = mid.pre;
                tag--;
            }
        } else {
            // 靠前 
            mid = head;
            int tag = 0;
            while (tag != index) {
                mid = mid.next;
                tag++;
            }
        }
        return mid.value;
    }

```

###　双链表如何根据下标修改?

```java
    public String set(int index, String str) {
        if (index < 0 || index >= size) throw new IllegalArgumentException("size" + size);

        Node mid = null;
        if (index > (size / 2)) {
            // 靠后
            mid = end;
            int tag = size - 1;
            while (tag != index) {
                mid = mid.pre;
                tag--;
            }
        } else {
            // 靠前
            mid = head;
            int tag = 0;
            while (tag != index) {
                mid = mid.next;
                tag++;
            }
        }

        String oldStr = mid.value;
        mid.value = str;
        return oldStr;
    }

```

###　数组与链表的时间复杂度?

**数组** 和 **链表** 操作的时间复杂度正好相反

|     | 添加/ 删除 | 查找  |
| --- | --- | --- |
| 数组  | O(n) | O(1) 根据下标 |
| 链表  | O(1) | O(n) |

1.  数组使用的是连续的内存空间，可以利用 **CPU** 的高速缓存磁盘预读数据，链表的内存空间不连续的，不能有效预读数据。 如果数组过大，系统没有足够的连续内存空间，会抛出Out of Memory.
2.  数组的缺点是大小固定，没法动态的调整大小，如果要存储一些对象，如果数组太大，浪费内存空间; 如果数组太小，我们需要重新重新申请一个更大数组，并将数据拷贝过去，耗时.
3.  如果业务对内存的使用非常苛刻，数组更适合，因为结点有指针域，更消耗内存，而且对链表的频繁插入和删除，会导致结点对象的频繁创建和销毁，有可能会导致频繁的GC活动.

### 什么是泛型?

泛型, 即" **参数化类型** "，就是将类型由原来的 **具体类型"参数化"** , 此时 **类型也定义成参数形式** ，然后在 **使用/ 调用时传入具体的类型**

**DemoUser.java**

```java
public class DemoUser {
    public static void main(String[] args) {
        User<String> user1 = new User<>();
        user1.age = "1";

        System.out.println(user1.age);
    }
}
```

**User.java**

```java
public class User <T>{
    String name;
    T age;
}
```

### 泛型一般用于什么样的情况?

泛型一般常用于 **java** 的集合类中

![](https://img.fengqigang.cn//img/20210429221940.png)

### 使用泛型有什么好处?

1.  提高了程序的 **安全性**
2.  将运行期遇到的 **问题转移到了编译期** : 编译时问题会提示我们有些错误，可以立刻修改
3.  省去了类型强转的麻烦

### 泛型的有哪几种?

1.  泛型类
2.  泛型方法
3.  泛型接口

![](https://img.fengqigang.cn//img/20210429151705.png)

### 什么是泛型类?

把泛型定义在类上

格式: public class 类名 <泛型类型1,...>

参数化类型必须是引用类型



![](https://img.fengqigang.cn//img/20210429143842.png)

![](https://img.fengqigang.cn//img/20210429143852.png)

### **泛型的一般定义习惯**

![](https://img.fengqigang.cn//img/20210429144036.png)

![](https://img.fengqigang.cn//img/20210429144248.png)

![](https://img.fengqigang.cn//img/20210429144552.png)

### 如果我们定义一个泛型类/接口/方法， 都可以定义多个泛型，在语法上是完全允许的，但是，一般来说不要把泛型定义过多，（不要超过两个）

### 如何我们定义一个泛型，但是在使用的时候并没有指定泛型类型，那么这个泛型类型会指定为什么?

![](https://img.fengqigang.cn//img/20210429145108.png)

Object 类型

![](https://img.fengqigang.cn//img/20210429145145.png)

### java 在什么时候有泛型?

![](https://img.fengqigang.cn//img/20210429145803.png)

![](https://img.fengqigang.cn//img/20210429145822.png)

### 泛型 继承?

![](https://img.fengqigang.cn//img/20210429150056.png)

![](https://img.fengqigang.cn//img/20210429150546.png)

![](https://img.fengqigang.cn//img/20210429150748.png)

![](https://img.fengqigang.cn//img/20210429151012.png)

![](https://img.fengqigang.cn//img/20210429151342.png)

![](https://img.fengqigang.cn//img/20210429151626.png)

### 泛型接口?

![](https://img.fengqigang.cn//img/20210429152145.png)

![](https://img.fengqigang.cn//img/20210429152050.png)

### 泛型方法？

![](https://img.fengqigang.cn//img/20210429152219.png)

![](https://img.fengqigang.cn//img/20210429152306.png)

**定义泛型**

![](https://img.fengqigang.cn//img/20210429152405.png)

![](https://img.fengqigang.cn//img/20210429152543.png)

### 什么是泛型擦除?

![](https://img.fengqigang.cn//img/20210429155629.png)

![](https://img.fengqigang.cn//img/20210429155043.png)

![](https://img.fengqigang.cn//img/20210429155444.png)

### 泛型可以用int吗?

![](https://img.fengqigang.cn//img/20210429155744.png)

![](https://img.fengqigang.cn//img/20210429155826.png)

### 自动拆箱装箱?

![](https://img.fengqigang.cn//img/20210429155951.png)

### jvm的协变?

![](https://img.fengqigang.cn//img/20210429160341.png)

![](https://img.fengqigang.cn//img/20210429160901.png)

### 泛型不允许协变

![](https://img.fengqigang.cn//img/20210429161156.png)

### 泛型不允许协变，但不想用类似数组的功能?

![](https://img.fengqigang.cn//img/20210429161436.png)

![](https://img.fengqigang.cn//img/20210429161603.png)

![](https://img.fengqigang.cn//img/20210429161705.png)

![](https://img.fengqigang.cn//img/20210429162126.png)

![](https://img.fengqigang.cn//img/20210429162407.png)

![](https://img.fengqigang.cn//img/20210429163933.png)

### 什么是 Bean 类?

非功能类, 模拟实际中存在的事物

### 什么是功能类?

### foreach?

![](https://img.fengqigang.cn//img/20210429171119.png)

### 可变长参数?

### java 集合类?

![](https://img.fengqigang.cn//img/20210429171648.png)

### 线性表的分类?

操作受限

### 什么是顺序映像？ 什么是非顺序映像?

### 栈的概念?

![](https://img.fengqigang.cn//img/20210429172823.png)

### 如何实现栈(数组)?

1.  添加: push
2.  删除: pop
3.  查看栈顶元素: peek

![](https://img.fengqigang.cn//img/20210429173755.png)

**构造方法**

- 无参

![](https://img.fengqigang.cn//img/20210429173841.png)

- 有参

![](https://img.fengqigang.cn//img/20210429174111.png)

**push**

![](https://img.fengqigang.cn//img/20210429175150.png)

![](https://img.fengqigang.cn//img/20210429175204.png)

**pop**

![](https://img.fengqigang.cn//img/20210429175602.png)

**peek**

![](https://img.fengqigang.cn//img/20210429175705.png)

### 不能是泛型数组


