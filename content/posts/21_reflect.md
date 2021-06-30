---
title: "21_reflect"
date: 2021-06-30T09:32:16+08:00
lastmod: 2021-06-30
author: "xiaonan"
math:
 enable: true

tags: [java]
categories: [王道]
---

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

### 如何利用反射，获取成员方法参数类型?

**getParameterTypes**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        // 获取方法的参数类型
        Method[] declaredMethods = personCls.getDeclaredMethods();
        Class[] parameterTypes = declaredMethods[1].getParameterTypes();
        for (Class param : parameterTypes) {
            System.out.println(param.getSimpleName());
        }
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

```

![20210427140654](https://img.fengqigang.cn//img/20210427140654.png)

### 如何利用反射，获取父类?

**getSuperclass()**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        // 获取方法的父类
        Class superclass = personCls.getSuperclass();
        System.out.println(superclass.getSimpleName());
    }
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

![20210427140914](https://img.fengqigang.cn//img/20210427140914.png)

### 如何通过反射，获取接口?

**getInterfaces**

**Demo2.java**

```java
public class Demo2 {
    public static void main(String[] args) throws ClassNotFoundException {
        Class personCls = Class.forName("Demo.Person");

        // 获取接口
        Class[] interfaces = personCls.getInterfaces();
        for(Class i : interfaces){
            System.out.println(i.getSimpleName());
        }
    }
}
```

**Person.java**

```java
public class Person implements Comparable{
    public int money;
    public int age;
    public String name;

    @Override
    public int compareTo(Object o) {
        return 0;
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

![20210427141257](https://img.fengqigang.cn//img/20210427141257.png)

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




