# 5 个伟大但鲜为人知的 JavaScript 特性

> 原文：<https://javascript.plainenglish.io/5-great-little-javascript-features-8bc2bec6dcb6?source=collection_archive---------4----------------------->

JavaScript 中有一些并不是每个人都知道的很棒的小特性。当我第一次开始使用它们时，我惊讶于它们是如此的酷和简单。我仍然很惊讶有多少前端开发者没有意识到这些的存在！

![](img/72e0cf38fdeccbdffb17f046da3803e7.png)

# 1 —数字分隔符

数字分隔符可用于提高可读性。考虑下面的代码行，当扫描过去时，你能很快看到它实际上是 10，000 吗？

```
let duration = 10000;
```

我们可以向数字添加数字分隔符，如下所示:

```
let duration = 10_000;
```

值不变，只是更容易阅读。

尝试一下:

# 2 —零化合并运算符(？？)和逻辑或(||)

多年来，我们已经习惯于在 C#等编程语言中这样做，但我们也可以在 Javascript 中这样做。

## 那个？？操作员

[？？当左边的**为空或未定义时，运算符**](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)返回右边的操作数。

```
leftExpr ?? rightExpr
```

示例:

```
console.log(null ?? 'some default value');// expected output:
// 'some default value'let xx; // leave this undefined
console.log(xx ?? 'some default value');// expected output: 
// 'some default value'
```

尝试一下:

## ||运算符

[逻辑 OR 运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)几乎与？？接线员。这里真正的区别是左边可以是 **null，undefined，NaN，0 或者空字符串。人们倾向于用这个来设置默认值。**

```
leftExpr || rightExpr
```

示例:

```
console.log(null || 'some default value');
// expected output : 'some default value'let xx; // leave this undefined
console.log(xx || 'some default value');
// expected output : 'some default value'console.log(0 || 'some default value');
// expected output : 'some default value'console.log('' || 'some default value');
// expected output : 'some default value'console.log(-1 || 'some default value');
// expected output : -1console.log('real' || 'some default value');
// expected output : 'real'
```

尝试一下:

# 3-扩展语法(…) {…}

spread 语法是一个强大的工具，有助于编写简洁的代码。如果你用过 React，那么你可能已经遇到过这种情况。

## 将对象的特性提取到新特性中

假设你有一个复杂的对象，你只对这个对象的两个属性感兴趣。您可以通过以下方式根据您想要的属性声明新的变量

## 从数组中提取项目

同样，你可以用上面的方法来析构一个对象，你也可以用数组来这样做。

## 合并对象

您可以使用 spread 语法来组合对象。在 jQuery 中，我们通常使用$。extend()但是随着 jQuery 的逐渐消亡，我们可以在浏览器中直接使用这个方法。

```
const destinationObject = {...baseObject, ...sourceObject};
```

例如，查看输出如何显示 cat 被新值“meeeeeeow”覆盖的所有默认值:

## 克隆对象

Javascript 中的对象是引用类型。如果你设置 object2 = object1，你将拥有同一个对象两次。这意味着如果您更新对象 2 上的属性，它也会更新对象 1 上的属性。

下面的代码将 object2 设置为 object1，然后更新 object2 的属性并输出每个对象的值。您将看到每个对象的输出是相同的。

那么，你想克隆这个物体？。我见过很多这样的方法，包括序列化为 JSON，然后反序列化回一个对象。

使用扩展语法，您现在可以像这样克隆一个对象:

```
const object2 = {...object1};
```

如下所示，每个对象的输出是不同的:

# 4-可选链接(？。)

我们可以用？。如果某个值为空或未定义，则停止求值并将其短路。

例如，下面的代码引发一个错误(无法读取 undefined 的属性“sound”):

```
const someObject = {
  cat: {
    sound: 'meow'
  },
  dog: {
    sound: 'woof'
  },
  duck: {
    sound: 'quack'
  }
};console.log(someObject.duck.sound);
// expected : 'quack'console.log(someObject.elephant.sound);
// expected : Uncaught TypeError: Cannot read property 'sound' of undefined
```

我们可以通过添加？。操作员:

```
const someObject = {
  cat: {
    sound: 'meow'
  },
  dog: {
    sound: 'woof'
  },
  duck: {
    sound: 'quack'
  }
};console.log(someObject.duck?.sound);
// expected : 'quack'console.log(someObject.elephant?.sound);
// expected : undefined
```

尝试一下:

这也可以用于对象上的函数，而不仅仅是属性。为此，您需要添加。。在()之前，如下图所示

```
myobject.someMethod?.()
```

在这个例子中，我检查属性是否存在，函数调用是否存在。只有第一个会执行。

```
const someObject = {
  cat: {
    sound: 'meow',
    doSomething:() => console.log(true)
  },
  dog: {
    sound: 'woof',
  },
  duck: {
    sound: 'quack',
    doSomething:() => console.log(true)
  }
};someObject.duck?.doSomething?.();
// expected : truesomeObject.dog?.doSomething?.();
// expected : NOTHINGsomeObject.elephant?.doSomething?.();
// expected : NOTHING
```

尝试一下:

# 5-通过[括号]符号访问对象属性(和方法)

这已经存在很长时间了，但是我仍然和那些没有意识到他们可以使用这种技术的开发者交谈。

当然，我们可以通过属性名来访问属性，但是有时我们需要将正在访问的属性存储在配置中，并动态地访问它。这就是括号符号的由来。

下面的代码使用传统访问器访问对象的 cat 属性，然后使用括号符号访问器。

我们还可以使用 Object.keys 获得对象的属性列表。

此外，我们可以用 for 迭代属性...在:

希望你在这里学到了一些新东西，或者用不同的方式思考了一些事情。或者你已经知道这些事情了。JavaScript 中有很多很酷的东西，在过去的几个版本中，它已经真正成长为一门语言。我不认为已经使用了几十年的开发者意识到了 JavaScript 现在所有的新特性。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)