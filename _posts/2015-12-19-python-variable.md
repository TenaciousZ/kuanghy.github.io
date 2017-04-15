---
layout: post
title: "Python 类变量与实例变量"
category: Python
tags: python
---

### 基本概念

- 类变量：

类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。类变量在整个实例化的对象中是公用的。

- 实例变量：

定义在方法中的变量，用 self 绑定到实例上，只作用于当前实例的类。

### 访问方式

- 类变量：

在类内部和外部，类变量都用 ` 类名.类变量` 的形式访问。在类内部，也可以用 `self.类变量` 来访问类变量，但此时它的含义已经变了，实际上它已经成了一个实例变量。在实例变量没有被重新赋值时，用 `self.类变量` 才能访问到正确的值。简单的说就是实例变量会屏蔽掉类变量的值，就像局部变量屏蔽掉全局变量的值一样。所以一般情况下是不将类变量作为实例变量使用的。

- 实例变量：  

在类内部，实例变量用 `self.实例变量` 的形式访问；在类外部，用 `实例名.实例变量` 的形式访问。实例变量是绑定到一个实例上的变量，它只属于这个实例。这一点区别于类变量，类变量是所有来自于同一个类的实例所共享的。

### self 简介

类的方法与普通的函数只有一个特别的区别——它们必须有一个额外的第一个参数名称，但是在调用这个方法的时候你不为这个参数赋值，Python会提供这个值。这个特别的变量指对象本身，按照惯例它的名称是self。虽然你可以给这个参数任何名称，但是 强烈建议 你使用self这个名称。

实际上，实例变量就是一个用 self 修饰的变量。self 将一个变量绑定到一个特定的实例上，这样它就属于这实例自己。

### 举例说明

```python
#! /usr/bin/env python
# -*- coding: utf-8 -*-

# *************************************************************
#     Filename @  classvar.py
#       Author @  Huoty
#  Create date @  2015-12-19 09:39:36
#  Description @  
# *************************************************************

class A(object):
    va = 10

    def foo(self):
        print A.va
        print self.va

        self.va = 40
        print A.va
        print self.va

        va = 20
        print va

        A.va = 15
        print A.va
        print self.va

# Script starts from here

obj1 = A()
obj2 = A()
obj1.foo()
print A.va
print obj1.va
print obj2.va
```

程序的输出结果：

<pre>
10
10
10
40
20
15
40
15
40
15
</pre>

分析程序结果我们发现，一般情况下，类变量可以用类名或者self的形式访问。当 `self.类变量` 被重新赋值时，它的值就发生了变化，但类变量的值不会随之变化。方法内的局部变量会屏蔽掉类变量和实例变量。类变量是所有实例共享的，而实例变量只属于对象自己，每个实例的实例变量可以有不同的值。

### 要点总结

- 1、类变量可以用 `类名.类变量` 和 `self.类变量` 两种方式访问，后者一般情况不建议使用。

- 2、类变量是所有对象所共享的，无论任何时候都建议用类名的方式访问类变量。

- 3、实例变量在类内部用 self 访问，在类外部用实例名访问。

- 4、类变量通过 self 访问时则被转化为实例变量，被绑定到特定的实例上，其值会屏蔽掉类变量。

- 5、通过对实例变量（self）的形式对类变量重新赋值后，类变量的值不随之变化。

- 6、方法内的局部变量会屏蔽掉类变量和实例变量。

- 7、同一实例变量在不同的实例中可能拥有不同的值。