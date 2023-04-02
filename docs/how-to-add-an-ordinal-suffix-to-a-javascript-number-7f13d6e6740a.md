# 如何给一个 JavaScript 数字加一个序数后缀？

> 原文：<https://javascript.plainenglish.io/how-to-add-an-ordinal-suffix-to-a-javascript-number-7f13d6e6740a?source=collection_archive---------7----------------------->

![](img/8e9eb1bbd8a978ec769bd334d3cbf06f.png)

Photo by [Yonatan Tesfaye](https://unsplash.com/@ytetbyflex?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想给 JavaScript 数字添加一个序号后缀。

在本文中，我们将了解如何给 JavaScript 数字添加序号后缀。

# 使用 Intl。多重规则构造函数

我们可以使用`Intl.PluralRules`构造函数轻松地给 JavaScript 数字添加正确的序号后缀。

例如，我们可以这样使用它:

```
const ordinal = (number) => {
  const ordinalRules = new Intl.PluralRules("en", {
    type: "ordinal"
  });
  const suffixes = {
    one: "st",
    two: "nd",
    few: "rd",
    other: "th"
  };
  const suffix = suffixes[ordinalRules.select(number)];
  return (number + suffix);
}
console.log(ordinal(101))
```

我们用`number`参数创建了`ordinal`函数。

在函数中，我们用`Intl.PluralRules`构造函数创建了`ordinalRules`对象。

第一个参数是`'en'`，它获取英语地区的规则。

第二个参数是一个将`type`设置为`'ordinal'`的对象，它让我们返回顺序规则。

接下来，我们用规则创建`suffixes`对象。

然后我们用`number`调用`select`方法返回`'one'`、`'two'`、`'few'`或`'other'`。

因此`suffix`将是`suffixes`中的属性值之一。

最后，我们返回连接在一起的`number`和`suffix`。

因此控制台日志应该记录`'101st'`。

# 结论

我们可以使用`Intl.PluralRules`构造函数给 JavaScript 数字添加一个序号后缀。

*更多内容尽在* [***说白了***](http://plainenglish.io)