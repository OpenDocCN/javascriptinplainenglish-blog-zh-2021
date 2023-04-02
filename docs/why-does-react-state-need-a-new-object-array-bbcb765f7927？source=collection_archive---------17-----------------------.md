# 为什么反应状态需要新的对象/阵列？

> 原文：<https://javascript.plainenglish.io/why-does-react-state-need-a-new-object-array-bbcb765f7927?source=collection_archive---------17----------------------->

![](img/5fa20f559c05a7cdb9c232eb28793f2a.png)

如果您已经使用“反应”有一段时间了，那么您应该熟悉状态更新是如何工作的。有很多内部优化，React 可以加快渲染速度。反应内部的实现细节之一是，它检查给定的状态对象是否已经实际改变。但是分配一个新的对象/数组的行为会让新来的人大吃一惊。让我们理解为什么在分配状态时，React 需要一个新的对象/数组副本。

# JavaScript 中的 Object.is()

`Object.is()`是 JavaScript 中的比较运算符。它被附加到 Object.prototype，可以用来比较 JavaScript 值，包括对象值和原始值。

对于对象:

```
const author1 = {name: "Saransh Kataria"};
const author2 = {name: "Saransh Kataria"};
Object.is(author1, author2); // false
```

由于对象是通过引用存储的，因此比较返回 false。

# 就反应而言，这种相关性如何？

使用 Object.is()进行上一个和下一个状态的比较，以确定是否更新 DOM。该案件的相关部分是:

```
const author1 = {name: "Saransh Kataria"};
author1.name = "Wisdom Geek";
Object.is(author1, author1); // true
```

因为我们正在改变同一个对象及其属性，所以比较将始终返回真。

因此，当我们这样做时:

```
const [author, setAuthor] = useState({name:"Saransh Kataria")};const updateName = () => {
  author.name = "Wisdom Geek";
  setAuthor(author)
}
```

在 update name 函数中，我们正在更新作者对象。并将更新后的对象发送给 setAuthor。这不会更新用户界面，即使我们已经更新了作者对象。

# 为什么用户界面没有更新？

正如我们之前看到的，改变一个对象的属性并不会改变该对象的引用。当我们调用 setter 函数时，React 在引擎盖下使用 Object.is()来确定状态是否被更新。

因为对象引用没有改变，所以 Object.is()返回 false，即使我们确实更新了它的某些属性。因此，React 感觉不到更新用户界面的需要，因为根据它没有任何改变。

为了让它正确工作，我们需要传入一个对 useState 函数的新引用。为此，我们需要创建一个新的对象。一旦我们这样做，Object.is()将返回 true，因为引用将不会相同，我们将触发重新渲染。

```
const updateName = () => {
  setAuthor(prevState => {...prevState, name: "Wisdom Geek"});
}
```

这使用扩展语法和回调函数来更新状态。我们返回一个新的对象，它没有任何从初始对象直接引用的属性。我们也更新了我们想更新的属性。

同样的逻辑也适用于数组，因为它们也是引用类型。

# 结论

希望这个解释能稍微揭开 reactor 内部的神秘面纱，并对 reactor 中状态管理的实现细节有更好的了解。如果您有任何问题，请在下面留言！

*原载于 2021 年 5 月 25 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/react/why-does-react-state-need-new-object-array/)。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)