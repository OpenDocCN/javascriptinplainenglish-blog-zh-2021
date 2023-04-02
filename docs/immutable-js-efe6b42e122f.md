# 不可变. js 快速介绍

> 原文：<https://javascript.plainenglish.io/immutable-js-efe6b42e122f?source=collection_archive---------12----------------------->

## 以及 JavaScript 中不变性的含义

![](img/11c60bd53c5828f224ae76e9bdb2b401.png)

Screenshot by the author from [immutable-js.com](http://immutable-js.com)

我认为不变性是最容易被误解的概念之一——尤其是对于 JavaScript。然而，这并不困难。

在[维基百科](https://en.wikipedia.org/wiki/Immutable_object)上，是这样定义的:

> […]不可变对象(不可改变的对象)是一个对象，它的状态在创建后不能被修改。

不变性？在 JavaScript 中，我们有 const 关键字，对吗？嗯，没那么容易。我们来举个例子。

```
const person = "Max"
person = "Tim" 
// error! 
```

这将抛出一个错误，因为我们将 *person* 定义为一个常量。我们不能重新分配用`const`声明的变量。这就是问题的关键:许多人认为这是不变性——他们错了。

不能重新赋值并不意味着它是不可变的。
下面是另一个例子:

```
const person = { name: "Max", age: 25 }
person.name = "Tim"console.log(person) // { name: "Tim", age: 25 }
```

如果`const`可以保证不变性，我们就不能改变这里的`name`属性。但事实正好相反:运行代码会非常好。

对象 person 现在包含“Tim”作为名称——我们改变了我们的对象，尽管我们使用了 const 关键字。然而，重新分配变量的以下代码不起作用:

```
const person = { name: "Max", age: 25 }person = { name: "Karl", age: 22 }
```

**const-keyword 只防止重分配，不防止变异。**

这就是为什么我们的物体可以如此容易地变异。为了使它完整，JavaScript 中任何不是原始类型的东西都可以变异。JavaScript 中的基本类型有字符串、数字、布尔等等。

其他所有东西，像数组甚至函数，基本上都是对象——正如我们刚刚学到的，它们可以在 JavaScript 中变异。

我想你现在明白不变性到底是什么了。

# 试图使我们的对象在普通 JS 中不可变

好的，我们的目标是让我们的对象不可变——因为数组、集合、映射等等也是对象，我也指的是一般意义上的对象。

## 第一种方法—控制属性访问

说实话，我知道这个功能还没那么久。当手动定义对象的属性时，我们可以控制它是否可写。

下面是例子。正如我们之前所学的，我们可以简单地改变一个对象的属性。让我们让老好人马克斯再高一点。

```
const person = { name: “Max”, age: 25, height: 5.9 }person.height = 6.1
```

这没有任何问题——高度属性现在是 6.1。如果我们想避免改变值的可能性，我们可以将属性设置为 writable: false。以下是方法:

```
const person = { name: “Max”, age: 25, height: 5.9 }Object.defineProperty(person, “height”, {
  writable: false
})person.height = 6.1
```

现在，`person.height`仍然是 5.9——即使我们试图改变属性，它也不会工作。然而，也没有警告(在严格模式下，它会导致错误)。变异根本不起作用。

这种方法有点麻烦。尤其是因为我们只能让对象的一个属性不可变。如果我们想让所有的属性都不可变，我们就必须遍历所有的属性。当然，有更好的方法。

## 第二种方法——冻结物体

早些时候，我们禁止进入个人财产。但是在 defineProperty()旁边，还有一个函数，使得整个对象不可变。

再说一次，麦克斯是我们的小白鼠。

```
const person = { name: “Max”, age: 25, height: 5.9 }Object.freeze(person)person.height = 6.1
```

身高属性仍然是 5.9——同样，改变年龄或名字也不起作用。如你所见，我们成功地冻结了这个物体。此外，添加新的属性不再可能。

无论如何，当试图改变任何东西时，都会导致错误，但只是在严格模式下。

# 不可变的. js——也许是更优雅的解决方案

不可变的. js 是一个非常著名的 JavaScript 库，帮助我们实现不变性。然而，图书馆经常被误解。首先，重要的是理解一切都围绕着地图和列表——即使是“普通”的对象，比如我们的*人物*，也被视为这些数据结构。

不过，我们不要急着做任何事。首先，我们需要用`npm install immutable`安装它。那我们就可以走了。

基本上，有两种方法可以将我们的 person-object 从普通的 JavaScript 转换成不可变的. js 对象，顾名思义，不可变的。

首先，我们可以把它定义为“从无到有”:

```
const { Map, fromJS } = require("immutable") const personIm = Map({ name: "Max", age: 25, height: 5.9 })
```

如您所见，我们只是使用 Immutable.js 的 Map 来包装我们的对象。

第二种方法是，将我们的 plain-js 对象转换成 Immutable.js 对象:

```
const person = { name: "Max", age: 25, height: 5.9 }const personIm = fromJS(person)
```

两者导致相同的结果。当我们想得到一个属性的值时，现在情况有点不同了。

您可能已经注意到，在创建不可变的. js 对象的第一种方法中，我们使用了库的 Map-object。当我们使用`fromJS`时，我们也接收到了 Map-object。顾名思义，它基本上像我们从普通 JavaScript 中了解的`map`一样工作。为了得到一个属性的值，我们写:

```
personIm.get("name") // "Max"
```

要更改属性的值，有一个`set`函数。但是由于我们的对象是不可变的，下面的代码不应该改变我们的对象:

```
const person = { name: "Max", age: 25, height: 5.9 }const personIm = fromJS(person)personIm.set("name", "Carl")console.log(personIm.get("name")) // "Max"
```

厉害！我们的人-物现在是不变的。当我们试图改变它时，什么也没有发生——也没有错误。原因很简单:这是被通缉的行为。实际上，当试图改变我们的对象时，会发生一些事情。但这不是要改变原来的物体。

> **试图改变一个不可变的对象，并不会改变这个对象——它会创建一个改变的副本**

当我们稍微修改一下代码时，我们可以更好地看到这一点:

```
const personCopy = personIm.set("name", "Carl")console.log(personIm.get("name"))     // "Max"
console.log(personCopy.get("name"))   // "Carl"
```

如您所见，试图改变对象会创建一个副本。这就是 Immutable.js 的全部哲学——同样，当我们想给对象添加一个新属性时，它会返回一个新属性。

这不仅适用于 Immutable.js 中的`Map`对象，也适用于它提供的其他数据结构——例如，Set 或 List。甚至`delete`或`update`函数也不会改变原始对象。

它们总是返回原始对象的修改过的副本。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)