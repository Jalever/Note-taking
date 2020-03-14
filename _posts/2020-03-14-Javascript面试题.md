---
layout: post
title: Javascript面试题
subtitle: 面试题
date: 2020-03-14
author: Jalever
header-img: img/post_bg_fancyCrave.jpg
catalog: true
tags:
  - Interview Questions
---

- [undefined 和 null 有什么区别？](#undefined-%e5%92%8c-null-%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
- [什么是事件传播?](#%e4%bb%80%e4%b9%88%e6%98%af%e4%ba%8b%e4%bb%b6%e4%bc%a0%e6%92%ad)
- [什么是事件冒泡？](#%e4%bb%80%e4%b9%88%e6%98%af%e4%ba%8b%e4%bb%b6%e5%86%92%e6%b3%a1)
- [什么是事件捕获？](#%e4%bb%80%e4%b9%88%e6%98%af%e4%ba%8b%e4%bb%b6%e6%8d%95%e8%8e%b7)
- [event.preventDefault() 和 event.stopPropagation()方法之间有什么区别？](#eventpreventdefault-%e5%92%8c-eventstoppropagation%e6%96%b9%e6%b3%95%e4%b9%8b%e9%97%b4%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
- [如何知道是否在元素中使用了 event.preventDefault()方法？](#%e5%a6%82%e4%bd%95%e7%9f%a5%e9%81%93%e6%98%af%e5%90%a6%e5%9c%a8%e5%85%83%e7%b4%a0%e4%b8%ad%e4%bd%bf%e7%94%a8%e4%ba%86-eventpreventdefault%e6%96%b9%e6%b3%95)
- [什么是 event.target 和 event.currentTarget？](#%e4%bb%80%e4%b9%88%e6%98%af-eventtarget-%e5%92%8c-eventcurrenttarget)
- [== 和 === 有什么区别？](#%e5%92%8c--%e6%9c%89%e4%bb%80%e4%b9%88%e5%8c%ba%e5%88%ab)
- [如何在一行中计算多个表达式的值？](#%e5%a6%82%e4%bd%95%e5%9c%a8%e4%b8%80%e8%a1%8c%e4%b8%ad%e8%ae%a1%e7%ae%97%e5%a4%9a%e4%b8%aa%e8%a1%a8%e8%be%be%e5%bc%8f%e7%9a%84%e5%80%bc)
- [什么是提升？](#%e4%bb%80%e4%b9%88%e6%98%af%e6%8f%90%e5%8d%87)
- [什么是作用域？](#%e4%bb%80%e4%b9%88%e6%98%af%e4%bd%9c%e7%94%a8%e5%9f%9f)
- [什么是闭包？](#%e4%bb%80%e4%b9%88%e6%98%af%e9%97%ad%e5%8c%85)
- [JavaScript 中的虚值是什么？](#javascript-%e4%b8%ad%e7%9a%84%e8%99%9a%e5%80%bc%e6%98%af%e4%bb%80%e4%b9%88)
- ['use strict' 是干嘛用的？](#use-strict-%e6%98%af%e5%b9%b2%e5%98%9b%e7%94%a8%e7%9a%84)

## undefined 和 null 有什么区别？

它们属于 JavaScript 的 7 种基本类型

- string
- number
- null
- undefined
- boolean
- symbol
- bigint

`undefined`是未指定特定值的变量的默认值，或者没有显式返回值的函数，如：`console.log(1)`，还包括对象中不存在的属性，这些 JS 引擎都会为其分配 `undefined` 值

```js
let _thisIsUndefined;
const doNothing = () => {};
const someObj = {
  a: "ay",
  b: "bee",
  c: "si"
};

console.log(_thisIsUndefined); // undefined
console.log(doNothing()); // undefined
console.log(someObj["d"]); // undefined
```

`null`是“不代表任何值的值”。`null`是已明确定义给变量的值

```js
fs.readFile("path/to/file", (e, data) => {
  console.log(e); // 当没有错误发生时，打印 null
  if (e) {
    console.log(e);
  }
  console.log(data);
});
```

在比较`null`和`undefined`时，我们使用`==`时得到`true`，使用`===`时得到`false`

## 什么是事件传播?

当事件发生在`DOM`元素上时，该事件并不完全发生在那个元素上。在“冒泡阶段”中，事件冒泡或向上传播至父级，祖父母，祖父母或父级，直到到达`window`为止；而在“捕获阶段”中，事件从`window`开始向下触发元素 事件或`event.target`。

事件传播有三个阶段：

- 捕获阶段–事件从 `window` 开始，然后向下到每个元素，直到到达目标元素。

- 目标阶段–事件已达到目标元素。

- 冒泡阶段–事件从目标元素冒泡，然后上升到每个元素，直到到达 `window`

## 什么是事件冒泡？

```js
<div class="grandparent">
  <div class="parent">
    <div class="child">1</div>
  </div>
</div>
```

如果单击`child`元素，它将分别在控制台上记录`child`，`parent`，`grandparent`，`html`，`document`和`window`，这就是事件冒泡。

## 什么是事件捕获？

```js
<div class="grandparent">
  <div class="parent">
    <div class="child">1</div>
  </div>
</div>
```

如果单击`child`元素，它将分别在控制台上记录`window`，`document`，`html`，`grandparent`，`parent`和`child`，这就是事件冒泡。

## event.preventDefault() 和 event.stopPropagation()方法之间有什么区别？

`event.preventDefault()`方法可防止元素的默认行为

- 如果在表单元素中使用，它将阻止其提交
- 如果在锚元素中使用，它将阻止其导航
- 如果在上下文菜单中使用，它将阻止其显示或显示

`event.stopPropagation()`方法用于阻止捕获和冒泡阶段中当前事件的进一步传播

## 如何知道是否在元素中使用了 event.preventDefault()方法？

我们可以在事件对象中使用`event.defaultPrevented`属性。它返回一个布尔值用来表明是否在特定元素中调用了`event.preventDefault()`

## 什么是 event.target 和 event.currentTarget？

简单来说，`event.target`是发生事件的元素或触发事件的元素, `event.currentTarget`是我们在其上显式附加事件处理程序的元素

假设有如下的 HTML 结构：

```js
<div
  onclick="clickFunc(event)"
  style="text-align: center;margin:15px;
border:1px solid red;border-radius:3px;"
>
  <div style="margin: 25px; border:1px solid royalblue;border-radius:3px;">
    <div style="margin:25px;border:1px solid skyblue;border-radius:3px;">
      <button style="margin:10px">Button</button>
    </div>
  </div>
</div>
```

如果单击 `button`，即使我们将事件附加在最外面的`div`上，它也将打印 `button` 标签，因此我们可以得出结论`event.target`是触发事件的元素。
如果单击 `button`，即使我们单击该 `button`，它也会打印最外面的`div`标签。在此示例中，我们可以得出结论，`event.currentTarget`是附加事件处理程序的元素

## == 和 === 有什么区别？

`==`用于一般比较，`===`用于严格比较，`==`在比较的时候可以转换数据类型，`===`严格比较，只要类型不匹配就返回`flase`

## 如何在一行中计算多个表达式的值？

可以使用逗号运算符在一行中计算多个表达式。它从左到右求值，并返回右边最后一个项目或最后一个操作数的值。

```js
let x = 5;

x = (x++, (x = addFive(x)), (x *= 2), (x -= 5), (x += 10));

function addFive(num) {
  return num + 5;
}
```

上面的结果最后得到 x 的值为`27`。首先，我们将`x`的值增加到`6`，然后调用函数`addFive(6)`并将`6`作为参数传递并将结果重新分配给`x`，此时`x`的值为`11`。之后，将`x`的当前值乘以 `2` 并将其分配给`x`，`x`的更新值为`22`。然后，将`x`的当前值减去 `5` 并将结果分配给`x` `x`更新后的值为`17`。最后，我们将`x`的值增加`10`，然后将更新的值分配给`x`，最终`x`的值为`27`

## 什么是提升？

`提升`是用来描述变量和函数移动到其(全局或函数)作用域顶部的术语。

为了理解提升，需要来了解一下执行上下文。`执行上下文`是当前正在执行的“代码环境”。`执行上下文`有两个阶段:`编译`和`执行`。

`编译`-在此阶段，`JS` 引荐获取所有函数声明并将其提升到其作用域的顶部，以便我们稍后可以引用它们并获取所有变量声明（使用 var 关键字进行声明），还会为它们提供默认值：`undefined`。

`执行`——在这个阶段中，它将值赋给之前提升的变量，并执行或调用函数(对象中的方法)。

注意:只有使用`var`声明的变量，或者`函数声明`才会被提升，相反，`函数表达式`或`箭头函数`，`let`和`const`声明的变量，这些都不会被提升。

假设在全局使用域，有如下的代码：

```js
console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));

function greet(name) {
  return "Hello " + name + "!";
}

var y;
```

上面分别打印：`undefined`,`1`, `Hello Mark!`。

上面代码在编译阶段其实是这样的：

```js
function greet(name) {
  return "Hello " + name + "!";
}

var y; // 默认值 undefined

// 等待“编译”阶段完成，然后开始“执行”阶段

/*
console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));
*/
```

编译阶段完成后，它将启动执行阶段调用方法，并将值分配给变量。

```js
function greet(name) {
  return "Hello " + name + "!";
}

var y;

//start "execution" phase

console.log(y);
y = 1;
console.log(y);
console.log(greet("Mark"));
```

## 什么是作用域？

`JavaScript` 中的作用域是我们可以有效访问变量或函数的区域。`JS`有三种类型的作用域：全局作用域、函数作用域和块作用域(ES6)。

`全局作用域`——在全局命名空间中声明的变量或函数位于全局作用域中，因此在代码中的任何地方都可以访问它们

```js
//global namespace
var g = "global";

function globalFunc() {
  function innerFunc() {
    console.log(g); // can access "g" because "g" is a global variable
  }
  innerFunc();
}
```

`函数作用域`——在函数中声明的变量、函数和参数可以在函数内部访问，但不能在函数外部访问。

```js
function myFavoriteFunc(a) {
  if (true) {
    var b = "Hello " + a;
  }
  return b;
}

myFavoriteFunc("World");

console.log(a); // Throws a ReferenceError "a" is not defined
console.log(b); // does not continue here
```

`块作用域`-在块`{}`中声明的变量（`let`，`const`）只能在其中访问

```js
function testBlock() {
  if (true) {
    let z = 5;
  }
  return z;
}

testBlock(); // Throws a ReferenceError "z" is not defined
```

作用域也是一组用于查找变量的规则。如果变量在当前作用域中不存在，它将向外部作用域中查找并搜索，如果该变量不存在，它将再次查找直到到达全局作用域，如果找到，则可以使用它，否则引发错误，这种查找过程也称为`作用域链`。
```js
 /* 作用域链

     内部作用域->外部作用域-> 全局作用域
  */

  // 全局作用域
  var variable1 = "Comrades";   
  var variable2 = "Sayonara";

  function outer(){
  // 外部作用域
    var variable1 = "World";
    function inner(){
    // 内部作用域
      var variable2 = "Hello";
      console.log(variable2 + " " + variable1);
    }
    inner();
  }  
  outer(); // Hello World
```


## 什么是闭包？
`闭包`就是一个函数在声明时能够记住当前作用域、父函数作用域、及父函数作用域上的变量和参数的引用，直至通过作用域链上全局作用域，基本上闭包是在声明函数时创建的作用域

## JavaScript 中的虚值是什么？

```js
const falsyValues = ["", 0, null, undefined, NaN, false];
```

简单的来说虚值就是是在转换为布尔值时变为 `false` 的值。

## 'use strict' 是干嘛用的？
`"use strict"` 是 ES5 特性，它使我们的代码在函数或整个脚本中处于严格模式。严格模式帮助我们在代码的早期避免 bug，并为其添加限制

设立”严格模式”的目的，主要有以下几个：

- 消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为;

- 消除代码运行的一些不安全之处，保证代码运行的安全；

- 提高编译器效率，增加运行速度；

- 为未来新版本的Javascript做好铺垫。

