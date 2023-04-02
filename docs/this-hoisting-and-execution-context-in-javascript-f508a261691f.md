# JavaScript 中的提升和执行上下文

> 原文：<https://javascript.plainenglish.io/this-hoisting-and-execution-context-in-javascript-f508a261691f?source=collection_archive---------16----------------------->

![](img/1fd576e0424bbb50922fd1993a24faf1.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 这

如果你一直在学习 JavaScript，你可能会碰到“这个”几次，通常会有一个简单的解释，然后是类似“不要担心它是如何工作的，以后会更有意义”的内容。现在是稍后，这是什么？

***This:*** *一个执行上下文(全局、函数或 eval)的属性，在非严格模式下，总是对一个对象的引用，在严格模式下可以是任意值。* [-MDN 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)

要理解这意味着什么，你必须理解 JavaScript 如何执行代码。让我们从对这一点的基本理解、这一点的不同示例以及手动设置这一点的值开始，然后我们将继续执行上下文，最后是提升。

解释 MDN 引用的一个更简单的方法是，对于函数来说，它的值是调用它的上下文，对于事件侦听器来说，它是侦听器所附加的元素，对于方法来说，它是拥有该方法的对象。

```
function returnThis () {
  return this
}
```

在这个例子中，调用 return 这将返回窗口对象(在浏览器中),因为函数是在全局上下文中声明的，因此属于全局对象，这意味着它没有在另一个函数或对象中声明。

```
class WhatIsThis {
  returnThis () {
    return this
  }
}
let test = new WhatIsThis
```

在此示例中，test.returnThis()返回“test”引用的 what is 的实例，因为 what is 是拥有 returnThis()方法的对象。

```
function log () {console.log(this)}const button = document.querySelector('button');buttons.addEventListener('click', log);
```

对于这个例子，假设我们有一个网页，其中包含一个带有事件监听器的按钮，事件监听器在被触发时调用日志功能。你用我做的这个 [codepen](https://codepen.io/SVRourke/pen/ZEBxRRo) 试试，你会看到按钮 DOM 元素在按钮被按下的时候被记录到控制台。这是因为事件侦听器中的值是侦听器所附加的元素，但是，如果我们不使用事件侦听器而直接在控制台中运行 log()，它将返回窗口对象。这是因为函数中的这个值是由调用它的上下文决定的，这意味着当在事件侦听器中调用 log()时，log 中的这个值就是 DOM button 元素！

```
function external () {
  return this.name
}let person = {
  name: "Sam",
  age: 27
}let sam = external.bind(person)console.log(sam())
```

此代码示例显示了如何使用？bind()，使用 a.bind(b)将返回一个新函数，其主体和作用域与 a 相同，但与 b 中的相同。在此代码示例中，我们定义了返回 this.name 的函数 external，如果 external 按原样调用，它将返回一个空字符串。我们还创建了一个具有两个属性的对象“person ”:姓名和年龄。接下来，我们使用 bind()创建一个名为 sam 的新函数，该函数使用 this of person 和函数 external。通过调用 sam()，您将看到返回了 person 对象的 name 属性。

# 执行上下文

当你运行一个脚本时，你可能会认为 JavaScript 引擎一行一行地运行你的代码，同时执行代码，然而这是不正确的，因为 JavaScript 引擎分两个阶段运行:创建和执行。

```
const myName = 'Sam';function greet (name) {
  return `Hello ${name}`;	
}
const greetSam = greet(myName);console.log(greetSam)
```

我们将像 JavaScript 引擎一样一步一步地浏览这段代码。当您第一次执行这个脚本时，JavaScript 创建第一个执行上下文，全局执行上下文并将其绑定到关键字 this，它还为变量 myName 和 greetSam 以及 greet()的函数声明分配内存，但是它将变量存储为未定义。

在创建阶段之后，JavaScript 转到执行阶段，在那里它给变量赋值并执行函数调用。每当 JavaScript 调用一个函数时，它都会为该函数创建新的执行上下文，再次经历每个新上下文的创建和执行阶段，将结果值返回给全局执行上下文，该上下文继续执行剩余的代码。为了在进入执行阶段后继续我们的示例，JavaScript 引擎将:

1.  将字符串“Sam”赋给变量 myName。
2.  为 greetSam 中 greet()的调用创建一个新的执行上下文
3.  执行 greet()调用的上下文
4.  将 greet()的结果返回给全局执行上下文。
5.  将返回值赋给变量 greetSam
6.  将 greetSam 的值记录到控制台

# 提升

提升是一种将 JavaScript 构建执行上下文的方式概念化的方式，这种方式会影响代码执行期间变量和函数何时可用。在执行代码之前，创建阶段将所有变量和函数放入内存的方式，使所有变量和函数声明看起来好像都被“吊”到了文件的顶部，例如:

```
greetUser()function greetUser () {
  console.log('Hello')
}
```

在本例中，greetUser()函数在编写之前就被调用了，您可能会直觉地认为这会导致错误，但是在创建阶段，greetUser 声明是在调用执行之前被挂起的。

仅悬挂声明:

```
console.log(x) // Undefined
var x;         // Declaration// let & const not hoisted, cannot reference before init
// const must have initializer in declaration
console.log(y) // ReferenceError
let y = 6;     // Declaration and Initialization NO HOIST
```

对 JavaScript 执行代码的方式有了基本的了解，代码提升应该是一个相当简单的概念。

# 结论

希望这篇文章能帮助一些人更好地理解这个，提升，和 JavaScript 代码执行，我知道它肯定对我有帮助。

如果你喜欢我的写作，请随意查看我的网站，并在 T2 的 LinkedIn 上与我联系

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)