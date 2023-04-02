# 如何从 JavaScript 对象数组中提取数组形式的属性值

> 原文：<https://javascript.plainenglish.io/how-to-extract-a-value-of-a-property-as-an-array-from-an-array-of-javascript-objects-4f586729a7b3?source=collection_archive---------6----------------------->

![](img/b54208ad0ceba0c7d160e066817adf07.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从一系列 JavaScript 对象中提取属性值是我们必须经常做的事情。

在本文中，我们将研究如何从 JavaScript 对象数组中提取属性值来创建数组。

# 数组映射方法

`map`方法可以在 JavaScript 数组实例中使用，它允许我们将一个数组映射到另一个数组。

这意味着我们可以使用它从数组中的每个对象提取属性，并将提取的值放入它自己的数组中。

例如，我们可以写:

```
const objArray = [{
  foo: 1
}, {
  foo: 2
}, {
  foo: 3
}]
const result = objArray.map(a => a.foo);
```

我们有带有具有`foo`属性的对象的`objArray`数组。

然后我们用一个函数调用`map`来返回每个数组元素的`foo`属性值。

`a`是被迭代的数组元素。

因此`result`就是`[1, 2, 3]`。

我们也可以写:

```
const objArray = [{
  foo: 1
}, {
  foo: 2
}, {
  foo: 3
}]
const result = objArray.map(({
  foo
}) => foo)
```

在`map`回调中，我们用参数来破坏`a`对象。

所以我们只能拿到`foo`并退回。

# 洛达什

我们也可以使用洛达什方法来做同样的事情。

我们可以使用`pluck`方法将一个对象数组映射到一个对象，该对象具有数组中每个对象的给定属性的属性值。

例如，我们可以写:

```
const objArray = [{
  foo: 1
}, {
  foo: 2
}, {
  foo: 3
}]
const result = _.pluck(objArray, 'foo');
```

在最后一行，我们传入`objArray`，这是对象数组。

第二个参数是我们想从数组中的每个对象中得到的属性。

因此`result`应该给出与前面例子相同的答案。

洛达什还有一个`map`方法让我们做同样的事情。

例如，我们写道:

```
const objArray = [{
  foo: 1
}, {
  foo: 2
}, {
  foo: 3
}]
const result = _.map(objArray, 'foo');
```

参数与`pluck`相同，返回相同的结果。

最新版本的洛达什还附带了`property`方法，我们可以通过书写将它与`map`方法结合起来:

```
const objArray = [{
  foo: 1
}, {
  foo: 2
}, {
  foo: 3
}]
const result = _.map(objArray, _.property('foo'));
```

`property`返回一个给定属性名的访问器，我们将它传递给方法。

访问器被`map`识别，它将使用访问器从数组中的每个对象中提取属性。

因此，我们得到了与其他示例相同的结果。

# 结论

我们可以使用普通的 JavaScript 或 Lodash 从数组中的每个对象中提取属性值。希望你觉得这篇文章有用，谢谢你的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io/)