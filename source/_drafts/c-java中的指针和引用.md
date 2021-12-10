---
title: 'c++,java中的指针和引用'
date: 2021-12-10 08:31:52
tags: [java, c++, '指针', '引用']
categories: 笔记
---

`C++` 中有指针（Pointer）和引用 （Reference），而 `Java` 中只有引用的。那它们之间到底有什么区别呢？

## 指针 （Pointer）

在 `C++` 中，指针就是变量，不过其中保存的是另一个变量的内存地址。可这样定义：

```c++
int a = 5;
int *b = &a;
```

`a`  为整型变量，`b` 为 `int` 型的指针，`&` 为取址符号，可通过 `&a` 来取得变量 `a` 在内存中的地址，赋值给 `b`。

## 引用 （Reference）

在 `C++` 中，引用表示一个变量的别名。引用一旦初始化后，便不可再修改。与常量指针类似，可这样定义：

```c++
int a = 5;
int &b = a;
```

在 `Java`中，引用型变量保存的是新创建的对象在内存中的地址，与 `C++` 中的指针类似。不过在 `Java` 中，引用是不能运算的。可这样定义：

```java
StringBuilder s = new StringBuilder("hello world!!!");
s = new StringBuilder("hello Java!!!");
```

## 指针和引用的区别

`Java` 中引用和 `C++` 指针类似，故分开说明：

### `C++`中的指针与引用

* 指针变量在定义后，再初始化。而引用在定义时必须初始化。
* 指针变量可指向 `NULL` 值，而引用不可以。
* 指针在初始化后，可改为指向其它同样类型的变量。而引用在初始化后，便不能修改。
* 指针变量需要通过 `*` 来取得所指变量的值，而引用只需要用名字即可。

### `Java`中的引用与 `C++` 中的指针

`C++` 中的指针是可以运算的。而 `Java`中的引用不可以。

```c++
int a[] = {1, 2, 4};
int *b = a;
cout << *(b+1);
```

如代码所示，指针 `b` 指向数组 `a` 的初始地址，可通过指针运算的方式，取得数组中的值。

指针很灵活，不过如果不能正确的运用，风险也是很大的。

## 引用

* [Differences between pointers and references in C++](https://www.educative.io/edpresso/differences-between-pointers-and-references-in-cpp)
