---
title: "Day23"
date: 2021-04-26T23:39:19+08:00
lastmod: 2021-04-26
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

### 类加载的细分?

类加载通过 **加载**, **连接**， **初始化** 三步来实现

![](https://img.fengqigang.cn//img/20210426093507.png)

### 类加载中的加载是如何执行的？

通过类加载器获得二进制字节流

在内存中生成一个代表这个类的 java.lang Class对象，作为方法区这个类的各种数据的访问入口

### 类加载中的连接是如何执行的?

验证：确保被加载类的正确性正确性的校验

cafe babe:magic number起校验作用的

准备：负责为类的静态成员分配内存并设置默认初始化值

解析：将类中的符号引用 (跟编译原理相关) 潜替换为直接引用(内存地址)

### 类加载中的初始化是如何执行的？

给静态成员变量赋初值，执行静态代码块内容

### 类加载时机有哪些?

创建类的实例 (首次创建该类)

对象访问类的静态变量（首次)

调用类的静态方法（首次)

使用反射方式来强制创建某个类或接口对应的 **java.lang.Class** 对象

加载某个类的子类，会先触发父类的加载

直接使用 **java. exe** 命令来运行某个主类，也就是执行了某个类的main方法

### 类加载中有哪些加载器?

**Bootstrap ClassLoader**

根类加载器负责Java运行时核心类的加载，JDK中JRE的目录下 rt jar

**Extension ClassLoader**

扩展类加载器负责JRE的扩展目录中jar包的加载，在JDK中JRE的目录下ext日录

**Sysetm ClassLoader**

系统类加载器/应用加载器负责加载自己定义的Java类

### **java** 在计算机中有哪几种阶段?

![](https://img.fengqigang.cn//img/20210426094815.png)

1.  源文件阶段
2.  Class 类对象阶段(通过类加载器 ClassLoader 加载)
3.  运行时阶段

### 什么是反射?

获取类运行时信息的一种技术，这种技术叫做反射技术

### 获取字节码文件有哪些方式?

1.  Class.forName("全限定类名")
    
2.  类名.class
    
3.  对象.getClass（）
    

![](https://img.fengqigang.cn//img/20210426100051.png)

### 如何用 **Class.forName("全限定类名")** 获取字节码文件？

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        // 第一种 Class.forName（"全类名"）
        Class personCls = Class.forName("idea.Person");
        System.out.println(personCls);
    }
}
```

![](https://img.fengqigang.cn//img/20210426165518.png)

### 如何用 **类名.class** 获取字节码文件？

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        // 第一种 Class.forName（"全类名"）
        Class personCls = Class.forName("idea.Person");
        System.out.println(personCls);

        // 类名.class
        Class personCls2 = Person.class;
        System.out.println(personCls2);
    }
}
```

![](https://img.fengqigang.cn//img/20210426165909.png)

### 如何用 **对象.getClass（）** 获取字节码文件？

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        // 第一种 Class.forName（"全类名"）
        Class personCls = Class.forName("idea.Person");
        System.out.println(personCls);

        // 类名.class
        Class personCls2 = Person.class;
        System.out.println(personCls2);
        
        // 第三种，对象.getClass()
        Person person = new Person();
        Class personCls3 = person.getClass();

        System.out.println(personCls3);
    }
}
```

![](https://img.fengqigang.cn//img/20210426185935.png)

### ![](https://img.fengqigang.cn//img/20210426100159.png) 其结果是什么?

相同

### ![](https://img.fengqigang.cn//img/20210426190203.png)，![](https://img.fengqigang.cn//img/20210426190242.png) 会发生什么?

第一种会触发类加载， 第二种不会

### 获取所有构造方法?

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("idea.Person");

        Constructor[] constructors = personCls.getConstructors();
        for (Constructor constructor : constructors) {
            System.out.println(constructor);
        }
    }
}
```

![](https://img.fengqigang.cn//img/20210426191044.png)

### 如何获取所有声明的构造方法?

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("idea.Person");

        // 获取所有的构造方法
        System.out.println("获取所有的构造方法-----");
        Constructor[] declaredConstructors = personCls.getDeclaredConstructors();
        for (Constructor constructor : declaredConstructors) {
            System.out.println(constructor);
        }
    }
}
```

### 如何获取单个 public 的构造方法?

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException {
        Class personCls = Class.forName("idea.Person");

        // 获取单个public的构造方法
        System.out.println("获取单个的构造方法-----");
        Constructor constructor = personCls.getConstructor(int.class);
        System.out.println(constructor);

    }
}
```

![](https://img.fengqigang.cn//img/20210426191637.png)

### 如何获取单个的构造方法?

```java
public class TestDemo {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException {
        Class personCls = Class.forName("idea.Person");

        // 获取单个public的构造方法
        System.out.println("获取单个的构造方法-----");
        Constructor declaredConstructor = personCls.getDeclaredConstructor(int.class);
        System.out.println(declaredConstructor);

    }
}
```

![](https://img.fengqigang.cn//img/20210426191820.png)



### ![20210426220818](https://img.fengqigang.cn//img/20210426220818.png)对于这种非public 的构造方法如何进行实例化?

**暴力破解** 

setAccessible(true) 如果为 true, 将忽略

![](https://img.fengqigang.cn//img/20210426111001.png)


**Person.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("利用非 public 构造方法实例化");
        Constructor declaredConstructor = personCls.getDeclaredConstructor(int.class);
        declaredConstructor.setAccessible(true);
        Person person = (Person) declaredConstructor.newInstance(10);
        System.out.println(person);
    }
}
```


**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("利用非 public 构造方法实例化");
        Constructor declaredConstructor = personCls.getDeclaredConstructor(int.class);
        declaredConstructor.setAccessible(true);
        Person person = (Person) declaredConstructor.newInstance(10);
        System.out.println(person);
    }
}
```

### 如何用反射获取所有 public 修饰的成员变量?

**getFields()**


**Demo2**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("获取所有 public 的成员 变量--- ");
        Field[] fields = personCls.getFields();
        for(Field field : fields){
            System.out.println(field);
        }
    }
}
```

**Person**

```java
public class Person {
    public int age;
    public String name;

    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age){
       this.age = age;
    }
}
```

![20210426221815](https://img.fengqigang.cn//img/20210426221815.png)

### 如何用反射获取所有声明成员变量?

**getDeclaredField**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("获取所有 public 的成员 变量--- ");
        Field[] fields = personCls.getDeclaredFields();
        for (Field field : fields) {
            System.out.println(field);
        }
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age) {
        this.age = age;
    }
}
```

![20210426222210](https://img.fengqigang.cn//img/20210426222210.png)


### 如何利用反射 给成员变量 设置值?

**getDeclaredField**

**getDeclaredFields**

set

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchFieldException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("给成员变量设置值 与 获取值----");
        Constructor declaredConstructor = personCls.getDeclaredConstructor();
        Person o = (Person) declaredConstructor.newInstance();
        Field nameField = personCls.getDeclaredField("name");
        nameField.set(o, "王五");
        System.out.println(o.toString());
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426223634](https://img.fengqigang.cn//img/20210426223634.png)


### 如何利用反射 获取成员变量 的值?

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchFieldException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("给成员变量设置值 与 获取值----");
        Constructor declaredConstructor = personCls.getDeclaredConstructor();
        Person o = (Person) declaredConstructor.newInstance();
        Field nameField = personCls.getDeclaredField("name");
        nameField.set(o, "王五");
        System.out.println(o.toString());
        String name = (String) nameField.get(o);
        System.out.println("name " + name);
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426224404](https://img.fengqigang.cn//img/20210426224404.png)

### 如何利用反射，获取成员所有方法(包括父类的)?

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchFieldException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("获取所有的public的成员方法----");
        Method[] methods = personCls.getMethods();
        for (Method method : methods) {
            System.out.println(method);
        }
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age) {
        this.age = age;
    }

    public void eat (){
        System.out.println("eat food");
    }

    private void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426224827](https://img.fengqigang.cn//img/20210426224827.png)


![](https://img.fengqigang.cn//img/20210426113002.png)

![](https://img.fengqigang.cn//img/20210426113405.png)

### 如何获取获取单个方法?

**getDeclaredMehtod**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchFieldException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("如何获取单个的方法----");
        Method eatMethod2 = personCls.getDeclaredMethod("eat", String.class);
        System.out.println(eatMethod2);
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    private Person(int age) {
        this.age = age;
    }

    public void eat (){
        System.out.println("eat food");
    }

    private void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426225311](https://img.fengqigang.cn//img/20210426225311.png)

### 如何使用反射, 并使用成员方法?

**method.invoke(对象, args)**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, InvocationTargetException, InstantiationException, IllegalAccessException, NoSuchFieldException {
        Class personCls = Class.forName("Demo.Person");

        System.out.println("如何获取单个的方法----");
        Method eatMethod2 = personCls.getDeclaredMethod("eat", String.class);
        System.out.println(eatMethod2);

        // 获取构造方法， 再实例化
        Constructor declaredConstructor = personCls.getDeclaredConstructor();
        declaredConstructor.setAccessible(true);
        Object o = declaredConstructor.newInstance();
        eatMethod2.invoke(o, "123");
    }
}
```

**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426230947](https://img.fengqigang.cn//img/20210426230947.png)


### 如何通过反射获取 全类名?

**getName()**


**Person**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

**Demo2**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        String name = personCls.getName();
        System.out.println(name);
    }
}
```


### 如何通过反射获取简单的类名?

**getSimpleName()**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        String name = personCls.getSimpleName();
        System.out.println(name);
    }
}
```


**Person.java**

```java
public class Person {
    int money;
    public int age;
    public String name;


    static {
        System.out.println("init Person");
    }

    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426231543](https://img.fengqigang.cn//img/20210426231543.png)

### 如何利用反射获取成员变量的权限修饰符?

**getModifiers()**

**Modifier**


**Person.java**

```java
public class Person {
    public int money;
    public int age;
    public String name;


    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```


**Demo2**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");


        Field[] declaredFields = personCls.getDeclaredFields();
        System.out.println(declaredFields.length);
        System.out.println(declaredFields[0].getName());

        int modifiers = declaredFields[0].getModifiers();
        System.out.println(modifiers);

        String s = Modifier.toString(modifiers);
        System.out.println(s);
    }
}
```

![20210426232118](https://img.fengqigang.cn//img/20210426232118.png)

### 如何通过反射，获取成员变量的类型?

**getType()**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        Field[] declaredFields = personCls.getDeclaredFields();
        System.out.println(declaredFields.length);
        System.out.println(declaredFields[0].getType().getName());

    }

```

```java
public class Person {
    public int money;
    public int age;
    public String name;


    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426232346](https://img.fengqigang.cn//img/20210426232346.png)


### 如何通过反射，获取成员方法的返回值类型?

**getReturnType()**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        // 获取方法的返回值类型
        Method[] declaredMethods = personCls.getDeclaredMethods();
        System.out.println(declaredMethods.length);
        System.out.println(declaredMethods[0]);

        Class returnType = declaredMethods[0].getReturnType();

        // 获取方法的返回值类型
        System.out.println(returnType);
        System.out.println(returnType.getSimpleName());
    }
}
```

**Person.java**

```java
public class Person {
    public int money;
    public int age;
    public String name;


    public Person() {
    }

    public Person(int age) {
        this.age = age;
    }

    private void eat (){
        System.out.println("eat food");
    }

    public void eat(String s){
        System.out.println("eat" + s);
    }

    @Override
    public String toString() {
        return "Person{" +
                "money=" + money +
                ", age=" + age +
                ", name='" + name + '\'' +
                '}';
    }
}
```

![20210426233113](https://img.fengqigang.cn//img/20210426233113.png)

### 获取成员方法参数?

![](https://img.fengqigang.cn//img/20210426115355.png)

### 获取父类?

![](https://img.fengqigang.cn//img/20210426115654.png)

### 获取接口?

![](https://img.fengqigang.cn//img/20210426115721.png)

### 如何反编译成员变量?

![](https://img.fengqigang.cn//img/20210426143229.png)

### 如何反编译成员方法?

![](https://img.fengqigang.cn//img/20210426144450.png)

### 反射一般有什么应用场景?

用于框架中

![](https://img.fengqigang.cn//img/20210426144907.png)

**Object–relational mapping**

### 通过反射调用默认无参的构造方法?

![](https://img.fengqigang.cn//img/20210426145347.png)

直接通过 NewInstalnce 可以要通过，默认的方法

### 什么是注释?

1.  单行注释: //
2.  多行注释: /\* */
3.  文档注释: /\*\* */

**注释是给程序员看的，不参与编译**

### 什么是注解？

与 **接口**，**类** 是同一级别的

理解为一个标签

**参与编译**

**语法**

```java
权限修饰符 @interface 注解名称 {
}
```

### 什么是注解体?

```java
权限修饰符 @interface 注解名称 {
    // 注解体
    属性类型 属性名称();
}
```

![](https://img.fengqigang.cn//img/20210426151654.png)

注意(属性类型):

- 基本数据类型
- String 类型
- Class 类型
- 枚举类型(Enum)
- 注解类型
- 以及以上类型的数组

![](https://img.fengqigang.cn//img/20210426151934.png)

![](https://img.fengqigang.cn//img/20210426152003.png)

### 如何使用注解?

![](https://img.fengqigang.cn//img/20210426154322.png)

![](https://img.fengqigang.cn//img/20210426154523.png)

![](https://img.fengqigang.cn//img/20210426154747.png)

![](https://img.fengqigang.cn//img/20210426163737.png)

### 使用注解创建学生对象?

![](https://img.fengqigang.cn//img/20210426155245.png)

![](https://img.fengqigang.cn//img/20210426155345.png)

### 什么是注解处理器？

![](https://img.fengqigang.cn//img/20210426160340.png)

**用注解来判断**

isAnnotationPresent()

![](https://img.fengqigang.cn//img/20210426161044.png)

![](https://img.fengqigang.cn//img/20210426161546.png)

**忽略语法检查**

**DeclaredField**

### 什么是元注解?

**元注解**:

描述注解的注解

**常用的元注解**

- @Retention 元注解
    - RetentionPolicy.RUNTIME
    - RetentionPolicy.CLASS
    - RetentionPolicy.SOURCE

![](https://img.fengqigang.cn//img/20210426163257.png)

![](https://img.fengqigang.cn//img/20210426163308.png)

### 什么是元数据?

修饰数据的数据

### 注解的3种保留级别?

和 **java** 程序一致，注解有3种保留级别:

**SOURCE**:

注解将被编译器丢弃 (class 文件中没有)

**CLASS**:

注解在 **class** 文件中可用，但会被 **JVM** 丢弃(内存没有)

**RUNTIME**:

**JVM**在运行时，也会保留注解信息

### 连接数据库？

![](https://img.fengqigang.cn//img/20210426164325.png)

###　注解与配置文件的比较

![](https://img.fengqigang.cn//img/20210426164444.png)

### 什么是显式的内存管理?

由程序员去管理内存

**malloc()**

**free()**

**可能出现的问题**

- 野指针
- 内存泄漏

### 隐式的内存管理

![](https://img.fengqigang.cn//img/20210426171741.png)

### 谁是垃圾?

1.  引用计数算法

![](https://img.fengqigang.cn//img/20210426172117.png)

2.  根搜索算法

![](https://img.fengqigang.cn//img/20210426172229.png)

![](https://img.fengqigang.cn//img/20210426172507.png)

### 如何回收垃圾?

1.  标记清除算法

![](https://img.fengqigang.cn//img/20210426172856.png)

它会产生垃圾碎片，如果要创建一个数组，但是无法创建一个连续的存储空间

2.  标记复制算法

![](https://img.fengqigang.cn//img/20210426173107.png)

![](https://img.fengqigang.cn//img/20210426173229.png)

1.  一次性回收大片的连续空间
    
2.  不会产生内存碎片
    
3.  如果说有少量存活对象，复制起来很快，适用于少量对象存活的情况
    
4.  但是，内存利用率低
    
5.  如果有大量对象存活，就需要复制大量对象，效率就低了
    
6.  标记整理算法(Mark Compact)
    

![](https://img.fengqigang.cn//img/20210426173626.png)

4.  分带收集算法

![](https://img.fengqigang.cn//img/20210426173839.png)

**死的快的用** 标记复制算法

![](https://img.fengqigang.cn//img/20210426174252.png)

### 何时回收垃圾？

![](https://img.fengqigang.cn//img/20210426174452.png)

idle 休眠

heap space 堆内存

**System.gc()**

### GC 相关概念?

![](https://img.fengqigang.cn//img/20210426174617.png)

![](https://img.fengqigang.cn//img/20210426174924.png)

![](https://img.fengqigang.cn//img/20210426174950.png)

### 内存泄露与内存溢出的关系 ?

![](https://img.fengqigang.cn//img/20210426175328.png)

![](https://img.fengqigang.cn//img/20210426175256.png)


