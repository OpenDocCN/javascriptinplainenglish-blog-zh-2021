# Array.at()将改变我们在 JavaScript 中访问数组值的方式

> 原文：<https://javascript.plainenglish.io/array-at-will-change-how-we-access-array-values-in-javascript-517c3a13d505?source=collection_archive---------2----------------------->

## 如何在 JavaScript 中访问负索引，以及这如何随着 Array.prototype.at()而改变

![](img/d4ff610010508b378b4c570b6dfdc0bb.png)

Photo by [La-Rel Easter](https://unsplash.com/@lastnameeaster?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时候，我觉得迫切需要反向访问数组元素，可能是最后一项或倒数第二项。

实现它的方法从来都不简单，就像在其他语言中，你只需要说 array[-1]就可以得到最后一项。

相反，我们不得不做类似`array[array.length-1]`之类的事情。

`[]`语法不是特定于数组和字符串的；它适用于所有对象。通过索引引用一个值，像`array[1]`，实际上只是用键`1`引用对象的属性，这是任何对象都可以拥有的东西。所以`array[-1]`在今天的代码中已经“工作”了，但是它返回对象的`-1`属性的值，而不是返回一个从末尾向后计数的索引。

## 访问元素

试图获取数组中不存在的索引值将会在 JavaScript 中返回 undefined。

```
const arr=['a', 'b', 'c', 'd', 'e'];arr[1] // barr[4] // earr[-1] // undefined
```

这里有什么选项来访问最后一个元素，目前我们可以做`arr[arr.length — 1]`或`arr.slice(-1)[0]`，这将给我们`e`作为上述数组的输出。

## 拟建物业—“at”

有了这个新属性，访问数组中的元素将变得更加方便。

我们访问值的方式不会随着的**而改变，但是访问负索引将变得容易。下面是它的样子:**

```
const arr=['a', 'b', 'c', 'd', 'e'];arr.at(1) // barr.at(4) // earr.at(-1) // earr.at(10) // undefined
```

## 结论

希望这将很快推进到第 4 阶段，并被正式采用。我对此感到非常兴奋，并且可以看到这成为访问数组元素的语法糖。

还有一个 [**last**](https://github.com/tc39/proposal-array-last) 属性正在讨论中(访问数组/字符串的最后一个元素)，但它仍处于第 1 阶段，很可能会因为这个新属性 中的 [**而被放弃，因为它已经是第 3 阶段了，并解决了相同的目的和更多的问题。**](https://github.com/tc39/proposal-relative-indexing-method)

[](https://github.com/tc39/proposal-relative-indexing-method) [## tc39/建议相对索引方法

### TC39 建议增加一个。at()方法对所有基本的可索引类(Array，String，TypedArray) Stage: 3…

github.com](https://github.com/tc39/proposal-relative-indexing-method) [](https://github.com/tc39/proposal-array-last) [## tc39/建议-阵列-最后

### (目前是第一阶段)该提案的支持者(@keithamus)目前不打算进入第二阶段。其他提议…

github.com](https://github.com/tc39/proposal-array-last) 

*更多内容看*[***plain English . io***](http://plainenglish.io)