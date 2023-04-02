# 如何避免 JavaScript 中的对象突变(移除属性)

> 原文：<https://javascript.plainenglish.io/how-to-avoid-object-mutation-in-javascript-removing-properties-df32a2debd3d?source=collection_archive---------12----------------------->

## 展示如何在删除属性时避免 JavaScript 中对象变异的快速指南&免费的乔恩·斯图尔特 Gifs 再一次…

![](img/bf839fb74720f34fafc7b42b37e7bd5a.png)

Photo by [Gary Chan](https://unsplash.com/@gary_at_unsplash?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

上周，我深入探讨了 [JavaScript 对象以及如何避免对它们进行变异](/javascript-how-to-avoid-object-mutation-7cd733913a9f)的话题。实际上，我从社区中得到了一些很好的回应，所以我想跟进其中的一些回应。首先，谢谢大家！我真的很感激你们这么多人愿意回应和分享你们的想法。第二，上周我只涉及了这个主题的一部分，因为我忽略了关于对象变异的某个方面…

## 移除属性时如何避免对象突变

我让你失望了。我很抱歉。我只向您展示了如何在添加属性时避免对象突变。但是如果我们想删除属性呢？这实际上比你想象的要容易，而且你已经在不知不觉中学会了如何去做！

好吧。让我们从上周的相同设置开始。

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
}let avenger = character;character.lastName = 'Marvel';
```

使用上面的代码，我们改变了我们的原始对象字符，因为两个变量，`character`和`avenger,`引用了同一个对象。那么，我们如何创建一个由 avenger 变量引用的新对象，而不是删除属性呢？

## 1.[展开语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_object_literals)与[对象析构](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment#object_destructuring)

没错，朋友们！我们拿出我们那碗语法上含糖的好东西，开始把这些东西展开，但是多加了一点糖。这与我们之前所做的并没有太大的不同，只是现在我们将通过结合 spread 操作符和 object destructuring 来删除我们不想包含在新对象中的属性。

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let { lastName, ...avenger } = character;avenger.lastName = 'Marvel';
```

就是这样。我们储存在角色中的物品完好无损，我们继续愉快地完成储存在复仇者中的物品。

这种使用 spread 语法的方式与我们在上一篇博客中使用的方式之间的主要区别是，在我们设置`avenger.lastName = ‘Marvel’;`的属性之前，我们的新对象是什么样子的。请参见下面的差异:

```
let character = {
    firstName: 'Captain',
    lastName: 'America'
};let avenger = { ...character };
let { lastName, ...avenger2 } = character;console.log(avenger);
console.log(avenger2);// { firstName: 'Captain', lastName: 'America' }// { firstName: 'Captain' }
```

在我之前的博客中，我们使用 spread 语法`let avenger = { …character };`直接复制了整个对象。通过对象析构，我们移除了`lastName`属性，并复制了在变量`character`中引用的对象的剩余部分，将其存储在变量`avenger2`中。我不确定其中一种一定比另一种更好，但是两种方式都完成了我们想要做的事情。

## 2.没有 2！

技术上来说，没有 2 有点误导。在这个博客系列中，我希望在没有库帮助的情况下，严格使用普通的 JavaScript。然而，当我研究是否有其他我不知道的方法时，我偶然发现了几个 [引用](https://stackoverflow.com/questions/33053310/remove-value-from-object-without-mutation)到 [Lodash 的库](https://lodash.com/)。您可以同时使用`[_.omit](https://lodash.com/docs/4.17.15#omit)` & `[_.pick](https://lodash.com/docs/4.17.15#pick)`两种方法来达到想要的效果。我不会在这个博客中涉及 Lodash，但我想给你一个参考。

## 结论

就是这样，朋友们！再次抱歉，我没有在上一篇博客中提到这个。我希望这对你有所帮助，我鼓励你练习所有这些不同的方法来巩固这些 JS 技能。下次见！

快乐编码🤓