---
title: java面试题
date: 2021-12-04 17:03:35
tags: [java, 面试]
categories: [面试]
---



## java基础数据类型 (java primitive data type)

* 整型：byte(1 byte),short(2 byte),int(4 byte),long(8 byte)
* 浮点型：float(4 byte),double(8 byte)
* 字符型：char(2 byte)
* 布尔类型：boolean(1 byte)

## final关键字

final关键字可修饰类，变量和方法

* final修饰变量，表示该变量只能被赋值一次，之后不能重新赋值。如final修饰引用类型的变量，虽不能重新赋值，但可以修改内部状态
* final修饰类，表示该类无法被继承，或该类是不可变的，如String
* final修饰方法，表示该方法不能被重写（overridden）

### 引用

* [final Keyword in Java](https://www.geeksforgeeks.org/final-keyword-in-java/)

## static关键字

static关键字可修饰变量，方法，代码块和嵌套类。被static修饰，表示该变量/方法/代码块是隶属于类，而不是该类的某个对象。可直接通过[Class].[变量/方法]来调用

* static修饰变量，表示该变量是静态的，只会在类加载的时候分配内存，该变量是该类的所有对象共享的。可通过[Class].[Variable]来使用
* static修饰方法，表示该方法为静态方法，可以直接使用[Class].[Method]来使用，无需实例化。静态方法在编译器进行解析，而方法重写发生在运行期，故静态方法不能被重写
  - 抽象方法不能是静态的
  - 静态方法不能使用this或super关键字
  - 静态方法只能访问静态成员变量或静态成员方法
* static修饰代码块。可以在类中声明静态代码块，static {}, 表示该代码块在类加载期间运行。适用于以下场景：
  - 静态变量的初始化除了赋值还有其它逻辑
  - 静态变量的初始化可能有错误，需要捕获异常
* static修饰内部类，内部类表示我们可以在一个类内部声明一个类，使得代码更有组织和易读。内部类如被static修饰，表示该类为静态嵌套类，只能访问外部类中的静态方法和静态变量。如未被static修饰，表示该类为内部类，可以访问外部类中的成员方法和成员变量。

### 引用

* [A Guide to the Static Keyword in Java](https://www.baeldung.com/java-static)

## ==和equals()的区别

* “==” 主要比较两个对象在内存中的地址是否相等。如是基础数据类型，则是判断两变量的值是否相等。
* “equals()” 未被重写时，该方法与"`==`"作用相同。如两个对象的内容相同，成员变量的值相等，因是两个对象，地址不相同，如使用未重写的 “equals()” 或 "`==`" 判断，则两对象并不相等。我们可以通过重写 “equals()” ，改为判断两个对象的内容是否相同，来实现我们的需求。 

## java异常和错误的区别，如何处理异常

在java中,`Exception`和`Error`都继承自`Throwable`类。该类直接继承自`Object`.

* `Error`表示出现了非常严重的错误，不能通过程序去处理，而应该检查程序架构的问题。如`StackOverflowError`、`OutOfMemoryError`等。
* `Exception`作为程序出现异常的条件。可分为非受检型异常和受检型异常。`Exception`中除`RuntimeException`外，其它类及其子类均为受检型异常。受检型异常发生在编译器，必须通过程序显式捕获处理，否则不能通过编译。如：`IOException`， `FileNotFoundException`.`RuntimeException`类及其子类为非受检型异常，无需通过程序显式捕获处理。如 `NullPointerException`等。

`Error`和`RuntimeException`无需通过程序显式处理，而应该通过检查修改程序来解决。受检型异常需要通过程序显式捕获处理。

异常处理代码示例：

```

try {
    // 可能会发生异常的代码块
} 
catch (IOException e) {
    // 异常发生时，执行的代码
}

```

## io流的类层级结构

### io流的分类

* 按照流向划分，分为输入流和输出流
* 按照操作单元划分，分为字符流和字节流
* 按照流的角色划分，分为节点流和处理流

java中所有io流都是以下4个抽象类派生出来的：

* InputStream/Reader：所有输入流的基类，前者是字节输入流，后者是字符输入流
* OutputStream/Writer: 所有输出流的基类，前者是字符输出流，后者是字符输出流

![Files IO](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112041706517.jpeg)

### 引用

* [Java 中 IO 流](https://snailclimb.gitee.io/javaguide-interview/#/./docs/b-1%E9%9D%A2%E8%AF%95%E9%A2%98%E6%80%BB%E7%BB%93-Java%E5%9F%BA%E7%A1%80?id=_2132-java-%e4%b8%ad-io-%e6%b5%81)
* [Java - Files and I/O](https://www.tutorialspoint.com/java/java_files_io.htm)

## java泛型 （java generics）

> 泛型程序设计意味着编写的代码可以对不同类型的对象重用。 —— 《java核心技术 卷一》第11版
>
> **Generics** are a facility of [generic programming](https://en.wikipedia.org/wiki/Generic_programming) that were added to the [Java programming language](https://en.wikipedia.org/wiki/Java_(programming_language)) in 2004 within version [J2SE](https://en.wikipedia.org/wiki/Java_Platform,_Standard_Edition) 5.0. They were designed to extend Java's [type system](https://en.wikipedia.org/wiki/Type_system) to allow "a type or method to operate on objects of various types while providing compile-time type safety"  —— java官方文档

先看下如下代码：

```java
public static void main(String[] args) {
    ArrayList goods = new ArrayList();
    goods.add(15.2);
    goods.add(16.3);
    printArray(goods);
}

private static void printArray(ArrayList goods) {
    for (int i = 0; i < goods.size(); i++) {
        System.out.println((int)goods.get(i));
    }
}
```

`ArrayList`内部是使用 `Object` 来存储的，故我们可以添加任何引用类型的值。不过会出现这样的问题：我们在其中添加的是浮点类型的值，而在取值时，转成了 `Integer`。而这样在编译期是允许的。运行上述代码，会出现以下错误：

```
class java.lang.Double cannot be cast to class java.lang.Integer
```

为了避免类型转换的问题，我们需要为每一种数据类型，都添加该数据结构的实现。如 `StringArrayList`, `DoubleArrayList`,`IntegerArrayList`。这样使得数据结构实现很繁琐，不通用。于是在 `java 5.0` 中引入了泛型：来看使用泛型后的代码：

```java
public static void main(String[] args) {
    ArrayList<Integer> goods = new ArrayList<Integer>();
    goods.add(15.2);
    goods.add(16.3);
    printArray(goods);
}

private static void printArray(ArrayList goods) {
    for (int i = 0; i < goods.size(); i++) {
    	System.out.println((int)goods.get(i));
    }
}
```

无需运行，`idea` 就检查出了问题：

![image-20211206101505584](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112061015791.png)

我们声明了一个 `Integer` 类型的 `ArrayList`， 在其中添加 `Double` 类型的值时，就会报错。

泛型使得我们可以编写通用的方法和类型实现，在编译期就能检查到问题，借助编译器的静态代码检查，无需运行即能检查到类型相关问题，降低了代码运行时出问题的风险。

### 引用

*  [Generics in Java](https://en.wikipedia.org/wiki/Generics_in_Java#cite_note-1)
* [Generics](https://docs.oracle.com/javase/tutorial/java/generics/index.html)

## java多态 (polymorphism)

> 多态指的是同一个行为具有多个不同表现形式或形态的能力。 
>
> 多态是指，针对某个类型的方法调用，其真正执行的方法取决于运行时期实际执行的方法。

多态是面向对象中非常重要的一个概念。可分为编译时多态和运行时多态。前者基于方法重载实现，后者基于方法重写实现。首先看一个例子：

```
public class Shape {

    // 正方形面积
    public void area(int n) {
        System.out.println("正方形的面积为：" + n * n);
    }

    // 三角形面积
    public void area(int l, int h) {
        System.out.println("三角形面积为：" + l * h / 2);
    }
}

public static void main(String[] args) {
    Shape shape = new Shape();
    // 正方形面积
    shape.area(3);
    // 三角形面积
    shape.area(5,2);
}

正方形的面积为：9
三角形面积为：5
```

定义一个形状的类，有两个同名，参数不同，来实现计算打印正方形和三角形的面积。此种方式，称之为方法重载。运行时通过传入不同的参数，来实现不同的行为。编译时即可确定。

接下来，看一个运行时多态的例子：

```
public interface Animal {

    public void eat();
    public void drink();
    public void run();
}

public class Cat implements Animal {
    
    @Override
    public void eat() {
        System.out.println("猫猫吃饭");
    }
}

public class Dog implements Animal {

    @Override
    public void eat() {
        System.out.println("狗狗吃饭");
    }
}

public static void main(String[] args) {
        Animal dog = new Dog();
        Animal cat = new Cat();
        dog.eat();
        cat.eat();
    }
    
狗狗吃饭
猫猫吃饭
```

`cat`和 `dog` 的类都实现了 `Animal` 接口，都实现了 `eat` 方法。编译时，只知道 `dog` 和 `cat` 是 `Animal` 类型，只有在运行时才知道具体调用哪个实现方法。

### 引用

* [多态](https://www.liaoxuefeng.com/wiki/1252599548343744/1260455778791232)
* [Polymorphism in Java – An Introduction](https://www.mygreatlearning.com/blog/polymorphism-in-java/#What%20is%20Polymorphism%20in%20Java?)

## 抽象类和接口的区别

抽象类：至少有一个抽象方法。抽象方法：只有方法的定义，没有具体实现。方法定义后加分号。抽象类用 `Abstract` 修饰。

接口：所有方法均为抽象方法。关键字 `Interface`。

## HashMap的实现原理

## ConcurrentHashMap的实现原理

# 数据库基础

## MySQL锁的类型，各自的适用场景

* 按使用粒度划分为表锁，行锁，间隙锁。
* 按级别划分为读锁和写锁。

### 表锁 (Table Level Locks)

表锁是 `MySQL` 的访问表或查询表中数据的默认锁的级别。 `MyISAM` 存储引擎只支持表锁。

sql语句：

```
LOCK TABLES 
```

```
FLUSH TABLES tabl_name,[,tbl_name] WITH READ LOCK
```

### 行锁 (Row Level Locks)

`InnoDB` 和 `NDB` 存储引擎使用行级锁而不是表锁。这意味着只会锁住实际用到的记录而不是整个表。

### 读锁 (Read Locks)

读锁为共享锁 (Shared Lock)。有如下特征：

* 多个会话可同时获得共享锁。此外，其它会话可在没有获得锁时读取表中数据。
* 获得读锁的会话，只能读取表中数据，不能向表中写入数据。其它会话在读锁释放前，不能向表中写入数据。写操作在读锁释放前，将进入等待状态。
* 如会话终止，`MySQL`会显式释放所有的锁。

### 写锁 (Write Locks)

写锁为排它锁 (Exclusive Lock)。有如下特征：

* 获得写锁的会话，可从表中读取数据或向表中写入数据。其它会话不能读取或者写入，在排它锁释放前。
* 仅有一个会话能获得写锁。

### 引用

* [MySQL Table Locking](https://www.mysqltutorial.org/mysql-table-locking/)
* [What are the various types of locking used in the MySQL Server](https://www.thegeekdiary.com/what-are-the-various-types-of-locking-used-in-the-mysql-server/)
* [InnoDB Locking](https://dev.mysql.com/doc/refman/8.0/en/innodb-locking.html)

## 事务的隔离级别，MySQL的默认隔离级别

`InnoDB` 提供了四种事务的隔离级别：读未提交 (READ UNCOMMITTED), 读已提交 (READ COMMITTED), 可重复读 (REPEATABLE READ) 和序列化 (SERIALIZABLE)。`InnoDB` 默认的隔离级别为可重复读 (REPEATABLE READ)。 

### 引用

* [Innodb中的事务隔离级别和锁的关系](https://tech.meituan.com/2014/08/20/innodb-lock.html)
* [Transaction Isolation Levels](https://dev.mysql.com/doc/refman/8.0/en/innodb-transaction-isolation-levels.html)

## 事务的特性 ACID

原子性(atomicity), 一致性 (consistency), 隔离性 (isolation), 持久性 (durablity)。

* 原子性 (atomicity)。事务为一系列工作单元，可以被提交或者回滚。事务中对数据库做出的修改，要么 `commit` 后成功，要么失败后 `roll back`回滚。
* 一致性 (consistency)。事务中如涉及到多张表的修改，则在事务提交或回滚后，查询各表数据。要么成功后，各表中数据为修改后的值。要么失败回滚后，各表中数据为操作前的值。
* 隔离性 (isolation)。各事务在执行期间相互隔离，不能互相干扰或者读取到其他事务未提交的数据。隔离性是基于锁机制来实现的。有经验的用户可以通过修改事务的隔离级别，牺牲隔离性以提升性能和并发性，不过要确保事务之间不会相互干扰。
* 持久性 (durability)。事务一旦成功提交，即使中途发生断电，系统崩溃，竞争条件或其它潜在的非数据库应用被攻击的风险，事务中对数据做的改变也不会丢失。在写操作期间，持久性通常涉及到将操作写入到磁盘，足够数量的冗余备份以应对电源故障或软件崩溃。

### 引用

* [MySQL Glossary](https://dev.mysql.com/doc/refman/8.0/en/glossary.html#glos_acid)

# Spring基础

## spring-boot默认的数据源连接池

数据源 (DataSource) : 连接到物理数据库的工厂，作为 `DriverManager`的替代性增强。数据源可通过设置 `URL`，用户名和密码来建立连接。

`SpringBoot` 自动配置了轻量级、高性能的连接池：`HikariCP`, `Tomcat JDBC Connection Pool` , `Common DBCP`.

`Spring Boot 1.x` 默认的连接池为 `Tomcat JDBC Connection Pool` ，`Spring Boot 2.x` 改为了 `Hikaricp`. 

### 引用

*  [Configuring a DataSource Programmatically in Spring Boot](https://www.baeldung.com/spring-boot-configure-data-source-programmatic)
* [Spring Boot DataSource Configuration](https://howtodoinjava.com/spring-boot2/datasource-configuration/)

## spring-boot自动装配原理

## SpringBootApplication 注解原理

## spring boot 如何整合spring mvc

## mybatis where原理

## spring cache

## spring双向引用（circular dependency）

## bean的生命周期，如何捕获生命周期事件

## spring缓存机制

## 项目中哪些会用到spring security,解决了哪些问题

## docker解决了什么问题

## vue数据流驱动底层原理

## 虚拟dom的工作原理

* [Reconciliation](https://reactjs.org/docs/reconciliation.html)
* [What is Virtual Dom? And Why is it faster?](https://dev.to/karthikraja34/what-is-virtual-dom-and-why-is-it-faster-14p9?utm_source=pocket_mylist)
