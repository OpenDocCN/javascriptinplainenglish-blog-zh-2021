# 如何用 JavaScript 改变元素的类

> 原文：<https://javascript.plainenglish.io/how-to-change-an-elements-class-with-javascript-c294388ede7?source=collection_archive---------18----------------------->

![](img/ad23f4756b8a39ce297221048c36d1db.png)

Photo by [Anne Nygård](https://unsplash.com/@polarmermaid?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们使用 web 前端应用程序，那么改变元素的类是我们经常要做的事情。

在本文中，我们将看看如何用 JavaScript 改变元素的类。

# classList 属性

一个元素有一个`classList`属性，可以让我们操作应用于该元素的类。

例如，如果我们有一个 div:

```
<div>
  hello world
</div>
```

然后，要向 div 添加一个类，我们可以编写:

```
document.querySelector("div").classList.add('hello');
```

我们调用`add`将`'hello'`类添加到 div 中。

如果已经添加了`hello`类，那么什么都不会做。

要删除一个类，我们可以调用`classList.remove`方法:

```
document.querySelector("div").classList.remove('hello');
```

为了检查一个类是否已经存在于一个元素中，我们可以使用`classList.contains`方法:

```
document.querySelector("div").classList.contains('hello');
```

如果该类应用于 div，则返回`true`，否则返回`false`。

为了切换应用于元素的类，我们可以调用`classList.toggle`方法:

```
document.querySelector("div").classList.toggle('hello');
```

如果将`hello`类应用于 div，那么它将被移除。

否则，`hello`类将被添加到 div 中。

这在最近的浏览器中是可用的。

# 类名属性

操纵元素类的另一种方法是操纵`className`字符串属性。

例如，我们可以写:

```
document.querySelector("div").className = 'hello';
```

我们获取 div 并将`className`设置为`'hello'`以将 div 的`class`属性设置为`'hello'`。

要通过操作`className`属性来添加一个类，我们可以写:

```
document.querySelector("div").className += ' hello';
```

我们添加一个空格和`hello`来将`hello`类添加到 div 中。

要删除`hello`类，我们可以使用`replace`方法:

```
document.querySelector("div").className.replace(/(?:^|\s)hello(?!\S)/g, '')
```

我们检查在类名的开头或结尾是否有空格的`hello`,并用空字符串替换它们。

`g`标志将找到所有的实例，并对它们进行替换。

要确定一个类是否在 div 中，我们可以写:

```
document.querySelector("div").className.match(/(?:^|\s)hello(?!\S)/)
```

我们用正则表达式调用`match`，该正则表达式匹配`hello`前后的空格，以检查该类是否在`className`字符串中。

# 结论

操纵 HTML 元素的类的最好和最简单的方法是使用`classList`属性。

或者，我们也可以操作`className`字符串属性来改变元素的`class`属性。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)