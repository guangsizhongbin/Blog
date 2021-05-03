---
title: "Day27"
date: 2021-04-30T22:52:59+08:00
lastmod: 2021-04-30
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---


### MyLIstStack

### 栈列有什么应用?

1. 函数调用栈
2. 反序字符串
3. 括号匹配
4. 编译器利用栈实现表达式求值
5. 浏览器的前进后退功能
6. 利用栈实现 **DFS: depth-first-search**



### 实现renumber方法?

![](https://img.fengqigang.cn//img/20210430100447.png)

### 实现括号匹配(judgeBracket)方法?

![](https://img.fengqigang.cn//img/20210430101704.png)

### 什么是中缀表达式, 前缀表达式, 后缀表达式?

运算符放到

**中间**: 中缀表达式

**之前**: 前缀表达式

**后面**: 后缀表达式

### (2 * ( 9 + 6 / 3 -5 ) + 4) 转成后缀表达式的过程是什么样的?

**从左到右** 遍历中缀表达式的每个数字和符号

若是数字就输出，即成为后缀表达式的一部分

若是符号，则判断其与栈顶符号的优先级，是右括号或者优先级低于栈顶符号(乘除优先加减)

则栈顶元素依次出栈并输出，并将当前符号进栈，一直到最终输出后缀表达式为止

![20210503183651](https://img.fengqigang.cn//img/20210503183651.png)



### 2 - 1 + 3 * 2 -5 转成后缀表达式的结果是什么?

中缀转后缀是 **从左往右** 扫描

2 1  - 3 2 * + 5 -

![](https://img.fengqigang.cn//img/20210430102809.png)

### (1 + (3 * 4) / 6) -5 转成前缀表达式的过程是什么?

1. 初始化两个栈: 运算符栈 `S1`, 操作数栈 `S2`

2. 从右至左扫描中缀表达式

3. 遇到 `操作数` 时, 将其压入 `S2`

4. 遇到 `运算数` 时, 比较其与 `S1` 栈顶运算符的优先级

- 如果 `S1` 为空, 或栈顶运算符为右括号 `)`, 或其优先及比栈顶运算符的优先级较高或相等，则直接将 `此运算符` 入栈

- 否则， 将 `S1` 栈顶的运算符弹出并压入到 `S2` 中， 再次进行与 `S1` 栈顶运算符的优先级比较

![20210503190950](https://img.fengqigang.cn//img/20210503190950.png)

然后将其弹出 

```
- + 1 / * 3 4 6 5
```

### (1 + (3 * 4) / 6 ) - 5 转成前缀表达式后的结果是什么?

```
- + 1 / * 3 4 6 5
```

### 什么是队列?

是一种 "操作受限" 的线性表

体现在一端插入数据在另一端删除数据

![20210503191715](https://img.fengqigang.cn//img/20210503191715.png)

### 在用链表实现队列时，如何定义一个队列?

**队头**

**队尾**

**队长度**

```java
public class MyLinkedQueue<T> {

    private Node head; // 队头
    private Node end; // 队尾
    private int size;

    class Node {
        T value;
        Node next;

        public Node(T value, Node next) {
            this.value = value;
            this.next = next;
        }
    }
}
```


### 如何实现向链表队列中添加结点?

添加结点为 **offer**

1. 判断链表是否空

-  为空， 添加至队头, head = end

- 不为空，添加至end, end后移

```java
    public boolean offer(T t) {
        // 如果原队列为空
        if (isEmpty()) {
            head = new Node(t, null);
            end = head;
            size++;
            return true;
        }

        // 如果原出队列不为空
        end = new Node(t, null);
        end = end.next; // end 后移
        size++;
        return true;
    }
```


### 如何实现向链表队列中删除结点?

 **删除 poll**

1. 判断链表是否空

- 为空抛出异常

- 只有一个结点

- 不只有一个结点

```java
    public T poll() {
        // 链表为空
        if (isEmpty()) throw new RuntimeException("queue is empty");

        // 链表中只有一个元素
        if (size == 1) {
            T oldValue = head.value;
            head = null;
            end = null;
            size--;
            return oldValue;
        } else {
            // 链表中不止一个元素
            T oldValue = end.value;
            head = head.next;
            size--;
            return oldValue;
        }
    }
```

### 如何实现向链表队列中查看队头元素?

**查看队头元素 peek**

```java
    public T peek(){
        if(isEmpty()) throw new RuntimeException("queue is Empty");
        return head.value;
    }
```

 ### 如何用数组定义一个队列?

```java
public class MyArrayQueue {
    Object objs;
    final int INIT_CAPACITY = 10;
    final int MAX_CAPACITY = Integer.MAX_VALUE - 8;

    public MyArrayQueue() {
        objs = new Object[INIT_CAPACITY];
    }

    public MyArrayQueue(int initCapacity) {
        if (initCapacity <= 0 || initCapacity > MAX_CAPACITY)
            objs = new Object[initCapacity];
    }
}
```


### 用数组定义的队列，如何实现增加结点?

**offer**

1. 判断数组是否满?
	- 已满
		- 获取新的才度
				- 判断长度是否溢出
		- 新建一个数组
	- 未满
			- 原队列是否为空


```java
    public boolean offer(T t) {
        // 判断数组是否满?
        if (size == objs.length) {
            int newLen = getLen();
            grow(newLen);
        }
        // 如果原队列为空
        if (isEmpty()) {
            objs[head] = t;
            end = head;
            size++;
            return true;
        } else {
            end = (end + 1) % objs.length;
            objs[end] = t;
            size++;
            return true;
        }
    }

    private void grow(int newLen) {
        Object[] newArr = new Object[newLen];
        for (int i = 0; i < objs.length; i++) {
            int index = (head + i) % objs.length;
            newArr[i] = objs[index];
        }
        objs = newArr;
        head = 0;
        end = size - 1;
    }

    private int getLen() {
        int oldLen = objs.length;
        int newLen = objs.length << 1;

        // 判断数据是否溢出
        if (newLen >= MAX_CAPACITY || newLen <= 0) {
            newLen = MAX_CAPACITY;
        }

        // 如果新长度和旧长度一样
        if (oldLen == newLen) throw new RuntimeException("stack can not add");
        return newLen;
    }

```



![](https://img.fengqigang.cn//img/20210430112105.png)


### 用数组定义的队列，如何实现弹出结点?

**poll**

- 队列是否为空
		- 是否只有一个元素

```java
    public T poll() {
        if (isEmpty()) throw new RuntimeException("queue is Empty");

        if (size == 1) {
            // 原队列只有一个元素 
            T oldValue = (T) objs[head];
            head = 0;
            end = 0;
            size--;
            return oldValue;
        } else {
            // 队列中超过一个元素 
            T oldValue = (T) objs[head];
            head = (head + 1) % objs.length;
            size--;
            return oldValue;
        }
    }

```

### 用数组定义的队列，如何实现查看队头元素?

**peek**

- 队列是否为空

```java
    public T peek() {
        if (isEmpty()) throw new RuntimeException("queue is Empty");
        return (T) objs[head];
    }
```

### 队列有什么应用?

普通的队列的应用场景是很有限的， 一般在工程中用到的是 **阻塞队列**

**阻塞队列**: 常用于生产者 - 消费者模型中

当队列满的时候, 入队列就阻塞

当队列空的时候，出队列就阻塞


### 什么是ni的深度? 根的深度为多少?

对于任意结点 ni, ni 的深度为从根到 ni 的唯一路径的长

根的深度为0

### 什么是ni的高度? 所有的树叶高是多少?

ni 的高是从ni 到一片树叶的最长路径的长

所有树叶的高都为0

![20210503203802](https://img.fengqigang.cn//img/20210503203802.png)



### 为什么一颗树有 n 个结点， 那么它有 n-1 条边?

每一结点都有一个边指向它

每一条边都指向一个结点



### 什么是二叉树?

一个树，一个结点最多有两个孩子，孩子有严格的左右之分


![20210503204422](https://img.fengqigang.cn//img/20210503204422.png)



### 完美二叉树既是完全二叉树又是满二叉树吗?![20210503204422](https://img.fengqigang.cn//img/20210503204422.png)

是

### 如果一颗树既是完全二叉树又是满二叉树，那么它是完美二叉树吗?![20210503204422](https://img.fengqigang.cn//img/20210503204422.png)

不是




### 二叉树在第 i 层至多有多少个节点?

至多有 2的(i-1) 方个节点

### 层次为k的二叉树至多有多少个节点?

1 + 2 + 4 + ... + 2的(i - 1)次方 = 2的i次方 - 1

![20210503205134](https://img.fengqigang.cn//img/20210503205134.png)



### 对于任何一颗二叉树 T, 如果其叶子节点数为 n0, 度为2 的节点数为 n2, 则n0与n2存在什么样的关系?

**边数 = 节点数 - 1**

边数(从上向下) = n1 + 2n2

边数(从下往上) = n0 + n1 + n2 -1(去掉根)

**叶子结点的个数比度为2的结点的个数多1个**

**n0 = n2 + 1**


### 具有n个节点的完全二叉树，树的高度为多少?

log2n 向下取整


1 + 2 + 4 + ... + 2的(i - 1)次方 = 2的i次方 - 1







### 以根, 左, 右这三种方式遍历树，有多少种情况?

![](https://img.fengqigang.cn//img/20210430163810.png)

### 什么是先序遍历, 中序遍历，后序遍历?

**先序遍历**: 先遍历根结点， 再遍历左子树, 再遍历右子树

**中序遍历**: 先遍历左子树， 再遍历根结点, 再遍历右子树

**后序遍历**: 先遍历左子树， 再遍历右子树, 再遍历根结点


### ![20210503210638](https://img.fengqigang.cn//img/20210503210638.png) 其先序遍历，中序遍历， 后序遍历的结果是什么?

先序遍历:

A B D C E F

中序遍历:

B D A E F C

后序遍历:

D B F E C A


### 前序遍历，后序遍历，中序遍历分别能确定什么?


前序: 第一个元素是根

后序: 最后一个元素是根

中序: 如果知道根，根的左边序列是左子树结点， 右边序列是右子树结点


### 任意去两个遍历序列, 都可以建树吗?

前序 + 中序, 可以，**前序可以确定根节点， 中序可以根据根节点划分左右子树**


后序 + 中序, 可以，**后序可以确定根节点， 中序可以根据根节点划分左右子树**

前序 + 后序, 不可以，**都只能确定根节点**

### 二叉树的先序遍历 ABDECFG, 中序遍历 DBEAFGC, 试求它的后序遍历?

![20210503211805](https://img.fengqigang.cn//img/20210503211805.png)

### 什么是二叉搜索树?

又叫二叉排序树

左子树中所有结点的key比根结点的key小，并且左子树也是二叉搜索树

左子树中所有结点的key比根结点的key大，并且左子树也是二叉搜索树


