# JavaScript 中的关键字“this”举例说明

> 原文：<https://javascript.plainenglish.io/the-keyword-this-in-javascript-explained-with-examples-9811050942a6?source=collection_archive---------17----------------------->

## 了解 JavaScript 中的关键字“this”。

![](img/7c8cbc451e5c79a9bb4d38fdb2f4b541.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

关键字`this`是 JavaScript 中引入的有用特性之一。它是指它所属的对象，根据它的使用场合，它有不同的值。就像单词`this`本身一样，我们可以理解它指的是什么。

在本文中，我们将通过一些实例来学习 JavaScript 中的关键字`this`。让我们开始吧。

# “这”的值

我说过，关键字`this`根据使用的场合不同，有不同的值。它在 JavaScript 中的工作方式不同于其他编程语言。

下面是关键字`this`可以取值的列表:

*   在方法中，`this`指所有者对象。
*   在函数中，`this`指的是全局对象。
*   在一个函数中，在严格模式下，`this`就是`undefined`。
*   单独，`this`指全局对象。
*   在事件中，`this`指的是接收事件的元素。
*   像`call()`和`apply()`这样的方法可以将`this`引用到任何对象。

# 方法中的关键字“this”

在下面的例子中，“**this”**表示 person 对象。因为 person 对象拥有 fullName 方法。

```
var person = {
  firstName: "John",
  lastName : "Doe",
  fullName : function() {
    return **this**.firstName + " " + **this**.lastName;
  }
};
//John Doe
```

正如您所看到的，关键字`this`对于在特定的上下文中引用属性非常有用。

# 单单“这个”这个关键词

当我们单独使用关键字`this`时，所有者就是全局对象。所以`this`指的是全局对象。

这里有一个例子:

```
let x = **this**;
console.log(x); // Prints the window object to the console.
```

通过在变量中单独使用关键字`this`。这种情况下的`this`指的是对象`window`(全局对象)。

# 函数中的关键字“this”

在 JavaScript 函数中，函数的所有者是`this`的默认绑定。

所以，在一个函数中，`this`指的是全局对象`[object Window]`。

```
function myFunction() {
  return **this**;
}
myFunction();
// [object Window]
```

在严格模式下，JavaScript 不允许默认绑定。因此，当在函数中使用时，在严格模式下，`this`将是`undefined`。

```
"use strict";
function myFunction() {
  return **this**;
}
myFunction();
// undefined
```

# 带有事件处理程序的关键字“this”

说到事件处理程序，关键字`this`指的是接收事件的元素。例如，在一个点击事件中，关键字`this`指的是接收该事件(点击)的按钮。

这里有一个例子:

```
<button onclick="**this.style.display='none'**">Click to Remove Me!</button>// When you click the button the style applies to it.
```

单击按钮元素后，它将被删除，因为关键字`this`指的是按钮。

# 显式函数绑定

`call()`和`apply()`方法是预定义的 JavaScript 方法。它们都可以用来调用一个对象方法，并将另一个对象作为参数。

在下面的例子中，当使用 person2 作为函数`call`的参数调用`person1.fullName`时，`this`将引用 person2，即使它位于 person1 对象中:

```
var person1 = {
  fullName: function() {
    return **this**.firstName + " " + **this**.lastName;
  }
}
var person2 = {
  firstName:"John",
  lastName: "Doe",
}
person1.fullName.**call**(person2);  // Will return "John Doe"
```

# 使用构造函数

当一个函数被用作构造函数(带有`new`关键字)时，它的`this`被绑定到正在被构造的新对象。

这里有一个例子:

```
function First() {
  **this**.a = 37;
}

var obj = new First();
console.log(obj.a); // 37
```

虽然构造函数的默认设置是返回由`this`引用的对象，但它也可以返回其他对象(如果返回值不是对象，则返回对象`this`)。

# 结论

JavaScript 中的关键字`this`是一个强大的工具，通常可以帮助开发人员在特定的上下文中引用属性，但有时在应用不同级别的范围时也可能会非常棘手。如果您有兴趣，可以从 [MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)中了解更多关于这个主题的信息。

感谢您阅读本文，希望您觉得有用。

# 更多阅读

[](https://medium.com/javascript-in-plain-english/writing-asynchronous-code-in-javascript-using-async-and-await-5d43ddcfa31b) [## 使用 Async 和 Await 在 JavaScript 中编写异步代码

### 用例子学习写异步 JavaScript。

medium.com](https://medium.com/javascript-in-plain-english/writing-asynchronous-code-in-javascript-using-async-and-await-5d43ddcfa31b)