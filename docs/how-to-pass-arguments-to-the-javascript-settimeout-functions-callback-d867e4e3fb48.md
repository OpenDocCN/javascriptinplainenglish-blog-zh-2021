# 如何给 JavaScript setTimeout 函数的回调传递参数？

> 原文：<https://javascript.plainenglish.io/how-to-pass-arguments-to-the-javascript-settimeout-functions-callback-d867e4e3fb48?source=collection_archive---------9----------------------->

![](img/48bc08134f33616cd310b4644af01ce4.png)

Photo by [Julian Hochgesang](https://unsplash.com/@julianhochgesang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

`setTimeout`函数让我们在几毫秒的延迟后运行 JavaScript 代码。

在本文中，我们将看看如何向 JavaScript `setTimeout`函数传递参数。

# 使用更多参数调用 setTimeout

向`setTimeout`函数的回调传递参数的一种方式是在`setTimeout`的第二个参数之后传递它们。

例如，我们可以写:

```
setTimeout((greeting, name) => {
  console.log(greeting, name)
}, 1000, 'hello', 'jane')
```

我们有一个接受`greeting`和`name`参数的回调函数。

在第二个参数之后是`'hello'`和`'jane'`参数。

它们将以同样的顺序被传递到回调函数中。

所以控制台日志应该记录`hello jane`。

# 使用 bind 方法

`bind`方法让我们返回一个带有我们想要传入的参数的函数。

所以我们可以用`bind`返回的函数作为回调来代替。

例如，我们可以写:

```
const greet = (greeting, name) => {
  console.log(greeting, name)
}
setTimeout(greet.bind(undefined, 'hello', 'jane'), 1000)
```

用我们用`setTimeout`传递给`bind`的参数调用`greet`。

`bind`的第二个及后续参数被传递到`greet`函数中。

所以我们得到了和以前一样的结果。

# 在回调中调用函数

我们可以向`setTimeout`回调传递参数的另一种方式是在回调中调用我们想要的函数。

例如，我们可以写:

```
const greet = (greeting, name) => {
  console.log(greeting, name)
}
setTimeout(() => {
  greet('hello', 'jane')
}, 1000)
```

我们没有试图将`greet`函数直接传递给`setTimeout`，而是在回调中用我们想要的参数调用`greet`。

这给了我们和以前一样的结果。

# 结论

有几种方法可以将参数传递给`setTimeout`回调。

我们可以用`bind`来转换回调，或者我们可以直接将参数传递给`setTimeout`。

同样，我们可以在回调中调用我们想要的函数。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)