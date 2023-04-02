# 如何在浏览器控制台中显示一个 JavaScript 对象？

> 原文：<https://javascript.plainenglish.io/how-to-display-a-javascript-object-in-the-browser-console-e13355e19a89?source=collection_archive---------9----------------------->

![](img/47ad74e23f42924e8f66161f6628faea.png)

Photo by [Clem Onojeghuo](https://unsplash.com/@clemono?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为了使调试更容易，我们可以在控制台中显示我们想要检查的对象。

有各种方法可以做到这一点。

在本文中，我们将研究如何在浏览器控制台中显示 JavaScript 对象。

# console.log

`console.log`方法将把对象的内容直接记录到控制台。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  child: {
    c: 3
  }
}
console.log(obj)
```

我们只需将`obj`传入`console.log`，将其内容直接记录到浏览器的控制台。

# JSON.stringify

`JSON.stringify`让我们将 JavaScript 对象转换成 JSON 字符串。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  child: {
    c: 3
  }
}
const str = JSON.stringify(obj);
console.log(str)
```

然后我们看到:

```
{"a":1,"b":2,"child":{"c":3}}
```

在控制台里。

为了更容易阅读，我们可以在字符串化的属性中添加缩进。

为此，我们写道:

```
const obj = {
  a: 1,
  b: 2,
  child: {
    c: 3
  }
}
const str = JSON.stringify(obj, undefined, 2);
console.log(str)
```

`JSON.stringify`的第三个参数指定了每个字符串的缩进。

2 表示 2 个空格。

所以我们应该得到:

```
{
  "a": 1,
  "b": 2,
  "child": {
    "c": 3
  }
}
```

登录到控制台。

# console.dir 方法

`console.dir`方法也像`console.log`一样将一个对象记录到控制台。

例如，我们可以写:

```
const obj = {
  a: 1,
  b: 2,
  child: {
    c: 3
  }
}
console.dir(obj)
```

将`obj`登录到控制台。

# console.table 方法

`console.table`方法让我们以表格格式记录对象的属性。

例如，如果我们写:

```
const obj = {
  a: 1,
  b: 2,
  child: {
    c: 3
  }
}
console.table(obj)
```

然后我们得到一个表，表中有一个对象的属性和值。

# 结论

浏览器提供了许多方法来将对象记录到控制台中。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)