---
title: "Day25"
date: 2021-04-28T23:09:33+08:00
lastmod: 2021-04-28
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 如何利用双指针法输出输出中的中间元素(快指针与慢指针)?

```java
public class Ex3 {
    public static void main(String[] args) {
        Node zs = new Node("zs", null);
        Node ls = new Node("ls", null);
        Node wu = new Node("wu", null);
        Node sq = new Node("sq", null);
        Node qg = new Node("qg", null);

        zs.next = ls;
        ls.next = wu;
        wu.next = sq;
        sq.next = qg;

        System.out.println(getMidNode(zs).toString());

    }

    private static Node getMidNode(Node head) {
        Node f = head; // 快指针, 一次走2个位置
        Node l = head; // 慢指针, 一次走1个位置

        // 保证快指针的下一个和下下一个结点 不是 null
        while (f.next != null && f.next.next != null) {
            f = f.next.next; // 快指针走两步
            l = l.next; // 慢指针走一步
        }

        return l; // 返回慢指针的位置，就是链表中间的位置
    }
}

class Node {
    String Node;
    Node next;

    public Node(String node, Node next) {
        this.Node = node;
        this.next = next;
    }

    @Override
    public String toString() {
        return "Node{" +
                "Node='" + Node + '\'' +
                ", next=" + next +
                '}';
    }
}
```

![](https://img.fengqigang.cn//img/20210428162631.png)

### 如何利用双指针法确认链表中是否有环?

```java
public class Ex3 {
    public static void main(String[] args) {
        Node zs = new Node("zs", null);
        Node ls = new Node("ls", null);
        Node wu = new Node("wu", null);
        Node sq = new Node("sq", null);
        Node qg = new Node("qg", null);

        zs.next = ls;
        ls.next = wu;
        wu.next = sq;
        sq.next = ls;

        System.out.println(hasCircle(ls));

    }

    private static boolean hasCircle(Node head) {
        Node f = head; // 快指针
        Node l = head; // 慢指针

        while (f.next != null && f.next.next != null) {
            f = f.next.next;  // 快指针两步
            l = l.next; // 慢指针走一步

            //  若有环，快指针一定会在环内追慢指针, 快指针比慢指针要快，所以一定能追上
            if (f == l) {
                return true;
            }
        }

        return false;
    }
}

class Node {
    String Node;
    Node next;

    public Node(String node, Node next) {
        this.Node = node;
        this.next = next;
    }

    @Override
    public String toString() {
        return "Node{" +
                "Node='" + Node + '\'' +
                ", next=" + next +
                '}';
    }
}
```

![](https://img.fengqigang.cn//img/20210428163224.png)

### 如何用双指针法，判断链表中是否有环，若有返回其环的结点?

![](https://img.fengqigang.cn//img/20210428165440.png)

- 如何有环， 那么环内是一个快指针追慢指针的问题，
    快指针每次追一个位置，也就意味着，不会在追的过程中跳过去
    
- 环内有y个元素, 两个指针最坏的情况是,
    快指针比慢指针快一个位置,
    则快指针每走一次是追一个位置，则它需要走y-1次必然能追上慢指针
    
- 在追的时候必然在当前环内追上
    

![](https://img.fengqigang.cn//img/20210428165621.png)

```java
public class Ex3 {
    public static void main(String[] args) {
        Node zs = new Node("zs", null);
        Node ls = new Node("ls", null);
        Node wu = new Node("wu", null);
        Node sq = new Node("sq", null);
        Node qg = new Node("qg", null);

        zs.next = ls;
        ls.next = wu;
        wu.next = sq;
        sq.next = qg;
        qg.next = ls;

        System.out.println(getCircle(zs));

    }

    private static Node getCircle(Node head) {
        Node f = head; // 快指针
        Node l = head; // 慢指针

        while (f.next != null && f.next.next != null) {
            f = f.next.next;  // 快指针两步
            l = l.next; // 慢指针走一步

            //  若有环，快指针一定会在环内追慢指针, 快指针比慢指针要快，所以一定能追上
            if (f == l) {
                // 意味着有环，到相遇的位置
                break;
            }
        }

        // 走到这一步:
        //1. 没有环:  f.next = null || f.next.next == null
        //2. 有环: f == l

        if (f.next == null || f.next.next == null) {
            // 没有环
            return null;
        }

        // 有环
        f = head; // 把其中一个指针移动到链表最开始的地方
        while (f != l) {
            f = f.next;
            l = l.next;
        }
        // 返回哪一个都可以
        return l;
    }
}

class Node {
    String Node;
    Node next;

    public Node(String node, Node next) {
        this.Node = node;
        this.next = next;
    }

    @Override
    public String toString() {
        return "Node{" +
                "Node='" + Node + '\'' +
                //", next=" + next +
                '}';
    }
}
```

![](https://img.fengqigang.cn//img/20210428170759.png)

### 如何采用头插法反转单链表?

```java
public class Ex3 {
    public static void main(String[] args) {
        Node zs = new Node("zs", null);
        Node ls = new Node("ls", null);
        Node wu = new Node("wu", null);
        Node sq = new Node("sq", null);
        Node qg = new Node("qg", null);

        zs.next = ls;
        ls.next = wu;
        wu.next = sq;
        sq.next = qg;

        System.out.println(reLinked(zs).toString());

    }

    private static Node reLinked(Node head) {
        // 先创建一个反转过后的链表
        Node reLink = null;

        Node mid = head; // mid 定义的遍历结点
        while (mid != null) {
            // 保留住之前的链表
            Node next = mid.next;
            mid.next = reLink; // 头插代码
            reLink = mid; // 将反转后的头结点前移
            mid = next; // mid 指回到之前的链表中去
        }
        return reLink;
    }


}

class Node {
    String Node;
    Node next;

    public Node(String node, Node next) {
        this.Node = node;
        this.next = next;
    }

    @Override
    public String toString() {
        return "Node{" +
                "Node='" + Node + '\'' +
                ", next=" + next +
                '}';
    }
}
```

![](https://img.fengqigang.cn//img/20210428175436.png)

### 如何用单链表实现一个线性表(定义)?

```java
public class MyLinked {
   private Node head; // 这个集合类底层所维护链表的头结点
   private int size; // 用来标记这个链表/集合类存储了多少数据
}
```

### 如何用单链表实现一个线性表(添加元素)考虑可以加null?

**MyLinked.java**

```java
public class MyLinked {
    private Node head; // 这个集合类底层所维护链表的头结点
    private int size = 0; // 用来标记这个链表/集合类存储了多少数据

    public MyLinked(Node head) {
        this.head = head;
    }

    public boolean add(String str) {
        if (size == 0) {
            // 链表为空, 新添加的元素作为头结点
            head = new Node(str, null);
            size++;
            return true;
        }
        // 链表原本不空
        // 添加到尾部: 先找到尾部
        Node mid = head; // 用mid标记遍历结点，最终找到尾结点
        while (mid.next != null) {
            mid = mid.next;
        }

        mid.next = new Node(str, null);
        size++;
        return true;
    }
    
        class Node {
        String value;
        Node next;

        public Node(String value, Node next) {
            this.value = value;
            this.next = next;
        }
    }

    
}
```

**MyLinkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);
        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428191353.png)

### 如何用单链表实现一个线性表(删除元素)考虑可以删除null?

**MyLinked.java**

```java
  public boolean remove(String str) {
        // 判断链表为空
        if (size == 0) throw new RuntimeException("Link is empty");

        // 链表不为空, 删除的是 null
        if (str == null) {
            // 判断是否是头结点
            if (str == head.value) {
                // 判断头结点是不是我们要删除的元素
                head = head.next;
                size--;
                return true;
            }
            // 删除不是头结点
            Node mid = head;
            while (mid.next != null && str != mid.next.value) {
                mid = mid.next;
            }

            // 两种结果
            // 1. 没找到， mid.next == null
            // 2. 找到了

            if (mid.next == null) {
                // 没找到
                return false;
            }

            // 找到了, 要删除的是mid的next
            mid.next = mid.next.next; // 删除mid的next
            size--;
            return true;
        } else {
            // 链表不为空, 删除的不是null
            // 判断是否是头结点
            if (str.equals(head.value)) {
                // 判断头结点是不是我们要删除的元素
                head = head.next;
                size--;
                return true;
            }
            // 删除不是头结点
            Node mid = head;
            while (mid.next != null && str != mid.next.value) {
                mid = mid.next;
            }

            // 两种结果
            // 1. 没找到， mid.next == null
            // 2. 找到了

            if (mid.next == null) {
                // 没找到
                return false;
            }

            // 找到了, 要删除的是mid的next
            mid.next = mid.next.next; // 删除mid的next
            size--;
            return true;
        }
    }
```

**MyLInkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);
        myLinked.remove(null);
        myLinked.remove("zs");


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428193743.png)

### 如何用单链表实现一个线性表(包含某元素)考虑可以包含null?

**MyLinked.java**

```java
    public boolean contains(String str) {
        if (isEmpty()) throw new RuntimeException("linked is empty");

        // 查找是null元素
        if (str == null) {
            // null 在头结点
            if (str == head.value) {
                return true;
            }
            // 查找的不是头结点
            Node mid = head;
            // mid的下一个元素不是null
            // mid的下一个元素 存储的值
            while (mid.next != null) {
                mid = mid.next; // mid 向后遍历
                if (mid.value == str) {
                    return true;
                }
            }
        } else {
            // null 在头结点
            if (str.equals(head.value)) {
                return true;
            }
            // 查找的不是头结点
            Node mid = head;
            // mid的下一个元素不是null
            // mid的下一个元素 存储的值
            while (mid.next != null) {
                mid = mid.next; // mid 向后遍历
                if (str.equals(mid.value)) {
                    return true;
                }
            }
        }
        return false;
    }

```

**![efe14182c413b4fa550bba7872cd309e.png](resources/98bb7cc5b85a47f6a1c741860a7b2fde.png)**

**会产生空指针异常， 要将它们分开来**

**MyLinkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

        System.out.println("zs " + myLinked.contains("zs"));
        System.out.println("ls " + myLinked.contains("ls"));
        System.out.println("null " + myLinked.contains(null));
        System.out.println(myLinked.contains(""));


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428195716.png)

### 如何用单链表实现一个线性表(根据内容查找替换成新的内容)考虑可以改null?

**MyLinked.java**

```java
    public boolean set(String oldValue, String newValue) {
        if (isEmpty()) throw new RuntimeException("linked is empty");

        // 如果要替换的值是null
        if (oldValue == null) {
            // 要替换的值是null
            Node mid = head;
            while (mid != null && oldValue != mid.value) {
                mid = mid.next;
            }

            // 1. mid == null; 没有找到
            // 2. oldValue == mid.value; 找到了mid就是要改变的结点
            if (mid == null){
               return false;
            }

            mid.value = newValue;
            return true;
        } else {
            // 如果要替换的值不是null
            Node mid = head;
            while (mid != null && !oldValue.equals(mid.value)) {
                mid = mid.next;
            }

            // 1. mid == null; 没有找到
            // 2. oldValue == mid.value; 找到了mid就是要改变的结点
            if (mid == null){
                return false;
            }

            mid.value = newValue;
            return true;

        }
    }

```

**MyLinkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

//        System.out.println("zs " + myLinked.contains("zs"));
//        System.out.println("ls " + myLinked.contains("ls"));
//        System.out.println("null " + myLinked.contains(null));
//        System.out.println(myLinked.contains(""));
        myLinked.set("zs", "sq");
        myLinked.set(null, "xg");


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428200953.png)

### 如何用单链表实现一个线性表(根据下标查找替换成新的内容)?

**MyLinked**

```java
    public String set(int index, String newValue) {
        // 判断下标是否合法
        if (index < 0 || index >= size) throw new IllegalArgumentException("size = " + size);

        int tag = 0;
        Node mid = head;
        while (tag != index) {
            mid = mid.next;
            tag++;
        }

        // 返回被替换的值
        String value = mid.value;
        mid.value = newValue;
        return value;
    }

```

**MyLinkedPractice**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

//        System.out.println("zs " + myLinked.contains("zs"));
//        System.out.println("ls " + myLinked.contains("ls"));
//        System.out.println("null " + myLinked.contains(null));
//        System.out.println(myLinked.contains(""));
        myLinked.set("zs", "sq");
        myLinked.set(null, "xg");

        myLinked.set(0, "fengxiaonan");


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428201829.png)

### 如何用单链表实现一个线性表(返回下标中的内容)?

**MyLinked.java**

```java
    public String get(int index) {
        // 判断下标是否合法
        if (index < 0 || index >= size) throw new IllegalArgumentException("size = " + size);

        int tag = 0;
        Node mid = head;
        while (tag != index) {
            mid = mid.next;
            tag++;
        }
        // 返回被替换的值
        return mid.value;
    }

```

**MyLinkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

//        System.out.println("zs " + myLinked.contains("zs"));
//        System.out.println("ls " + myLinked.contains("ls"));
//        System.out.println("null " + myLinked.contains(null));
//        System.out.println(myLinked.contains(""));
        myLinked.set("zs", "sq");
        myLinked.set(null, "xg");

        myLinked.set(0, "fengxiaonan");
        System.out.println(myLinked.get(0));


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428202316.png)

###　如何用单链表实现一个线性表(删除某个下标的内容)?

**MyLinked.java**

```java
    public String remove(int index) {
        // 判断给的下标是否合法
        if (index < 0 || index >= size) throw new IllegalArgumentException("size = " + size);

        // 删除是头元素
        if (index == 0) {
            String oldValue = head.value;
            head = head.next;
            size--;
            return oldValue;
        }

        // 删除的不是头元素
        int tag = 1; // 位置标记
        Node mid = head;
        while (tag != index) {
            mid = mid.next;
            tag++;
        }

        // mid 删除元素前一个
        String oldValue = mid.next.value;
        // 删除
        mid.next = mid.next.next;
        size--;
        return oldValue;
    }

```

**MyLinkedPractice.java**

```java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

//        System.out.println("zs " + myLinked.contains("zs"));
//        System.out.println("ls " + myLinked.contains("ls"));
//        System.out.println("null " + myLinked.contains(null));
//        System.out.println(myLinked.contains(""));
        myLinked.set("zs", "sq");
        myLinked.set(null, "xg");

        myLinked.set(0, "fengxiaonan");
        myLinked.remove(0);
        System.out.println(myLinked.get(0));


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428203325.png)

### 如何用单链表实现一个线性表(根据下标的增加内容)?

```java
    public boolean add(int index, String str) {
        //  判断给的下标是否合法
        if (index < 0 || index > size) throw new IllegalArgumentException("size = " + size);

        // 若添加的位置是头结点
        if (index == 0) {
            head = new Node(str, head);
            size++;
            return true;
        }

        // 添加的不是头位置
        int tag = 1;
        Node mid = head;
        while (tag != index) {
            mid = mid.next;
            tag++;
        }

        mid.next = new Node(str, mid.next);
        size++;

        return true;
    }

``````java
public class MyLinkedPractice {
    public static void main(String[] args) {
        MyLinked myLinked = new MyLinked(null);
        myLinked.add("zs");
        myLinked.add("ls");
        myLinked.add(null);

//        System.out.println("zs " + myLinked.contains("zs"));
//        System.out.println("ls " + myLinked.contains("ls"));
//        System.out.println("null " + myLinked.contains(null));
//        System.out.println(myLinked.contains(""));
        myLinked.set("zs", "sq");
        myLinked.set(null, "xg");

        myLinked.set(0, "fengxiaonan");
        myLinked.remove(0);
        System.out.println(myLinked.get(0));

        myLinked.add(0, "xiaonan");


        System.out.println(myLinked.toString());
    }
}
```

![](https://img.fengqigang.cn//img/20210428204241.png)


