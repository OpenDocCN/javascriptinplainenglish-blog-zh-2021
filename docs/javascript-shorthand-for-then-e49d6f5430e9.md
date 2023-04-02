# JavaScript 的简写。然后

> 原文：<https://javascript.plainenglish.io/javascript-shorthand-for-then-e49d6f5430e9?source=collection_archive---------14----------------------->

![](img/e33c56cb3f6eff3f64acf24c16d36064.png)

Photo by [Sudharshan TK](https://unsplash.com/@shantk18?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

也许我很慢。也许大多数人都是在没有任何帮助的情况下学会的。也许网上有很多我忽略的教程。我不知道，但我花了一年多的时间来琢磨我要在这里讨论的内容。

我依稀记得之前看到过这方面的例子，但对我来说没有任何意义，而且，如果我读过任何关于它的解释，它也没有坚持。所以，这就是我希望得到的解释。

JavaScript 中的一个常见情况是代码类似于:

```
Promise
 .then(function(args){ handle args; return value; })
 .then(function(args){ handle args; return value; })
 .then(function(args){ handle args; return value; })
 …
 .catch(function(error){ handle error; })
```

很多人对此进行速记，因此它看起来像:

```
Promise
 .then((args)=>{ handle args; return value; })
 .then((args)=>{ handle args; return value; })
…
```

或者，如果没有必要对论点做太多，它甚至可能是:

```
Promise
 .then((args)=> value)
 .then((args)=> value )
…
```

这个版本是我认为我应该早点明白的地方，但是也许我不是这里唯一一个慢性子，所以我想我会分享这个以防万一。

*(等)第二次争论。那么*就是从前一个*返回的*。

所以，代码如下:

```
Promise
 .then((arg)=>arg+1)
 .then((arg)=>arg+1)
 .then((arg)=>console.log(arg))
```

假设第一个“arg”为零，Will 最终会将数字 2 写入控制台。

好吧，这不是一个很大的飞跃，但这是这个等式中对我来说最重要的部分。

上面的方框可以写成:

```
Promise
 .then(arg=>arg+1)
 .then(arg=>arg+1)
 .then(console.log)
```

它的功能将完全相同。我可以简单地提供 console.log 函数，而不是用 arg 构建一个闭包函数，然后将它传递给控制台，它会自动传递从前面的*返回的值。然后*块。

您可以使用任何功能来执行此操作，包括您自己的功能。

或许:

```
function compress(str){ return compressedString; }
function send(str){ wretch(“send/url”).post(str) }
Promise
 .then(JSON.stringify)
 .then(compress)
 .then(send)
```

像这样将我的代码分解成块使得代码*更加易读和整齐。它允许我模块化成不同的文件，这使得代码维护更容易。*

总的来说，我觉得这是一个非常有用的琐事，我希望我能更快地找到它。

*多内容于* [***中。*T21*报名参加我们的***](http://plainenglish.io/) **[***免费周报在这里***](http://newsletter.plainenglish.io/) ***。*****