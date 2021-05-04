---
title: "Day28"
date: 2021-05-04T23:45:09+08:00
lastmod: 2021-05-04
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 1 10 -5 2 7 100 30 -10 -50 -25 -20 25 转换成二叉搜索树是什么样的?

左子树的所有节点的值均 **小于** 它的根节点

右子树的所有节点的值均 **大于** 它的根节点

![](https://img.fengqigang.cn//img/20210504094627.png)


### The meaning of <T extends Comparable <T>>?

This means that the type parameter **must support comparison with other instances of its own type** , via the Comparable interface.

### What is different between ![20210504171720](https://img.fengqigang.cn//img/20210504171720.png)?

![20210504171833](https://img.fengqigang.cn//img/20210504171833.png)

If you try to pass an array of unknow types of Comparable objects

one method will give you an error at compile time that this won't work, 

and the other will compile just fine, but you'll receive an error when you try to run it.

Ideally, you'will want to know about type safety issues as soon as possible, so the method that gives you a compile-time error is preferable.

### 若以链表来实现一个二叉搜索树, 如何定义一个BSTree?

```java
public class MyBSTree{
    private Node root; // 定义根结点
    private int size; // 定义树的结点个数
}
```

**需要节点与节点之间进行比较**

```java
public class MyBSTree<T extends Comparable<T>> {
    private Node root; // 定义根结点
    private int size; // 定义树的结点个数
}
```


### 若以链表来实现一个二叉搜索树, 如何定义一个BSTree的结点?

```java
public class MyBSTree<T extends Comparable<T>> {
    private Node root; // 定义根结点
    private int size; // 定义树的结点个数

    class Node {
        T value;
        Node left;
        Node right;

        public Node(T value, Node left, Node right) {
            this.value = value;
            this.left = left;
            this.right = right;
        }
    }
}	
```

### 若以链表来实现一个二叉搜索树, 如何实现加入一个新结点(add)的功能?

```java
    public boolean add(T t) {
        // 1. 不能加null结点
        if (t == null) throw new IllegalArgumentException("null is not allow to add");

        // 2.1 添加的不是null, 当前树为空
        if (size == 0) {
            root = new Node(t, null, null);
            size++;
            return true;
        } else {
            // 2.2 添加的不是null, 当前的树不为空
            // 找到要添加的位置(查找过程)

            // 从root向下找
            Node mid = root;
            Node midF = null;
            int com;

            // 一直向下找, 在null处结束
            //  同时记录其父结点
            while (mid != null) {
                // 判断左右 compareTo
                com = t.compareTo(mid.value);

                // t > mid, 向右走
                if (com > 0) {
                    midF = mid;
                    mid = mid.right;
                } else if (com < 0) {
                    // t < mid, 向左走
                    midF = mid;
                    mid = mid.left;
                } else {
                    // t == mid, 不添加
                    return false;
                }
            }

            // mid == null, 已经找到了要添加结点的位置
            // 通过 com 的大小， 判断要添加的左右位置(与其midF比较)
            if (t.compareTo(midF.value) > 0) {
                // 大于0, 在右边
                midF.right = new Node(t, null, null);
                size++;
                return true;
            } else {
                //  小于0, 在左边
                midF.left = new Node(t, null, null);
                size++;
                return true;
            }
        }
    }
```


### 若以链表来实现一个二叉搜索树, 如何实现删除一个结点(remove)的功能?(不用递归)

```java
    public boolean remove(T t) {
        // 确定删除的内容不能是null
        if (t == null) throw new IllegalArgumentException("param is not null");

        // 从根结点出发
        Node mid = root;
        int com;
        // 用midF 来删除
        Node midF = null;

        while (mid != null) {
            com = t.compareTo(mid.value);
            // 当前位置
            if (com == 0) {
                // 找到了, 跳出来
                break;
            } else if (com > 0) {
                // 向右
                midF = mid;
                mid = mid.right;
            } else {
                // 向左
                midF = mid;
                mid = mid.left;
            }
        }

        // 跳出
        // 1. mid == null
        if (mid == null) {
            return false;
        }

        // 2. com == 0
        // 2.1 单分支
        // 2.2 叶子结点
        // 2.3 双分支
        if (mid.left != null && mid.right != null) {
            // 找到右子树中最小的节点, 一直往左找
            Node min = mid.right;
            Node minF = mid;

            while (min.left != null) {
                minF = min;
                min = min.left;
            }

            // 将 最小的节点与 mid 交换
            mid.value = min.value;

            // 将双分支节点变成叶子结点
            mid = min;
            // 切换父结点
            midF = minF;
        }

        // 只剩下叶子结点与单分支结点
        // 找到不是null的分支
        // ch 是要保留的分支
        Node ch = (mid.left == null ? mid.right : mid.left);

        // 删除的根结点，并且根节点是单分支的结点
        if (midF == null) {
            root = ch;
            size--;
            return true;
        }


        // 上移
        if (mid == midF.left) {
            // 左边相同
            midF.left = ch;
            size--;
            return true;
        } else {
            // 右边相同, 或为null
            midF.right = ch;
            size--;
            return true;
        }
    }
```


### 若以链表来实现一个二叉搜索树, 如何实现查找树中是否包含某一结点?

```java
    public boolean contains(T t) {
        // 不能与null比较
        if (t == null) throw new IllegalArgumentException("param is not equal null");

        // 从 root 开始找
        Node mid = root;
        while (mid != null) {
            if (t.compareTo(mid.value) > 0) {
                // 向右
                mid = mid.right;
            } else if (t.compareTo(mid.value) < 0) {
                // 向左
                mid = mid.left;
            } else {
                // 相等
                // 找到了 0
                return true;
            }
        }
        // 没找到
        return false;
    }
```

### 如何实现后序遍历?

`左 右 根`

要有一个stack， 和一个list

根要最后输出

list 采用头插法方式， 弹出头结点后, 应该先插入左边还是右边?

因为 `左 右 根`

要先弹出右子树的元素, 所以先压入 left 子树， 再压入 right 子树

```java
    public List<T> postOrder() {
        // 保存遍历的结果
        ArrayList<T> ts = new ArrayList<>();

        Stack<Node> stack = new Stack<>();

        // 根节点
        stack.push(root);
        // 判断条件是栈不为空
        while (!stack.isEmpty()) {
            // 弹出栈顶元素
            Node pop = stack.pop();

            // 先压左子树, 不为null时
            if (pop.left != null) {
                stack.push(pop.left);
            }

            // 后压右子树, 不为null时
            if (pop.right != null) {
                stack.push(pop.right);
            }

            // 将弹出的元素放入list中(头插法)
            ts.add(0, pop.value);
        }

        return ts;
    }
```




### 如何实现前序遍历?


根 左 右

需要一个stack， 一个list

root 先压入栈中， 弹出

因为是 `根 左 右`, 先输出左，后右

先压入右子树， 后压入左子树

判断条件是栈不为空

```java
    public List<T> preOrder() {
        // 创建一个list保存数据
        ArrayList<T> ts = new ArrayList<>();

        // 创建一个stack
        Stack<Node> stack = new Stack<>();

        // 压入根节点
        stack.push(root);
        while (!stack.isEmpty()) {
            // 栈顶元素弹出
            Node pop = stack.pop();

            // 先压入右子树, 非null
            if (pop.right != null) {
                stack.push(pop.right);
            }

            // 后压入左子树, 非null
            if (pop.left != null) {
                stack.push(pop.left);
            }

            // 尾插法
            ts.add(pop.value);

        }
        return ts;
    }
```

### 如何实现中序遍历?

需要一个stack  和一个 list

左 根 右

因为根是放在中间， 所以先将根标记起来

向左遍历, 全部压入栈中(标记结点也要记录)，直到遇到null

弹出栈顶元素，标记向右移动

```java
    public List<T> inOrder() {
        // 保存要输出的list
        ArrayList<T> ts = new ArrayList<>();

        // 创建一个链表
        Stack<Node> stack = new Stack<>();

        Node mid = root;

        while (mid != null || !stack.isEmpty()) {
            while (mid != null) {
                // 向左走，压入stack中
                stack.push(mid);
                mid = mid.left;
            }

            // mid ==null
            // 栈顶,出栈
            // mid 向右移
            Node pop = stack.pop();
            ts.add(pop.value);
            mid = pop.right;
        }
        return ts;
    }
```

### 如何实现层级遍历(广度优先搜索)?

**队列**

```java
    public List<T> levOrder() {
        // 用队列来输出
        ArrayDeque<Node> deque = new ArrayDeque<>();

        // list
        ArrayList<T> list = new ArrayList<>();

        // root 入队
       deque.add(root);

       while(!deque.isEmpty()){
          // 队头元素出队
           Node pop = deque.pop();

           // 左子树入队, 非null
           if(pop.left != null){
              deque.add(pop.left);
           }
           // 右子树入队, 非null
           if(pop.right != null){
              deque.add(pop.right);
           }

           // 出队元素入list
           list.add(pop.value);
       }
       return list;
    }
```

### 如何实现深度优先遍历?

需要一个 **stack**  和 一个 **list**

将 **root** 压入栈中, 不断的压入其左边的元素, 直到左边的元素为null

压入其右边的元素, 再压入其左边的元素，直到左右边的元素都为null时弹出，当前的元素

加入到list中


```java
    public List<T> depOrder() {
        // 返回的list
        ArrayList<T> list = new ArrayList<>();

        // 创建一个stack
        Stack<Node> stack = new Stack<>();

        // root 入栈
        stack.push(root);

        while (!stack.isEmpty()) {
            Node pop = stack.pop();
            if (pop.left != null) {
                stack.push(pop.left);
            }
            if (pop.right != null) {
                stack.push(pop.right);
            }
            list.add(pop.value);
        }
        return list;
    }
```

### 如何实现中序与后序号建立树?

先获取根节点在中序的位置

根据后序来获取

T value = postOrder.get(postOrder.size() - 1);

int index = inOrder.indexOf(value);

**左子树** 的中序(切割): 0 ~ index - 1

**左子树** 的后序(切割): 0 ~ index - 1

**右子树** 的中序(切割): index + 1 ~ size - 1

**右子树** 的后序(切割): index ~ size - 2

![20210504224652](https://img.fengqigang.cn//img/20210504224652.png)


![20210504224758](https://img.fengqigang.cn//img/20210504224758.png)





```java
    public void buildTreeByInAndPostOrder(List<T> inOrder, List<T> postOrder) {
        // 调用私有方法建立树
        root = buildTreeByInAndPostOrder2(inOrder, postOrder);
        // 定义树的长度
        size = inOrder.size();
    }

    private Node buildTreeByInAndPostOrder2(List<T> inOrder, List<T> postOrder) {
        // 退出位置
        if (inOrder.size() == 0) return null;
        if (inOrder.size() == 1) return new Node(inOrder.get(0), null, null);

        // 找到根结点的值(后序中的最后一个)
        // get (int index)
        T value = postOrder.get(postOrder.size() - 1);
        // 获取根结点的位置(在中序中获得)
        int index = inOrder.indexOf(value);

        // 划分左子树
        List<T> leftInOrder = inOrder.subList(0, index);// 左闭右开
        List<T> leftPostOrder = postOrder.subList(0, index);

        // 划分右子树
        List<T> rightInOrder = inOrder.subList(index + 1, inOrder.size());
        List<T> rightPostOrder = postOrder.subList(index, inOrder.size() - 1);

        // 构建根结点
        Node node = new Node(value, null, null);

        // 获得左子树
        node.left = buildTreeByInAndPostOrder2(leftInOrder, leftPostOrder);
        // 获得右子树
        node.left = buildTreeByInAndPostOrder2(rightInOrder, rightPostOrder);

        return node;
    }
```


### 如何实现中序与前序号建立树?

先获取根节点在中序的位置

根据后序来获取

T value = postOrder.get(postOrder.size() - 1);

int index = inOrder.indexOf(value);

**左子树** 的中序(切割): 0 ~ index - 1

**左子树** 的前序(切割): 1 ~ index - 1

**右子树** 的中序(切割): index + 1 ~ size - 1

**右子树** 的前序(切割): index + 1 ~ size - 1

```java
    public void buildTreeByInAndPreOrder(List<T> inOrder, List<T> preOrder) {
        // 调用私有方法建树
        root = buildTreeByInAndPreOrder2(inOrder, preOrder);
        size = inOrder.size();
    }

    private Node buildTreeByInAndPreOrder2(List<T> inOrder, List<T> preOrder) {
        // 退出位置
        if (inOrder.size() == 0) return null;
        if (inOrder.size() == 1) return new Node(inOrder.get(0), null, null);

        // 找到根结点的值(先序中的第一个元素)
        T value = preOrder.get(0);
        // 获取根结点在 inOrder的位置
        int index = inOrder.indexOf(value);

        // 划分左子树
        List<T> leftInOrder = inOrder.subList(0, index);
        List<T> leftPreOrder = preOrder.subList(1, index + 1);

        // 划分右子树
        List<T> rightInorder = inOrder.subList(index + 1, inOrder.size());
        List<T> rightPreorder = preOrder.subList(index + 1, inOrder.size());

        // 构建递归根节点
        final Node node = new Node(value, null, null);

        // 获得左子树
        node.left = buildTreeByInAndPostOrder2(leftInOrder, leftPreOrder);

        // 获得右子树
        node.right = buildTreeByInAndPostOrder2(rightInorder, rightPreorder);

        return node;
    }
```




