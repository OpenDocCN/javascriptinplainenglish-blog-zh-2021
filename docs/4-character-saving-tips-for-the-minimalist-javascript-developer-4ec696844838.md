# 极简主义 JavaScript 开发人员的 4 个节省字符的技巧

> 原文：<https://javascript.plainenglish.io/4-character-saving-tips-for-the-minimalist-javascript-developer-4ec696844838?source=collection_archive---------19----------------------->

## 击键需要时间，时间就是金钱。你的公司可以通过采用这些标准做法来节省数百美分。

![](img/caa03dbecc119ce379defbd15d07b3fd.png)

Photo by [Bench Accounting](https://unsplash.com/@benchaccounting?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

曾经有一段时间，公司会按代码行付费，但他们早就识破了开发人员利用系统并消除了这个有利可图的漏洞。如今，随着极简主义在生活中风靡一时，是时候将同样的原则应用到我们的代码中了。

下面是一些节省字符的 JavaScript 技巧，它们对改进功能毫无帮助，但是可以让你所有重要的手指避免不必要的击键。

## 编写箭头函数时跳过括号

当然，你可以这样写:

```
**const** longWindedFunction = (likesMinimalisticCode) => `This took me too long to write true/false? ${likesMinimalistCode}`
```

但是为什么不像这样跳过写括号所需要的几次击键呢？：

```
**const** myKindOfFunction = likesMinimalisticCode => `This took me too long to write false? ${likesMinimalistCode}`
```

你的手指以后会感谢我的。

## 对无参数箭头函数使用下划线

多年来，我一直在无意中亵渎极简主义之神，用括号来启动我的无参数箭头函数。想象一下，当我发现一种方法可以将开头的字符数减半时，我有多惊讶。

我以前是怎么写的:

```
**const** functionWithNoArgs = () => 'Surely this is too long?'
```

我现在是这样写的:

```
**const** functionWithNoArgs = _ => 'Short and sweet'
```

在我的 IDE 中，这让我不必按下→按钮，我也不必一路到达*到左括号按钮。*

我*不知道*为什么是下划线，但我不在乎，我的手指也不在乎。你也不应该。

## 从 arrow 函数返回对象时跳过 return 语句

这是我最喜欢的一个，因为几个月来，我一直在为如何避免在返回一个对象的箭头函数中输入“return”这个词而苦恼。当返回对象以外的东西时，这很简单:

```
**const** returnsArray = _ => []
**const** returnsString = _ => ''
```

然而，当你试图以同样的方式返回一个对象，没有骰子:

```
**const** returnsObject = _ => {} // Psych! Returns void
```

多么令人恼火，但我突然明白了。我们之前无情抛弃的旧括号拯救了我:

```
**const** returnsObject = _ => ({}) // Winning
```

我不仅写了一个漂亮的、极简的函数，同时还创作了一些可爱的代码艺术品。

## 当变量名与键名匹配时，省略对象属性值名

这张一定会给新手留下深刻印象。没有人喜欢重复自己，所以如果你把一个变量的值赋给一个对象的属性，而不是做下面的事情:

```
**let** wow**,** so, repetitive// bonus point**const** soMuchWaste = {
    wow: wow,
    so: so,
    repetitive: repetitive
}
```

通过省略无用的词来减少赘肉:

```
**let** so, much, win**const** lessIsMore = {
    so,
    much,
    win
}
```

如果您的变量名与键不匹配，您可以更改它们，即使它们没有意义。毕竟，你可以用这个小宝石*节省几十次击键。*

这就是我现在所知道的，但是如果你碰巧知道任何更聪明的，像上面这样的字符保存 JavaScript 技巧，请在评论中告诉我，我会很高兴地假装是我想出的，将它们添加到本文中，并与任何人分享收益。

感谢你的阅读，我在此免除我自己对你可能从代码极简主义的憎恨者那里收到的任何负面信息的任何责任。

*更多内容看*[***plain English . io***](http://plainenglish.io/)