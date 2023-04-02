# 在 JavaScript 中使用 var、let 和 const 的艺术——一种稍微有点非传统的方法

> 原文：<https://javascript.plainenglish.io/the-art-of-using-var-let-and-const-d3a819a391a0?source=collection_archive---------4----------------------->

***更好的代码不需要明确的解释***

![](img/a489683e60d7cbd1efe322d3ed8c557b.png)

Image from : [https://images.wallpaperscraft.com/](https://images.wallpaperscraft.com/image/artist_waves_colorful_129158_2048x1152.jpg)

# 我为什么要写这个？

我看过很多关于这个话题的帖子和视频，但是，我决定写下我自己的观点。因为我看过的大多数文章都说，

> 1.避免使用`var`
> 
> 2.`let`是新的`var`

但是我有不同的方法。我对`let` 和`const` 的介绍有不同看法。我同意`var` 在某些特定情况下有一些问题，但是我们用了`var` 将近 20 年。

所以，我相信我们仍然可以在某些情况下使用`var`来获得更可读的代码。`let` 和`const` 也有它们的用法。首先，我们将看到每个人的行为。然后我们会看到如何使用它们来获得更可读的代码。

# **1。var**

1.  `*var*` *变量附加到封闭函数范围。*

![](img/3a9fb7c74eee13e0695c137b3eb8c1dd.png)

var attaches itself to enclosing scope. Image from : [https://clipground.com](https://clipground.com/images/onto-clipart-12.jpg)

> 定义为`var` 的变量不仅可以在定义它们的块内访问。而且，也可以在块外访问它们。这是因为`var` 变量将自己附加到`function` 作用域或`global` 作用域。`var` 仅将功能块和全局上下文视为作用域。

让我来说明我的意思。

运行上述代码时，您可能会遇到错误。相反，您将在控制台上记录 0 1 2 3 4 5 和 6。记录数字 6 是因为当执行从`for` 循环退出时，I 的值是 6。尽管 I 被定义在 for 循环块内部，我们仍然可以从外部访问它。那是因为`var`。

*2。* `*var*` *将受到吊装*的影响

![](img/e5e5519460a2308aaf252e53f144291b.png)

Photo by [Fas Khan](https://unsplash.com/@fasbytes?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当 JavaScript 引擎运行程序时，它将提升所有的`var` 变量。因此，我们可以在给变量赋值之前使用它们。为了理解这一点，让我们看看下面的代码片段。

上面的代码将运行没有任何错误，这是因为提升。

*3。我们可以在同一个范围内多次重新声明同一个变量。*

上述代码将在控制台上记录“efg”。因为`**var**` **变量可以在同一个作用域内重新声明。**

# 2.让

声明为`let` 的变量的行为类似于其他语言中的变量。所以，我不打算浪费时间详细解释它们。让我们简单地看看他们。

1.  范围仅限于定义它的块。

在这种情况下，如果我们运行上面的代码片段，我们将得到一个`RefferenceError` 。因为没有直接在`start` 函数内部声明变量。

2.`let`不受吊装影响。

这种情况下，你会得到一个`RefferanceError`。因为我们不能在声明之前使用 let 变量。

3.我们不能在同一个范围内重新声明一个变量。

在这种情况下，您将得到一个`SyntaxError`，因为您不能在相同的范围内使用相同的变量名。

# `**3\. const**`

关于`const` 令人困惑的是它的名字。我们通常用`const`来表示常数。但在这里，情况并不完全如此。`const` 这里在 JavaScript 中的意思是**你不能在第一次赋值后给变量赋值。但是，你可以改变它们。**

```
const fisrtName = “abc”;
fisrtName = “efg”;// TypeError
```

正如您已经猜到的，这将抛出一个`TypeError`。

然而，棘手的部分来了。

```
const myArray=[1,2,3];myArray[0]=2;console.log(myArray) //[2,2,3]
```

在这里，上面的代码完全没问题。正如我前面说过的，你不能给一个`const`变量赋值。但是你可以改变它们。

除上述行为外，`const` 与`let`相同。

# **应用**`**var**`**`**let,**`**`**const**`**(美工)******

****现在，我们知道了`var`、`let`和`const`的行为。让我们看看如何通过在合适的地方使用它们来改进我们的代码。****

## ****`**var**`****

> ****可以使用 var 来声明属于整个函数的变量。****

```
**function foo(){ var name="abc" … … console.log(name)}**
```

****这里，您在语义上告诉读者这个变量可以在`function`中的任何地方使用。****

> ****当你在`function`的其他地方使用一些变量时，`function` 可能会中断。避免对他们使用`var` 。****

****此外，您知道`var` 变量可以在相同的范围内再次声明。如果你有更长的函数—****

> ****您可以在函数中用相同的值再次声明相同的变量。这样，你就不需要一直走到变量被声明的地方，也不需要看到被赋值的值。****

## ****`**let**`****

> ****您可以使用 let 来声明只应在几行内使用的变量。因为在其他地方使用它可能会破坏代码。****

```
**function foo(){ let name=”abc”; console.log(name)}**
```

****另外，如果你担心有人会在`function`的其他地方使用这个变量****

> ****你也可以通过在两个花括号内声明变量来确定作用域。****

```
**function foo(){ {let name=”abc” console.log(name)}}**
```

****在上面的例子中，块内的 name 变量在块外是不可见的。这种行为将阻止程序员在其他地方使用该变量。****

> ****您可以在块外声明另一个同名的变量。这将防止我们的代码名称冲突。****

```
**function foo(){ {let name=”abc”;
       console.log(name)}//abc
       let name=”xyz”
       console.log(name)//xyz}**
```

## ****`**const**`****

****当我们看到`const`时，常量这个词会在我们的脑海中闪现****

> ****我们应该只对原始类型使用 const，例如，数字、字符串。因为当声明为 const 时，原语的行为与真实世界的常量相同。****

****这样，我们可以确保当其他程序员看我们的代码时，他/她理解的是正确的。****

```
**function foo(){ const age=21; const names=[“abc”,”xyz”];}**
```

****这里，在上面的代码中，将`array` 声明为`const` 是一个问题。Tt 更不可能把一个新数组重新赋值给同一个变量。由于`const`在数组上的行为不同，这使得代码可读性更差。即使我们将`arrays` 声明为`const`，它们也不是常量。****

# ******结论******

****与其用另一个行为完全不同的东西来代替某样东西，不如用它们来使我们的代码更容易理解。我在文章中只提到了几个场景。如果您发现任何其他用例，请在评论部分随意提及。因为我想在这个话题上发现更多。****

****谢谢大家！****

*****更多内容看* [***说白了. io***](http://plainenglish.io/)****