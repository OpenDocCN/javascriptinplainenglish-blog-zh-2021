# JavaScript 中的“this”关键字

> 原文：<https://javascript.plainenglish.io/the-this-keyword-in-javascript-93090abf261b?source=collection_archive---------4----------------------->

![](img/b6af92db870b48d2931b17f404d438ed.png)

JavaScript 中最被误解的特性在其他语言中被视为基础知识。即使花了一整天阅读关于其内部工作的书籍和教程，关键字仍然是一个令人困惑的话题。

我们不是不知道那是什么，我们知道。但是当我们需要将知识付诸实践的时候，我们总是会错过一些东西。

> “这个”以前是这个，但“这个”现在是那个

混乱和误解是这四条规则的原因。虔诚地追随他们，你就永远不会成为“这个”的疯狂的牺牲品。规则如下:

1.  默认(全局)绑定规则。
2.  隐式绑定规则。
3.  显式绑定规则
4.  用`new`调用构造函数

我的建议是:把这些规则写在便利贴上，放在你的桌子旁边。

在我们开始探索之前，让我们稍微解释一下为什么“这”是错误的。

# 困惑

当你写一段代码时，你的心理模型总是以**创建时间**为中心。创建时间是创建/编写这段代码的时期。JavaScript 还有另一个叫做**执行时间**的周期，它解释你写的东西。

绑定、引用和内存分配都是在执行时完成的。这是意料之中的——在大多数编程语言中，这是一种相互行为。

JavaScript 的问题在于，在运行时(执行)，它根据上下文绑定值。这意味着一个逻辑不一定按照它被(用户)写或读的方式来解释，而是基于所谓的它的**执行上下文**。

# 执行上下文

让我给你一个执行上下文的例子。

你有三个保安机器人每天晚上在你的社区巡逻。说机器人 A、B、C，晚上 9 点到 11 点，机器人 A、B 在值班，C 在充电。晚上 11 点，C 充满电，代替 a，现在我们有 B 和 C 值班。这种转换以 2 小时的间隔持续进行。

假设在执勤(执行)时，两人需要互相交流对方的位置和检查区域。在第一轮，A 和 B 在交流。当 A 被 C 取代时，A 不会继续与 B 通信；相反，它应该与 c。

执行上下文已更改，环境不再相同。在切换之后，A 不能与 B 交谈，但是 c 理解 A 不应该再与 B 交谈，这是我们对“this”关键字感到困惑的地方。

`this`可以看作是我们的机器人发现自己所处的现状。

现在你知道为什么它总是让你困惑，让我们来看看避免困惑的四条规则。

# 规则 1:默认(全局)绑定

首先，仔细查看以下示例，并猜测可以记录到控制台的内容。请随意误解:

```
// 1A
function printName() {
  console.log(this.name);
}var name = 'Scotch';printName();
```

记住答案，然后试着猜一猜这个:

```
// 1B
function printName() {
  'use strict';
  console.log(this.name);
}var name = 'Scotch';printName();
```

让我们分析一下:

当不在严格模式下时，这是指全局范围。在严格模式下，其绑定是未定义的。

**Ex 1A** 将在控制台上打印“Scotch”，因为“this”指的是全局默认绑定。

在 **Ex 1B** 中，“this”也可以指全局对象，但是因为“use strict”，它默认为`undefined`。`use strict`确保`this`的范围是功能范围，不是全局范围。

# 规则 2:隐式绑定

如果函数没有暴露给全局上下文，该怎么办？您对以下几点有什么看法？

```
var company = {
  name: 'Google',
  printName: function printName() {
    console.log(this.name);
  }
};var name = 'Scotch';company.printName();
```

这一次，这是保留对封装其包装功能的对象的引用。因此，规则规定-“这”是指包含在对象中的调用点。

标记“呼叫中心”字样。这条规则没有说“写站点”，而是说“呼叫站点”。上面的示例将打印“Google”，但是不要指望下面的示例打印相同的内容:

```
var company = {
  name: 'Google',
  printName: function printName() {
    console.log(this.name);
  }
}var name = 'Scotch';company.printName();  // Google// print name call site
// won't be the object
// but global
var printNameAgain = company.printName;printNameAgain(); // Scotch
```

本示例打印“Scotch”而不是“Google”，因为呼叫站点不是对象，而是全局对象。记住我们的安全机器人插图；执行环境才是最重要的。

# 规则 3:显式绑定

如果我们希望`printNameAgain`引用`company`对象，即使调用上下文不是`company`对象而是`global`对象？

显式绑定规则:

您可以使用`call`、`apply`或`bind`显式操作呼叫中心。

我们可以手工使`printNameAgain`引用`company`对象作为它的调用点:

```
var company = {
  name: 'Google',
  printName: function printName() {
    console.log(this.name);
  }
}var name = 'Scotch';var printNameAgain = company.printName;printNameAgain.call(company);
```

通常，当我们调用`printNameAgain`时，它引用了全局对象，但是我们现在使用`call`方法来硬绑定`company`作为它的执行上下文。

# 参数呢？

当函数有参数时，您可以在上下文之后传入:

```
var company = {
  name: 'Google',
  printName: function printName(prefix, suffix) {
    console.log(prefix + this.name + suffix);
  }
}var name = 'Scotch';var printNameAgain = company.printName;// hard bind company to printNameAgain
printNameAgain.call(company, 'Hi ', '!!');
```

printName 函数需要一个`prefix`和`suffix`参数。当用`call`调用传递的函数(`printNameAgain`)时，我们在`company`对象绑定后传入参数。

`apply`方法允许您以数组的形式传递参数:

```
printNameAgain.call(company, ['Hi ', '!!']);
```

最后一个是`bind`。它的作用与`call`和`apply`略有不同。`call`和`apply`执行功能，而`bind`不像它们那样。`bind`所做的是*绑定*正确的上下文并返回带有调整后的上下文的函数:

```
var printFunc = printNameAgain.bind(company);
```

然后，您可以在需要时调用返回的函数:

```
var printFunc('Hi ', '!!');
```

# 规则 4:用新的

每当看到用`new`关键字调用的函数时，最后一条规则就会浮现出来:

关键字`new`在一个链接到原型对象的函数中创建一个虚拟对象。如果这个虚构的对象中没有现有的 return 语句，它将由函数隐式返回。

让我们以尽可能简单的方式来分解它。

如果我有以下功能:

```
function Company() {
  this.name = 'Scotch'
}
```

然后尝试用 new 调用该函数:

```
new Company();
```

以下评论理想地展示了内部发生的情况:

```
function Company() {
  // var this = {};
  this.name = 'Scotch'
  // return this;
}
```

创建一个名为`this`的虚拟对象，如果函数没有返回任何内容，则返回`this`。因此，您可以将函数调用用作对象:

```
var companyInstance = new Company();console.log(companyInstance.name) // prints Scotch
```

该规则还规定该对象链接到原型对象。原型链接超出了本文的范围，但是如果我们看到一个这样的链接的例子，也不会有什么坏处:

```
function Company() {
  this.name = 'Scotch'
}Company.prototype.getName = function() {
  return this.name;
}var companyInstance = new Company();
console.log(companyInstance.getName()); // Scotch
```

我们只是给公司的原型对象附加了一个方法`getName`。该方法可以访问在`Company`中创建的同一个`this`对象。

**提示**:用`new`关键字调用的函数称为**构造函数**，通常用大写字母书写，而用`new`关键字调用的函数称为**构造函数调用**。

# 优先顺序

重要的是要注意这些规则是按照优先顺序应用的。这意味着如果在同一个场景中发现两个或更多的规则，它们的应用是有顺序的。内容如下:

1.  构造函数调用(规则 4)
2.  显式绑定(规则 3)
3.  隐式绑定(规则 2)
4.  默认绑定(规则 1)

正如你所看到的，仅仅颠倒规则就显示了它们的优先顺序。

# 常见陷阱:异步处理

`this`绑定有一些已知的缺陷。它们在接收回调作为处理程序的异步逻辑中最受关注。这些处理程序有时被绑定到不同的上下文，使得`this`的行为出乎意料。

事件处理就是这样一种情况。事件处理程序是传递给事件注册的回调函数。当事件被触发时，这些回调函数在运行时执行。下面是一个基本的例子:

```
button.addEventListener('click', function() {
  console.log('clicked')
});
```

浏览器需要给出一些关于事件的上下文信息。它通过绑定到函数中的`this`来做到这一点。因此，您可以从关键字:

```
button.addEventListener('click', function() {
  console.log(this)
});
```

这是预期的行为，直到您需要从外部上下文访问`this`。参见:

```
var company = {
  name: 'Scotch',
  getName: function() {
    console.log(this.name)
  }
}// This event's handler will throw an error
button.addEventListener('click', company.getName)
```

点击事件处理程序是`company`对象中的一个方法。正如我们已经提到的，事件处理程序有自己的`this`绑定，但是我们需要通过`this`访问`company`。运行上面的示例将抛出一个错误，告诉您无法读取`name`属性。更糟糕的是，`name`属性存在于事件的`this`属性上，从而产生奇怪的结果，甚至不会抛出错误。

要解决这个问题，我们需要手动绑定上下文:

```
var company = {
  name: 'Scotch',
  getName: function() {
    console.log(this.name)
  }
}// bind getName's context as 'company'
button.addEventListener('click', company.getName.bind(company))
```

# 结论

对，就是这样。这就是`this`的作用，仅此而已。下次您遇到代码示例时，不要坐立不安，因为它保存着关于正在运行的(不是编写的)代码的上下文信息。

要对此进行调试，请避免从代码编辑器中对其进行推理。打开浏览器，在遇到断点的地方添加断点。这样，您将确切地了解到一个`this`绑定正在存储什么，以及这些值可能来自哪里。

希望你喜欢。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)