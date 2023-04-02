# JavaScript 中的不变性——对象和数组

> 原文：<https://javascript.plainenglish.io/immutability-in-javascript-objects-and-arrays-34d6a85f29b7?source=collection_archive---------18----------------------->

![](img/7ad37ea6e272e162e80ad592577ae38c.png)

Photo by [Matthew Henry](https://unsplash.com/@matthewhenry?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是不可变对象？

> 在[面向对象](https://en.wikipedia.org/wiki/Object-oriented_computer_programming)和[函数式](https://en.wikipedia.org/wiki/Functional_programming)编程中，一个**不可变对象**(不可变对象)是一个[对象](https://en.wikipedia.org/wiki/Object_(computer_science))，它的状态在创建后不能被修改。
> 
> -维基百科

上面的定义相当简单，但我会详细说明。一旦创建了对象，就不能更改该对象的任何属性。这实际上是创建了一个不能更新的只读对象。

# 为什么我需要使用不变性？

利用不可变的设计可以提供许多好处，例如

*   线程安全
*   更容易调试
*   更易维护的代码

关于线程安全，对被多个线程访问的对象进行突变可能会导致意外和不正确的结果。如果您有一个计数器来计算有多少人访问了您的网站，您希望确保每个计数都记录正确。如果您直接更新计数器，由于并发错误，可能会遗漏一个视图，并且您将得到一个不正确的计数。如果你有一个不可变的计数器，每次都会创建一个新的版本来确保你有正确的值。

对于调试来说，能够及时查看某个位置的对象状态(带有值的属性)确实可以减少混乱。如果您有一个人的姓氏需要更新，在没有不变性的情况下，您可能会在更新后丢失以前的姓氏。使用不变性，您将拥有更新前对象的记录，以及替换它的具有更新名称的新对象。

不变性是一种常见的编码实践，在各行各业都有使用。通过应用不可变的设计模式，其他开发人员应该更容易理解您的代码和您试图完成的任务。

# JavaScript 中的示例—对象

既然我们已经介绍了什么是不可变对象以及我们为什么使用它们，那么让我们介绍一些使用突变和不可变设计模式的代码示例。

假设我们有一个人对象。person 对象有两个属性，名字和姓氏

```
const person = {
   firstName: 'Jane',
   lastName: 'Smith'
}
```

让我们想象一下，简刚刚结婚，想把她的姓改成她丈夫的姓。所以她现在的姓将不再是“史密斯”，而是“多伊”。首先，我们将介绍如何通过改变 person 对象来实现，然后我将介绍如何使用不可变的设计模式

## 使对象变异

使用简单的 JavaScript，很容易更新这个人的姓氏。我们只需给 person.lastName 赋一个新值，然后就可以记录结果了

```
person.lastName = 'Doe' // Mutation// Logging her new last name
console.log(person.lastName) // 'Doe'
```

太好了！但是她之前的姓呢？因为我们直接变异了对象，所以该值不再可访问。如果我们需要更新具有她旧姓氏的其他记录，这可能是一场噩梦。

## 使用不可变模式和 ES6 扩展语法

让我们创建一个具有更新后的姓氏的副本，而不是直接改变 person 对象。

```
// Create a copy of the original object with the updated last name
const updatedPerson = {
   ...person, // Copy values from original object
   lastName: 'Doe'
}
```

如果你不熟悉这个语法，让我解释一下。在 ES6 中，我们可以使用 spread 操作符从一个对象中提取属性，并将它们复制到一个新对象中。在这种情况下，我们基本上是说将 person 的所有属性复制到这个新的 updatedPerson 对象中。现在，在跨页下面，我们用新值包含 lastName，这样从 person ('Smith ')复制的值将被' Doe '覆盖。

我知道这有点令人困惑，但是相信我，一旦你练习了，就会明白很多道理。现在，有了这个不可变的结构，让我们再次尝试调试

```
console.log(person.lastName); // 'Smith'
console.log(updatedPerson.lastName); // 'Doe'
```

厉害！现在我们有了 Jane 的审计历史和对她姓氏的更新。如果我们需要检索或访问那个值，我们仍然可以在内存中找到旧的对象

# JavaScript 中的示例—数组

由于我们在前一节中已经介绍了很多对象，所以这一节会稍微简短一些。假设我们有一个姓氏数组，我们需要在 Jane 结婚后更新她的姓氏

```
const lastNames = ['Johnson', 'Smith', 'Kennedy']
```

## 变异一个数组

如果我们想将数组的第二项更新为“Doe ”,这就是我们通过数组变异来完成的方式。

```
lastNames[1] = 'Doe' // Mutation
console.log(lastNames) // ['Johnson', 'Doe', 'Kennedy']
```

数组现在更新了，但是像以前一样，我们丢失了姓氏列表的记录。

## 使用不可变模式和 ES6 扩展语法

这一次，我们不直接改变数组，而是创建数组的副本，然后更新对象。

```
const newLastNames = [...lastNames] // Create a copy of the array
newLastNames[1] = 'Doe'console.log(lastNames) // ['Johnson', 'Smith', 'Kennedy']
console.log(newLastNames) // ['Johnson', 'Doe', 'Kennedy']
```

在本例中，我们再次使用 spread 语法创建一个新数组，以创建所有数组元素的副本，并将它们放在一个新数组中。一旦完成，我们就可以更新新对象中的值，而不改变原始数组。正如我们再次看到的，我们可以保留对象的更新历史，并且不会遇到任何并发问题。

# ES6 扩展语法的注意事项

我必须提到，虽然 ES6 的 spread 语法很棒，但它也有一个缺点，那就是它只会执行*浅层复制*。我的意思是它只会向下克隆一层对象。因此，如果您的对象具有其他对象的属性，您将需要对这些嵌套属性使用 spread 语法，以确保它们保持不变。对象数组也是如此。

[这里有一篇很棒的文章，解释了浅复制和深复制](https://www.geeksforgeeks.org/what-is-shallow-copy-and-deep-copy-in-javascript/)

# 结束语

虽然实现不可变的设计模式是强大的，但它并不总是完美的解决方案。正如技术中的一切一样，您必须权衡利弊，选择适合您的解决方案。不变性确实增加了一些额外的代码行，但是作为一个经验丰富的程序员，我可以向您保证，从长远来看，它是值得使用的。我并不总是一个信徒，但我已经接受了这种模式，并将其整合到我的代码中适合的地方:

React 和 Redux 是利用不变性的主要支持者，所以本文将介绍如果您开始用 React 编码，您可能会看到什么以及为什么会这样。

一如既往，如果你喜欢这篇文章，请鼓掌并跟随，快乐编码！

*更多内容看*[***plain English . io***](http://plainenglish.io/)