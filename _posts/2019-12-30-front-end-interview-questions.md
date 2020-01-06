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

人人尽说江南好，游人只合江南老。春水碧于天，画船听雨眠。

## 基本概念

1。typeof 是做什么用的？什么情况下会用到？这反映了 JavaScript 变量的什么特点？

<details>
<summary>Example Answer</summary>
<p class="answer">
答： typeof 是用来检测变量的数据类型的。JavaScript 中有 5 种基本数据类型和 1 种复杂数据类型，分别是 Undefined、Null、Boolean、Number、String 和 Object，JS不支持创建自定义类型。更重要的是，JS 的变量是松散类型的，所谓松散类型就是可以用来保存任何类型的数据，鉴于此，当面对一个变量，我们想要获得它的变量类型时，typeof 就派上用场了。
</p>
</details>

2。 以下代码是否会报错？为什么？

```javascript
function doAdd(first, second) {
    console.log(first + second)
}

doAdd(1, 2, 3);
```

<details>
<summary>Example Answer</summary>
<p class="answer">
答：不会；JavaScript 中函数的参数与大多数其他语言的参数不同， JS 函数不介意传递进来多少个参数，也不在乎传进来的参数是什么类型。也就是说，即便你定义了只接收两个参数，在调用这个函数时也未必一定传递两个参数，可以传递一个、三个甚至不传递参数，而解析器永远不会有任何怨言。之所以会这样，原因是 JS 中函数的参数在内部是用一个数组来表示的，函数接收的始终都是这个数组，而不关心数组中包含哪些参数，在函数体内可以通过 arguments 对象来访问这个参数数组，从而可以获取到传递给函数的每一个参数。
</p>
</details>

## 基本类型与引用类型

1。【值传递】以下代码的输出值为？

```javascript
var num1 = 5;
var num2 = num1;
num1 = 10;
console.log(num2);
```

<details>
<summary>Example Answer</summary>
<p class="answer">
答： 在此，num1 中保存的值是 5。当使用 num1 的值来初始化 num2 时， num2 中也保存了值 5，但 num2 中的 5 和 num1 中的 5是完全独立的，该值知识 num1 中 5 的一个副本，此后，这两个变量不会相互影响。
</p>
</details>

2。【址传递】以下代码的输出值为？

```javascript
var obj1 = new Object();
var obj2 = obj1;
obj.name = "Nicholas";
console.log(obj2.name);
```

<details>
<summary>Example Answer</summary>
<p class="answer">
答： 变量 obj1 保存了一个对象的新实例，然后，这个值被复制到了 obj2 中，此时 obj1 和 obj2 都指向同一个对象，这样，当 obj1 添加了 name 属性后，可以通过 obj2 来访问这个属性，因为这两个变量引用的都是同一个对象。
</p>
</details>

3。【数组排序】以下代码的输出值为？

```javascript
var values = [10, 15, 5, 0, 1];
values.sort();
alert(values);
```

<details>
<summary>Example Answer</summary>
<p class="answer">
答： 0,1,10,15,5。<br>
<br>
原因： 数组中有 sort() 方法，默认按升序排列数组项，sort() 方法会调用每隔数组项的 toString() 转型方法，然后比较得到的字符串，以确定如何排序。即时数组中每一项都是数值，sort() 方法比较的也是字符串。
</p>
</details>

4。【数组重排序】为 sort() 方法写一个比较函数，使得数组 [0, 1, 5, 10, 15] 按照数值大小正确排序。

<details>
<summary>Example Answer</summary>
<p class="answer">
答： 由于 sort() 方法默认仅会通过测试字符串的结果改变原来的顺序，这在很多情况下并不是我们需要的方案，因此 sort() 方法可以接收一个比较函数作为参数，以便我们指定哪个值位于哪个值的前面。
</p>
<pre class="answer">
// javascript
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
</pre>
</details>

5。【数组迭代】数组迭代的方法有哪些？every()、some()、filter()、map()、forEach()的区别是什么？

<details>
<summary>Example Answer</summary>
<pre class="answer">
答：ES5 为数组定义了 5 个迭代方法，每个方法都接收两个参数：➀要在每一项上运行的参数➁[可选项]运行该函数的作用域对象。

every()：对数组中的每一项运行给定函数，如果该函数对每一项都返回 true，则返回 true。

some()：对数组中的每一项运行给定函数，如果该函数对其中一项返回 true，则返回 true。

filter()：对数组中的每一项运行给定函数，返回该函数会返回 true 的项组成的数组。

map()：对数组中的每一项运行给定函数，返回每次函数调用的结果组成的数组。

forEach()：对数组中的每一项运行给定函数。这个方法没有返回值。

这些方法都不会修改原数组包含的值。
</pre>
</details>

6。【Date类型】创建一个时间为 2020 年 1 月 3 日 23 时 05 分 25 秒 的本地时间日期对象。

<details>
<summary>Example Answer</summary>
<p class="answer">
答：var someDate = new Date(Date.parse("2020-01-03T23:05:25"));<br>
或：var someDate = new Date(2020, 0, 3, 23, 05, 25);
</p>
</details>

7。【Function类型】在 JavaScript 中，一切皆对象，函数实际上也是对象，每个函数都是 Function 类型的实例。在函数内部，有一个特殊的对象：arguments，请谈谈你对这个对象的理解。

<details>
<summary>Example Answer</summary>
<p class="answer">
答：JavaScript 中的函数不介意传递进来多少个参数，当调用某一个函数时，传递参数多了、少了都无所谓，原因是 JavaScript 中的参数内部是用一个数组来表示的，函数接收到的始终是这个数组，而不关心数组中包含哪些参数，如果这个数组中不包含任何元素，无所谓，如果包含多个元素，也没有问题。<br>
<br>
在函数体内，可以通过 arguments 这个对象来访问这个参数数组。
</p>
</details>

8。【Function类型】函数内部的 arguments 对象中有个 callee 的属性，它是做什么的？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：arguments 中的 callee 属性是一个指针，指向拥有这个 arguments 对象的函数。
</p>
</details>

9。【Function类型】函数内部有一个特殊对象 this，你如何理解的 this？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：this 引用的是函数据以执行的环境对象。
</p>
</details>

## 面向对象

> ECMA-262 把对象定义为：“无序属性的集合，其属性可以包含基本值、对象或者函数。”严格来讲，这就相当于说对象是一组没有特定顺序的值。对象的每个属性或方法都有一个名字，而每个名字都映射到一个值。正因这样，我们可以把 ECMAScript 的对象想象成散列表：无非就是一组名值对。

1。【工厂模式】创建对象有好几种方式，请书写一个工厂模式。

<details>
<summary>Example Answer</summary>
<pre class="answer">
// javascript
function createPerson(name, age, job) {
    var o = new Object();
    o.name = name;
    o.age = age;
    o.job = job;
    o.sayName = function() {
        alert(this.name);
    };
    return o;
}

var person1 = createPerson("Nicholars", 29, "Software Engineer");
</pre>
</details>

2。【工厂模式】使用 Object 构造函数或对象字面量的方式也可以用来创建单个对象，但代码可复用性较差，工厂模式解决了代码复用性的问题，这是它的优点，你能说说它的缺点吗？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：工厂模式虽然解决了创建多个相似对象的问题，但却没有解决对象识别问题，即怎样知道一个对象的类型。<br>
<br>
这也是构造函数之所以出现的原因。
</p>
</details>

3。【构造函数模式】请书写一个构造函数来创建对象。

<details>
<summary>Example Answer</summary>
<pre class="answer">
// javascript
function Person(name, age, job) {
    this.name = name;
    this.age = age;
    this.job = job;
    this.sayName = function() {
        alert(this.name);
    };
}

var person1 = new Person("Nicholars", 29, "Software Engineer");
</pre>
</details>

4。【构造函数模式】构造函数的缺点是什么？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：构造函数的主要问题，在于每个方法都要在每个实例上重新创建一遍，假如 Person 构造函数中有个 sayName 的函数，那么此时使用构造函数创建出的每个实例，都要重新创建一遍该方法。在 JavaScript 中，函数是 Function 引用类型的对象，因此，实际上，每个实例中的方法并不是同一个实例，尽管每个方法的运行机制、逻辑是相同的。这会造成不同的作用域链和标识符解析、资源浪费。<br>
<br>
这些问题可以使用原型模式解决。
</p>
</details>

5。【原型模式】任何时候，只要创建了一个新函数，就会为该函数创建一个 prototype 属性，这个属性就是指原型对象啦，在原型对象中有个 constructor 属性，你了解这个属性吗？这个属性是做什么的？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：这个属性包含一个执行 prototype 属性所在函数的指针。例如 Person 构造函数中有 prototype 属性，该 prototype 属性中有个 constructor（构造函数）属性，这个属性执行 Person 构造函数。
</p>
</details>

6。【原型模式】Chrome 为每个对象配置了一个属性 `__proto__`，你了解这个属性吗？请说一下构造函数、原型对象和实例之间的关系。

<details>
<summary>Example Answer</summary>
<p class="answer">
答：当调用构造函数创建一个新实例后，该实例内部将包含一个指针指向构造函数的原型对象，这个指针在 ES5 标准中称为 [[Prototype]]，不过，FireFox、Safari 和 Chrome 在每一个对象上都支持一个属性 `__proto__`，用以在对象上访问原型对象。<br>
<br>
构造函数、原型和实例的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个指向原型对象的内部指针。
</p>
</details>

7。【原型模式】你认为原型模式有什么问题？

<details>
<summary>Example Answer</summary>
<p class="answer">
答：首先，它省略了为构造函数传递初始化参数这一环节，结果所有实例在默认情况下都将取得相同的属性值，这在某种程度上会带来一些不方便。<br>
<br>
其次，原型模式中最大的问题是属性被所有实例共享。这种共享对于函数来说非常合适，N 个实例可以共享一个函数，对于包含基本值的属性也还说得过去，你可以通过在实例上添加一个同名属性来覆盖原型中的属性，但是对于包含引用类型值（比如 Array 的实例）的属性，问题比较突出。由于原型中的属性共享的本性，导致任何一个实例修改原型所在的属性值，该值所在的全部实例，都将被修改。危害极大。<br>
<br>
这就是为什么通行的做法中，大多组合使用构造函数模式和原型模式，实例属性都在构造函数中定义，而由所有实例共享的属性和方法则是在原型中定义。
</p>
</details>

8。【继承-原型链】什么是原型链？

<details>
<summary>My Answer</summary>
<p class="answer">
答：原型链就是让构造函数的原型对象指向另一个构造函数的实例，该实例包含指向原型对象的指针，而该指针又指向另另一个构造函数的实例，如此层层递进，就构成了实例与原型的链条，这就是所谓的原型链。
</p>
</details>

