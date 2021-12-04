---
title: java面试题
date: 2021-12-04 17:03:35
tags: [java, 面试]
categories: [面试]
---



## java基础数据类型

* 整型：byte(1 byte),short(2 byte),int(4 byte),long(8 byte)
* 浮点型：float(4 byte),double(8 byte)
* 字符型：char(2 byte)
* 布尔类型：bool

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

## java泛型

## java多态

## 抽象类和接口的区别

抽象类：至少有一个抽象方法。抽象方法：只有方法的定义，没有具体实现。方法定义后加分号。抽象类用 `Abstract` 修饰。

接口：所有方法均为抽象方法。关键字 `Interface`。

# 数据库基础

## MySQL锁的类型，各自的适用场景

## 事务的隔离级别，MySQL的默认隔离级别

### 引用

* [Innodb中的事务隔离级别和锁的关系](https://tech.meituan.com/2014/08/20/innodb-lock.html)

# Spring基础

## spring-boot默认的数据源连接池

## spring-boot自动装配原理

## SpringBootApplication 注解原理

## spring boot 如何整合spring mvc

## mybatis where原理

## 事务的特征（ACID）

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
