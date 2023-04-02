# JavaScript 等式:两倍等于(==)与三倍等于(===)

> 原文：<https://javascript.plainenglish.io/javascript-equality-double-equals-vs-triple-equals-81817c06a8b3?source=collection_archive---------7----------------------->

## JavaScript 中==和===的区别，为初学者讲解。

![](img/ecd97c3f53ec3f6a3c45f9637cd8db82.png)

Photo by [Tingey Injury Law Firm](https://unsplash.com/@tingeyinjurylawfirm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为任何编程语言的程序员，我们经常做的一件事是**等式检查**。这个值是否等于那个值。

在 **JavaScript 中，**有两个相等检查操作符:**双等于(==)** 和**三等于(===)** 。并且它们经常导致程序员在使用它们时感到困惑。

嗯，它们并不太复杂，难以理解。

在本文中，我们将讨论一些**差异和用例**，例如在哪里以及如何有效地使用这两种类型的操作符**。你猜怎么着？他们也很有趣，值得了解。**

> 所以我们走吧，🕊

但是坚持住。在深潜之前，我希望你考虑以下几点。

*   所有比较运算符在执行后都返回布尔值。不是 ***真*** 就是 ***假*** 。
*   而且我们都知道在编程中，只有两个值 1 和 0。所以如果我们更进一步，*真变成 1* 假变成 0。

好吧，记住这一点，让我们开始吧。

在 JavaScript 中，比较有两种方式。

*   与类型的比较
*   与值的比较

> 那么，==和===有什么区别呢？

# 一个简单的答案👇

double equals 首先*转换*操作数的类型，然后将它们与值进行比较。而三重等于比较值*而*不改变操作数的类型。

> 就这样吗？😒

当然不是。还有更多的。

> ***🔔但是等等，如果你不知道 JavaScript 中的类型转换，一定要看看下面的文章👇。那就更有意义了。***

[](/type-conversion-in-javascript-the-magic-c93cf96ba4da) [## JavaScript 中的类型转换:魔力

### 如果你是一个 JavaScript 开发者，那么你一定知道 JavaScript 有三种基本类型:数字、字符串和布尔。

javascript.plainenglish.io](/type-conversion-in-javascript-the-magic-c93cf96ba4da) 

# 现在，让我们来看一些场景:

要检查一个值是真还是假，我们可以使用 ***布尔*** 对象构造函数。以下是方法👇

```
**console.log(Boolean('hey'))**  //true
//-- any valid string is true**console.log(Boolean(0)) **      //false
//-- as I said earlier 1 is true and 0 is false**console.log(Boolean('0'))**     //true
//-- why 0 is true here ? Thanks to quotation, which makes it a String**console.log(Boolean(' '))**      //false
//-- the quotation has no character: not a valid string; false**console.log(Boolean([ ]))**     //true
//-- empty array
```

# 更多示例:

```
**console.log(false == 0)**  //true
**console.log(0 == '')**  //true
**console.log('' == false)**  //true
```

**双等于**将*假*和*“*转换为 0，这就是它们等于 0 的原因。

***但是！*** 这在三重相等的情况下不会发生。为什么？因为===不转换操作数的类型。

```
**console.log(false === 0)**  //false
//-- false is Boolean while 0 is Number, so they not equal for ===**console.log(0 === '')**  //false
//-- 0 is Number while '' is string**console.log('' === false)**  //false
//-- '' is String while false is Boolean
```

> ✨数据类型是任何编程语言中最重要的主题之一。我还写过一篇关于 JavaScript 中数据类型的文章。你可以在这里查看。👇

[](/data-types-in-javascript-the-weird-part-151e8fc3f1f3) [## JavaScript 中的数据类型——奇怪的部分

### 如果你对编程有一段时间的了解，你就会知道什么是数据类型，以及它们为什么重要。

javascript.plainenglish.io](/data-types-in-javascript-the-weird-part-151e8fc3f1f3) 

说完了，我们继续。在 JavaScript 中，我们有:null、undefined 和 NaN

*   **null** 是一种对象类型，表示没有注意到；空白的
*   **未定义**本身就是一种数据类型
*   **NaN** 是数的类型，意思不是数

```
**console.log(typeof null)** // object**console.log(typeof undefined )** // undefined **console.log(typeof NaN)** // Number
```

所以首先我们用== v/s ===来比较 null 和 undefined

```
**console.log(null == undefined)** // true
//-- double equal convert null into 0 and undefined as well**console.log(null === undefined)** // false
//-- for triple equal null is an object while undefined is undefined
```

> **null** 和 **undefined** 在与 Double Equal ( ==)比较时，只等于对方和自己。如果你把它们和其他值比较，你只会得到一个假值。

```
**console.log(null == null)** //true
**console.log(null == ' ')** //false
**console.log(null == false)** //false
**console.log(null == 000)** //false
**console.log(null == 123)** //false
**console.log(null == [])** //false**console.log(undefined  == undefined )** //true
**console.log(undefined == ' ')** //false
**console.log(undefined == false)** //false
**console.log(undefined == 0)** //false
**console.log(undefined == 1)** //false
**console.log(undefined == [])** //false
```

# 现在是南的时候了

**南**是 **JavaScript** 世界里的*神经病*玩家。为什么？因为它从来不等于任何值——你猜怎么着？甚至也不等于*本身*。

> 你在开玩笑吗？😵不，伙计，看看吧👇

```
**console.log(NaN == null)** //false
**console.log(NaN == 0)** //false
**console.log(NaN == 135)** //false
**console.log(NaN == 'NaN')** //false
**console.log(NaN == 'hellow')** //false
**console.log(NaN == 0)** //false
**console.log(NaN == undefined)** //false
**console.log(NaN == NaN)** //false
```

# 总结:

如你所见，在选择使用==还是===时，人们很容易感到困惑。

让我澄清这一点。每当你需要比较两个值时，总是用===，因为它给出预期的结果。但是一定要使用==和===，因为编程很有趣，对吗？

暂时就这样吧！

# 点击这里查看我的另一篇文章。👇

[](https://thesarveshprajapati.medium.com/) [## Sarvesh Prajapati -培养基

### 如果你想在 2021 年开始网络开发，你可能会非常不知所措🙄。在这里，我将带您通过一个方便的…

thesarveshprajapati.medium.com](https://thesarveshprajapati.medium.com/) 

# 在 Twitter 上与我联系:

# 下一集再见。😎

*更多内容请看*[***plain English . io***](http://plainenglish.io/)