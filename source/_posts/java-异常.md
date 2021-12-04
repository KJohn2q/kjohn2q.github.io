---
title: java 异常
tags:
  - java
  - 异常
categories:
  - java
date: 2021-12-04 08:40:24
---

## 如何进行异常处理？

`java` 通过面向对象的方法进行异常处理，把各种不同的异常进行分类，并提供了良好的接口。

## 异常处理机制

`java` 程序在执行的过程中如果出现异常，会自动生成一个异常对象，该异常对象将被自动提交给 `JVM`，当 `JVM` 接收到异常对象时，会寻找能处理这异常的代码并把当前异常对象交给其处理，这一过程称为捕获异常。如果 `JVM` 找不到可以捕获异常的方法，则运行时系统将终止，相应的Java程序也将退出。

### 关键字解释

- `try`: 测试它所包含的代码是否会发生异常
- `catch`: 在异常发生时就抓住它，并进行响应的处理，使程序不受该异常的影响从而继续执行下去。
- `throw`: 明确抛出一个异常。
- `throws`: 声明一个方法可能抛出的各种异常。
- `finally`: 为确保一段代码不管发生什么异常状况都要被执行。

## 异常类层次结构

![java-exceptions-hierarchy-example](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112040850922.png)

如图所示，异常类层次结构顶部为 `Throwable` 类，该类直接继承自 `Object`。 该类有两个直接子类：`Error` 和 `Exception`。

### Errors 和 Exceptions

`Error` 表示出现了非常严重的问题，不能通过程序捕获来解决问题，而应该检查架构。如：`OutOfMemoryError`, `StackOverflowError`等。

```java
public static void print(String myString) {
    print(myString);
}
```

```
Exception in thread "main" java.lang.StackOverflowError
at StackOverflowErrorExample.print(StackOverflowErrorExample.java:6)
```

上面的代码中，print方法递归调用自身，且没有中断条件。会导致不断地生成新的方法栈，当达到 `java` 栈的最大值时，栈溢出。

`Exception` 用于程序需要捕获的异常条件。如：`FileNotFoundException`，`SocketException`等。`Exception` 又分为受检型异常（`Checked Exception`）和非受检型异常（`Unchecked Exception`）。

### 受检型异常和非受检型异常

![img](https://cdn.jsdelivr.net/gh/KJohn2q/John-s-figure-bed/image/202112040956956.png)

受检型异常发生在编译时期，需要在程序中显式处理 `catch`. `Exception`中除 `RuntimeException`的其它类及其子类均为受检型异常。

```java
public void writeToFile() {
    try (BufferedWriter bw = new BufferedWriter(new FileWriter("myFile.txt"))) {
        bw.write("Test");
    } catch (IOException ioe) {
        ioe.printStackTrace();
    }
}

```

非受检型异常，可能发生在任何时期，如运行期。不需要在程序中显式处理 `catch`。`RuntimeException`及其子类均为非受检型异常。

```java
public void writeToFile() {
    try (BufferedWriter bw = null) {
    	bw.write("Test");
    } catch (IOException ioe) {
    	ioe.printStackTrace();
    }
}
```

当调用上面方法时，程序会发生 `NullPointerException` 异常。因为 `bw` 为 `Null`

```
Exception in thread "main" java.lang.NullPointerException
    at IOExceptionExample.writeToFile(IOExceptionExample.java:10)
    at IOExceptionExample.main(IOExceptionExample.java:17)
```

 如上所述，`NullPointerException` 属于非受检型异常，无需捕获。而应该修改程序来解决。

## 总结

综上所述，`Error` 和 非受检型异常应该通过检查和修改程序来解决，无需捕获。受检型异常发生在编译期，需要再程序中显式处理，否则无法通过编译。

## 引用

* [Java Exceptions Hierarchy](https://rollbar.com/blog/java-exceptions-hierarchy-explained/)
* [Java 中的异常处理](https://snailclimb.gitee.io/javaguide-interview/#/./docs/b-1%E9%9D%A2%E8%AF%95%E9%A2%98%E6%80%BB%E7%BB%93-Java%E5%9F%BA%E7%A1%80?id=_2129-java-%e4%b8%ad%e7%9a%84%e5%bc%82%e5%b8%b8%e5%a4%84%e7%90%86)
