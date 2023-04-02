# JavaScript 中的原语类型是什么？

> 原文：<https://javascript.plainenglish.io/what-are-primitive-types-in-javascript-671909def6ca?source=collection_archive---------4----------------------->

## JavaScript 中有 6 种原始类型(或“原始数据类型”):数字、字符串、布尔、bigints、符号和`undefined`。

![](img/6a95201d8f95b486cbd90c258f3c9279.png)

Photo by [Ellen Auer](https://unsplash.com/@ellenauer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 基本类型不是 JavaScript 对象。

JavaScript 中的一个基本概念是对象(属性集合)和基本类型之间有区别。

> “在 [JavaScript](https://developer.mozilla.org/en-US/docs/Glossary/JavaScript) 中，**原语**(原语值，原语数据类型)是不是[对象](https://developer.mozilla.org/en-US/docs/Glossary/object)并且没有[方法](https://developer.mozilla.org/en-US/docs/Glossary/method)的数据。”— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)

JavaScript 中有 6 种基本类型:

1.  [琴弦](https://medium.com/javascript-in-plain-english/how-to-check-for-a-string-in-javascript-a16b196915ff)
2.  [布尔型](https://medium.com/javascript-in-plain-english/how-to-check-for-a-boolean-in-javascript-98fdc8aec2a7)
3.  [数字](https://medium.com/javascript-in-plain-english/how-to-check-for-a-number-in-javascript-8d9024708153)包括`[NaN](https://medium.com/coding-in-simple-english/how-to-check-for-nan-in-javascript-4294e555b447)`(“非数字”)
4.  比根茨
5.  [符号](https://medium.com/p/30c3f294ea65)
6.  `[undefined](https://medium.com/coding-at-dawn/how-to-check-for-undefined-in-javascript-bcedd62c8ad)`

值`[null](https://medium.com/javascript-in-plain-english/how-to-check-for-null-in-javascript-dffab64d8ed5)`基本上也是一个原语，但是由于技术原因(我将在后面解释),它不被认为是原语。

基本类型的概念可能会令人困惑，因为我们实际上可以像访问对象一样，在 JavaScript 中直接访问基本数据类型的属性和方法。

例如，字符串有一个`.length` ( `[String.prototype.length](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/length)`)属性。然而，字符串不是对象——它们是原语。

JavaScript 提供了某些助手(在本例中，在[的](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String) `[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)` [](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)原型上)，但是字符串本身是[不可变的](https://developer.mozilla.org/en-US/docs/Glossary/Immutable)。

> 所有原语都是**不可变的**，即它们不能被改变。重要的是不要把原语本身与被赋予原语值的变量混淆。可以给变量重新分配一个新值，但不能像改变对象、数组和函数那样改变现有值— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)

您通常会听到与原语一起使用的单词“突变”(意味着变化)或“可变性”(被改变的能力)。

与您可以`.push()` ( `[Array.prototype.push()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/push)`)向其添加新项目的数组或可以使用`[.](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors)`[属性访问器](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_accessors)添加新对象键的对象不同，您不能改变基本类型。

换句话说，没有像数组那样的基元的“赋值方法”，数组有像`.sort()` ( `[Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)`)这样的方法来改变数组。

当我们在一个字符串上调用`.toUpperCase()` ( `[String.prototype.toUpperCase()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase)`)时，我们得到一个新的字符串——但是现有的字符串永远不会改变。这就是基本类型的定义。

赋给变量名的内容(使用`[let](https://medium.com/javascript-in-plain-english/how-to-use-let-var-and-const-in-javascript-cdf42b48d70)` [、](https://medium.com/javascript-in-plain-english/how-to-use-let-var-and-const-in-javascript-cdf42b48d70) `[var](https://medium.com/javascript-in-plain-english/how-to-use-let-var-and-const-in-javascript-cdf42b48d70)` [或](https://medium.com/javascript-in-plain-english/how-to-use-let-var-and-const-in-javascript-cdf42b48d70) `[const](https://medium.com/javascript-in-plain-english/how-to-use-let-var-and-const-in-javascript-cdf42b48d70)`关键字定义)是否可以改变，与是否可以改变一个基本类型是不同的问题。

例如，如果您定义了`const x = 2`，那么`x`不能被赋予新的值，因为它是用`const`定义的。

然而，如果你定义一个对象`y`为`const y = {}`，那么`y`不能被赋予一个新值，但是它的内容可以被改变。

对象是**可变的**，而原语是**不可变的**。

# 基本类型有基本包装对象。

我们获得这些助手属性的原因是因为在 JavaScript 中“包装”原始类型的[原型对象](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)。

> “除了`null`和`undefined`之外，所有的原始值都有环绕原始值的对象等价物:
> 
> `[String](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)`为字符串原语。
> 
> `[Number](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number)`为数本原。
> 
> `[BigInt](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/BigInt)`为 bigint 原始人。
> 
> `[Boolean](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean)`为布尔原语。
> 
> `[Symbol](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol)`为象征原始人。”— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Primitive#Primitive_wrapper_objects_in_JavaScript)

这里要记住的重要一点是，你永远不需要自己引用那些对象包装器。

JavaScript 在幕后自动将任何原语包装在对象包装器中，让您可以访问原型。

如果您需要取回原始值本身，有一个名为`valueOf()` ( `[Object.prototype.valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)`)的 helper 方法。

> "包装器的`[valueOf()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/valueOf)`方法返回原始值."— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Primitive#Primitive_wrapper_objects_in_JavaScript)

你可以想象在一个原语上调用`valueOf()`总是会返回原语本身。在实践中，它没有太多用处，但是如果你能理解`valueOf()`发生了什么，那么你就会理解基本类型的对象包装概念。

每当您访问基元值的任何属性或方法时，这些相同的步骤都会在幕后发生:

1.  您有一个原始数据类型，例如`"string"`
2.  您可以在原语上使用`.`属性访问器
3.  JavaScript 自动包装原语
4.  您现在可以访问原型方法了
5.  `"string".valueOf()`永远是`"string"`

除了`undefined`之外，其他任何基元类型的过程都相同。现在让我们回到`null`，它一点也不原始。

# 为什么`null`不是一个原始数据类型？

鉴于`undefined`是一个原始类型，值`null`似乎是一个原始类型。

> “还有[空](https://developer.mozilla.org/en-US/docs/Glossary/null)，看似原始，其实对于每一个`[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)`都是一个特例:任何结构类型都是通过[原型链](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Inheritance)从`null`派生出来的。”— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/Primitive)

我们通常使用`null`来表示*故意的*无值。相比之下，`undefined`用于表示*无意的*无值(或尚未定义的值，如未知的对象属性)。

然而`null`实际上是所有物体的起源，想起来有点奇怪。我不会太担心，如果你把`null`归为原始生物，就不会有坏事发生。

如果你关心为什么`null`不是一个原语，当你[检查](https://medium.com/javascript-in-plain-english/how-to-check-for-null-in-javascript-dffab64d8ed5) `[null](https://medium.com/javascript-in-plain-english/how-to-check-for-null-in-javascript-dffab64d8ed5)`时，它实际上与整个`[typeof](https://medium.com/better-programming/how-to-check-data-types-in-javascript-using-typeof-424d0520a329)` bug 相关。

> "每个对象都是从`null`值派生的，因此`typeof`操作符为它返回`object`"— [MDN 文档](https://developer.mozilla.org/en-US/docs/Glossary/null)

`typeof null`是`"object"`，因为对于 JavaScript 中的每个对象，每个[原型链](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)实际上都从`null`开始。很困惑吧。

您可以在控制台中通过使用`[Object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)`制作一个“真正空的”对象来证明这一点，它将一个原型对象作为其参数。调用`Object.create(null)`使用`null`作为原型，产生一个没有从原型继承任何东西的对象。

实际上并没有一个很好的理由来创建一个真正的空对象，但是它解释了为什么`null`实际上不是一个基本类型。

JavaScript 中不能调用`Object.create(undefined)`，只能调用`Object.create(null)`。

相比之下，`Object.create(Object.prototype)`使用`Object.prototype`作为原型对象:正常行为。

`Object.prototype`对象是所有标准 JavaScript 对象的标准原型。它存在于全局`[Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)`对象中，当我们用对象字面语法(`{}`花括号)创建一个对象时，它在幕后使用。当我们用`new`关键字:`new Object()`调用`[Object()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/Object)`构造函数时，也会用到对象原型。

真的，把`null`当成原始人没问题。但是一些技术访谈可能想让你知道，`null`在技术上是 JavaScript 中所有原型的起源，*不是*原语。

# 不要对象包装原始类型

总结一下，幕后的对象包装器解释了为什么不在内置基本类型的构造函数中使用`new`关键字。

与`[Date()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date/Date)`构造函数一样，JavaScript [构造函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/constructor)与`[new](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)`[关键字](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/new)一起用于创建该类型的对象。

当您编写`new`时，您明确地要求 JavaScript 创建和存储一个对象。因为原始数据类型与对象完全相反，所以永远不要对它们使用`new`。

然而，您仍然可以使用构造函数在 JavaScript 中执行[类型强制](https://developer.mozilla.org/en-US/docs/Glossary/Type_coercion)。在没有 `**new**` **关键字的情况下调用`String(value)`—**—**将把那个`value`作为字符串原语返回。**

原始数据类型(`[String()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/String)`、`[Number()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/Number)`等)的对象包装器的构造函数。)是您在 JavaScript **中调用的唯一的**构造函数，而没有使用**关键字`new`。**

这是一个常见的混淆来源:如果你从来不使用`new`调用构造函数，为什么原始类型——不是对象——有一个带有构造函数的“对象原型”？

原因还是为了转换类型——就像我举的例子，使用`String(value)`强制一些`value`变成一个字符串。

另一个原因是 JavaScript 自动使用这些构造函数来“对象包装”原始类型。但是您永远不需要使用`new`关键字手动完成这项工作。

这些概念看起来很高级，但是一旦你理解了它们，你就会对 JavaScript 中原始数据类型和对象的区别有深刻的理解。

**编码快乐！**👨‍🔬🥽🧪🔬💥

德里克·奥斯汀博士是《职业编程:如何在 6 个月内成为一名成功的 6 位数程序员》一书的作者，该书现已在亚马逊上出售。