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

1。typeof 是做什么用的？什么情况下会用到？这反映了 JavaScript 变量的什么特点？

答： typeof 是用来检测变量的数据类型的。JavaScript 中有 5 种基本数据类型和 1 种复杂数据类型，分别是 Undefined、Null、Boolean、Number、String 和 Object，JS不支持创建自定义类型。更重要的是，JS 的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据，鉴于此，当面对一个变量，我们想要获得它的变量类型时，typeof 就派上用场了。

2。 以下代码是否会报错？为什么？

```javascript
function doAdd(first, second) {
    console.log(first + second)
}

doAdd(1, 2, 3);
```

答：不会；JavaScript 中函数的参数与大多数其他语言的参数不同， JS 函数不介意传递进来多少个参数，也不在乎传进来的参数是什么类型。也就是说，即便你定义了只接收两个参数，在调用这个函数时也未必一定传递两个参数，可以传递一个、三个甚至不传递参数，而解析器永远不会有任何怨言。之所以会这样，原因是 JS 中函数的参数在内部是用一个数组来表示的，函数接收的始终都是这个数组，而不关心数组中包含哪些参数，在函数体内可以通过 arguments 对象来访问这个参数数组，从而可以获取到传递给函数的每一个参数。

## 基本类型与引用类型

1。【值传递】以下代码的输出值为？

```javascript
var num1 = 5;
var num2 = num1;
num1 = 10;
console.log(num2);
```

答： 在此，num1 中保存的值是 5。当使用 num1 的值来初始化 num2 时， num2 中也保存了值 5，但 num2 中的 5 和 num1 中的 5是完全独立的，该值知识 num1 中 5 的一个副本，此后，这两个变量不会相互影响。

2。【址传递】以下代码的输出值为？

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj.name = "Nicholas";
console.log(obj2.name);
```

答： 变量 obj1 保存了一个对象的新实例，然后，这个值被复制到了 obj2 中，此时 obj1 和 obj2 都指向同一个对象，这样，当 obj1 添加了 name 属性后，可以通过 obj2 来访问这个属性，因为这两个变量引用的都是同一个对象。

3。【数组排序】以下代码的输出值为？

```javascript
var values = [10, 15, 5, 0, 1];
values.sort();
alert(values);
```

答： 0,1,10,15,5。

原因： 数组中有 sort() 方法，默认按升序排列数组项，sort() 方法会调用每隔数组项的 toString() 转型方法，然后比较得到的字符串，以确定如何排序。即时数组中每一项都是数值，sort() 方法比较的也是字符串。

4。【数组重排序】为 sort() 方法写一个比较函数，使得数组 [0, 1, 5, 10, 15] 按照数值大小正确排序。

答： 由于 sort() 方法默认仅会通过测试字符串的结果改变原来的顺序，这在很多情况下并不是我们需要的方案，因此 sort() 方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面。

```javascript
function compare(value1, value2) {
    if (value1 < value2) {
        return -1;
    } else if (value1 > value2) {
        return 1;
    } else {
        return 0;
    }
}

var values = [0, 1, 5, 10, 15];
values.sort(compare);
alert(values);
```

5。【数组迭代】数组迭代的方法有哪些？every()、some()、filter()、map()、forEach()的区别是什么？

答：ES5 为数组定义了 5 个迭代方法，每个方法都接收两个参数：➀要在每一项上运行的参数➁[可选项]运行该函数的作用域对象。

every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。

some()：对数组中的每一项运行给定函数，如果该函数对其中一项返回 true，则返回 true。

filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。

map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。

forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。

这些方法都不会修改原数组包含的值。

6。【Date类型】创建一个时间为 2020 年 1 月 3 日 23 时 05 分 25 秒 的本地时间日期对象。

答：var someDate = new Date(Date.parse("2020-01-03T23:05:25"));

或：var someDate = new Date(2020, 0, 3, 23, 05, 25);

7。【Function类型】在 JavaScript 中，一切皆对象，函数实际上也是对象，每个函数都是 Function 类型的实例。在函数内部，有一个特殊的对象：arguments,请谈谈你对这个对象的理解。

答：JavaScript 中的函数不介意传递进来多少个参数，当调用某一个函数时，传递参数多了、少了都无所谓，原因是 JavaScript 中的参数内部是用一个数组来表示的，函数接收到的始终是这个数组，而不关心数组中包含哪些参数，如果这个数组中不包含任何元素，无所谓，如果包含多个元素，也没有问题。

在函数体内，可以通过 arguments 这个对象来访问这个参数数组。

8。【Function类型】函数内部的 arguments 对象中有个 callee 的属性，它是做什么的？

答：arguments 中的 callee 属性是一个指针，指向拥有这个 arguments 对象的函数。

9。【Function类型】函数内部有一个特殊对象 this,你如何理解的 this？

答：this 引用的是函数据以执行的**环境对象**。




## 面向对象