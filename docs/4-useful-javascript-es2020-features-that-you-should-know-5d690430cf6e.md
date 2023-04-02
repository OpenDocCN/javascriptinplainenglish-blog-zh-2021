# 您应该知道的 4 个有用的 JavaScript ES2020 特性

> 原文：<https://javascript.plainenglish.io/4-useful-javascript-es2020-features-that-you-should-know-5d690430cf6e?source=collection_archive---------3----------------------->

## 您应该知道的强大 ES2020 功能。

![](img/064b80950d70df6404737d10c5b7a75c.png)

Image created with ❤️️ By author.

JavaScript 是当今强大的编程语言，尤其是在 web 开发中。你可以用它创造很多有用的东西。感谢 ECMAScript 版本，每年我们都会获得新的有用的 JavaScript 特性，使得编码过程变得更加容易。

ES2020 为 JavaScript 开发者带来了许多有用且有趣的特性。在本文中，我们将了解一些您应该知道的 ES2020 特性。所以让我们开始吧。

# 1.globalThis

这不是 ES2020 的一大特色，但在我看来很有用。这只是一种总是引用全局对象的方式。

大家知道，在浏览器中，全局对象指的是`window`。例如在 NodeJS 中，有一个对象`global`。在网络工作者中，有`self`。所以这个特性`**globalThis**` 允许我们无论在什么类型的环境下都可以引用正确的全局对象。

这是一个在所有环境中都有效的通用全局的好方法。希望我解释清楚了。

这里有一个例子:

```
//In the browser:
console.log(**globalThis**);
// Output: Window {0: Window, 1: global, window: Window, self: Window, document: document, name: "", location: Location, …} //In NodeJS:
c**onsole.log(globalThis);** //returns the global object(global)
```

# 2.Promise.allSettled 函数

当我们有多个承诺时，使用`**Promise.allSettled()**`功能。检查是否所有的承诺都已解决是很有用的，这意味着所有的承诺都被解决或拒绝。

函数`allSettled()`将一组承诺作为参数。它以数组的形式返回一个新的承诺，包含我们传递给它的每个承诺的所有状态。

看看下面的例子:

```
const promise1 = new Promise((resolve, reject) => {
  resolve('The Promise number 1 was resolved')
})const promise2 = new Promise((resolve, reject) => {
  reject('The Promise number 2 was rejected')
})const promise3 = new Promise((resolve, reject) => {
  resolve('The Promise number 3 was resolved')
})// Using allSettled().
**Promise.allSettled([promise1, promise2, promise3])**
 .then(result => console.log(result))
 .catch(err => console.log(err))//output:
[
  {status: "fulfilled", value: "The Promise number 1 was resolved"},
  {status: "rejected", reason: "The Promise number 2 was rejected"},
  {status: "fulfilled", value: "The Promise number 3 was resolved"}
]
```

# 3.可选链接

当您有一个包含其他嵌套对象的大对象，并且想要检查该对象上的某些属性是否可用而不出现错误时，可选链接非常有用。

可选链接`**?.**`用于检查`**?.**`之前的值或属性是`null`还是`undefined`。如果是，则返回`undefined`。否则，它只返回值。

```
const user = {
  name: "Mehdi",
  age: 19,
}user.car.model;//Error.
**user?.car?.mode**l; //undefined (no error).
**user?.age**; //19
```

您还可以对对象方法使用可选的链接。您只需要在调用方法时在括号前添加操作符`?.`。

看看下面的例子:

```
const person = {
  name: "Mehdi",
  age: 19,
  fullName(){
   return "Mehdi Aoussiad";
  }
}person.**lastName()**; //Error.
person.**lastName?.()**; //undefined(no error).
person.**fullName?.()**; //Mehdi Aoussiad
```

因此，如果函数或属性存在，可选链接允许我们总是得到正常的输出。如果它们不存在，我们得到的是`undefined`而不是一个错误。

# 4.BigInt

如果你想处理大量的数据，这是一个非常有用的特性。在 JavaScript 中，可以处理的数量是有限制的。

在功能`BigInt`出现之前，我们无法超过这个数量限制。但现在我们可以超越这一点。

下面是一个例子:

```
//largest integer in JavaScript
let max = **Number.MAX_SAFE_INTEGER;**console.log(**max**); *// Output:* 9*007199254740991*//check the type of max.
console.log(typeof max); //number//try to add and increase the integer(max)
++max; //output: 9007199254740992++max; //output: 9007199254740992++max; //output: 9007199254740992 //create BigInt
let bigOne = **BigInt(max);** console.log(**bigOne**); //9007199254740991n//check the type of bigOne.
console.log(**typeof bigOne**); //bigint (not number)//try to increase
**++bigOne;** //9007199254740992n **++bigOne;** //9007199254740993n
**++bigOne;** //9007199254740994n
```

如您所见，通过使用构造函数`BigInt()`，我们可以超越 JavaScript 中的最大整数。因此，该功能为您提供了另一种类型的数字(`bigInt`类型)来使用。

# 结论

正如您所看到的，作为一名 JavaScript 开发人员，了解所有这些 ES2020 特性非常有用。我们没有涵盖 ES2020 中的所有功能，但现在我们知道了重要的功能。

谢谢你阅读这篇文章。我希望你发现它有用。

**继续阅读**

*如果你对 JavaScript 和网络开发相关的更有用的内容感兴趣，你可以* [*订阅*](https://mehdiouss.ck.page/) *我的时事通讯。*

*您也可以选择:*

[](/error-handling-in-javascript-explained-with-examples-bab0868ed879) [## 用例子解释 JavaScript 中的错误处理

### 了解 JavaScript 中错误处理的基础知识。

javascript.plainenglish.io](/error-handling-in-javascript-explained-with-examples-bab0868ed879) 

[*更多内容参见*](http://plainenglish.io/)