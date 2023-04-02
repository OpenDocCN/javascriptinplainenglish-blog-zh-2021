# 理解 JavaScript 中的绑定方法

> 原文：<https://javascript.plainenglish.io/understanding-the-bind-method-in-javascript-3e51d2b9c35a?source=collection_archive---------8----------------------->

## 通过示例了解 JavaScript 中的 bind 方法。

![](img/a6e61faba701177cadba927aa768ef18.png)

Image created with ❤️️ By [author](https://mehdiouss315.medium.com/).

# 介绍

在 JavaScript 中，函数有自己的原型对象`Function`。这个原型有很多我们可以使用的方法和属性，而 **bind** 方法就是其中之一。它返回新的函数，将它们自己的关键字`this`设置为提供的值。我们将在下面用一些例子来解释。

在本文中，我们将通过一些实例来学习 JavaScript 中的 bind 方法。让我们开始吧。

# 该绑定方法

JavaScript 中的方法`bind()`返回一个新函数，当调用这个函数时，它的`this`关键字被设置为一个特定的值。新返回的函数带有一个给定的参数序列，该序列位于调用它时提供的任何参数之前。

下面的例子说明了`bind()`方法的语法:

```
**fn.bind(thisArg[, arg1[, arg2[, ...]]])**
```

在这个语法中，方法`bind()`返回函数`fn`的副本，带有特定的`this`值(`thisArg`)和参数(`arg1`、`arg2`、…)。

# 使用 bind 方法进行绑定

方法`bind()`创建一个新的*绑定函数*，它是一个*外来函数对象*，包装了原来的函数对象。

让我们看看下面的例子:

```
const user = {
 name: "Mehdi",
 getName: function() {
  return this.name;
}
};const unboundFunc = user.getName;
console.log(unboundFunc()); 
// The function gets invoked at the global scope
// expected output: undefined
```

如您所见，`unboundFunc`返回的是`undefined`而不是`Mehdi`。这是因为`unboundFunc`是与用户对象(在全局范围内)分开调用和执行的，其中`this`的值与用户对象内`this`的值不同。

为了解决这个问题，我们需要使用方法`bind()`绑定函数`getName`。

下面的例子可以做到这一点:

```
const user = {
 name: "Mehdi",
 getName: function() {
 return this.name;
}
};const unboundFunc = user.getName;
console.log(unboundFunc()); 
// The function gets invoked at the global scope
// expected output: undefinedconst boundFunc = **unboundFunc.bind(user)**;
console.log(boundFunc());
// expected output: Mehdi
```

在这种情况下，方法`bind`创建了一个新函数，当这个函数被调用时，它的`this`关键字被设置为对象`user`中`this`的值。这就是为什么我们得到名称`Mehdi`作为输出。

# 从不同的对象借用方法

假设我们有一个名为 Mehdi 的用户的对象`user1`,还有一个名为 John 的用户的对象`user2`。两个对象都有一个方法`getAge`。

看看下面的例子:

*用户 1:*

```
const user1 = {
  name: "Mehdi",
  getAge: function(age){
    return this.name + " is " + age + " years old."
  }
}
```

*用户 2:*

```
const user2 = {
  name: "John",
  getAge: function(age){
    return this.name + " is " + age + " years old."
  }
}
```

现在我们可以使用方法`bind()`将`getAge`从用户 2 借用到用户 1。这里有一个例子:

```
let user = **user1.getAge.bind(user2, 22)**;
console.log(**user()**);// output: **John** is 22 years old.
```

如您所见，方法`bind()`让我们能够借用一个对象的方法，而无需复制该方法并在两个不同的地方维护它。

# 结论

bind 方法是 JavaScript 的一个强大而有用的特性。它创建一个新函数，该函数将特定的`this`设置为所提供的值。除此之外，它还允许一个对象从另一个对象借用一个方法，而不用复制那个方法。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*下面的链接是另一篇有用的文章:*

[](https://medium.com/javascript-in-plain-english/5-useful-css-tips-every-web-developer-should-know-5c19a088620e) [## 每个 Web 开发人员都应该知道的 5 个有用的 CSS 技巧

### 作为一名 web 开发人员，你应该知道的一些 CSS 技巧。

medium.com](https://medium.com/javascript-in-plain-english/5-useful-css-tips-every-web-developer-should-know-5c19a088620e)