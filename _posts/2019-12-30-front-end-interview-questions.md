---
layout: post
title: 《 JavaScript 高级程序设计》中的JS面试题
date: 2019-12-30 22:00:00
author: Haiyung
categories: cn
tags: 计算机应用技术
--- 

__Contents__

* content
{:toc}

## 前言

## 基本概念

1。typeof 是做什么用的？什么情况下会用到？这反映了 JavaScript 数据类型的什么特点？

答： typeof 是用来检测变量的数据类型的。JavaScript 中有 5 种基本数据类型和 1 种复杂数据类型，分别是 Undefined、Null、Boolean、Number、String 和 Object，JS不支持创建自定义类型。更重要的是，JS 的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据，鉴于此，当面对一个变量，我们想要获得它的变量类型时，typeof 就派上用场了。

2。 以下代码是否会报错？为什么？

```javascript
function doAdd(first, second) {
    console.log(first + second)
}

doAdd(1, 2, 3);
```

答：不会；JavaScript 中函数的参数与大多数其他语言的参数不同， JS 函数不介意传递进来多少个参数，也不在乎传进来的参数是什么类型。也就是说，即便你定义了只接收两个参数，在调用这个函数时也未必一定传递两个参数，可以传递一个、三个甚至不传递参数，而解析器永远不会有任何怨言。之所以会这样，原因是 JS 中函数的参数在内部是用一个数组来表示的，函数接收的始终都是这个数组，而不关心数组中包含哪些参数，在函数体内可以通过 arguments 对象来访问这个参数数组，从而可以获取到传递给函数的每一个参数。

## 作用域



## 引用类型

## JS 中的面向对象