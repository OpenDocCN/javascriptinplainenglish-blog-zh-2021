# 如何检查 JavaScript FormData 实例？

> 原文：<https://javascript.plainenglish.io/how-to-inspect-the-javascript-formdata-instance-796cbeb408a4?source=collection_archive---------5----------------------->

![](img/92a4afd40caefb0638259041b2e5030e.png)

Photo by [Paulius Dragunas](https://unsplash.com/@paulius005?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们有一个 HTML 表单，那么输入的数据可能存储在从`FormData`实例创建的对象中。

在本文中，我们将看看如何检查从`FormData`构造函数创建的对象。

# 带有 entries 方法的 for-of 循环

我们可以使用 for-of 循环遍历`FormData`实例的键值对来检查它们的值。

为了获得键值对，我们可以使用`FormData`实例的`entries`方法来返回数组中的键值对。

例如，我们可以写:

```
const formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');for (const [key, value] of formData.entries()) {
  console.log(key, value);
}
```

然后我们得到:

```
key1 value1
key2 value2
```

我们用`FormData`构造函数创建了`formData`对象。

然后我们分别用键和值调用`append`，将条目添加到`formData`对象中。

接下来，我们调用`formData.entries`返回一个数组，数组中有键值对。

在 for-of 循环中，我们析构键值对并用`console.log`记录它们。

# 省略 entries 方法

我们可以省略`entries`方法，因为`formData`是一个可迭代的对象。

它有一个迭代器来返回键值对。

因此，我们可以将其简化为:

```
const formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');for (const [key, value] of formData) {
  console.log(key, value);
}
```

# 对象. fromEntries

我们还可以使用`Object.fromEntries`将键-值对放入一个易于检查的对象中。

这是因为一个`FormData`实例有一个迭代器，它返回数组中的键值对数组。

例如，我们可以写:

```
const formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');
console.log(Object.fromEntries(formData))
```

然后我们得到:

```
{key1: "value1", key2: "value2"}
```

从控制台日志中。

# 使用响应构造函数

我们可以使用`Response`构造函数将`FormData`实例转换成我们可以轻松检查的文本。

例如，我们可以写:

```
const formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');(async () => {
  const text = await new Response(formData).text()
  console.log(text)
})()
```

`text`方法返回一个承诺，所以我们把它放在一个异步函数中。

那么`text`大概是这样的:

```
------WebKitFormBoundaryzCHPG30oZJEPIn1B
Content-Disposition: form-data; name="key1"value1
------WebKitFormBoundaryzCHPG30oZJEPIn1B
Content-Disposition: form-data; name="key2"value2
------WebKitFormBoundaryzCHPG30oZJEPIn1B--
```

如果我们只关心检查它，那么我们可以使用`text`方法。

# 结论

有几种方法可以检查一个`FormData`实例。

它是一个 iterable 对象，所以我们可以对它使用 for-of 循环。

同样，我们可以将它转换成一个`Response`实例，并使用`text`方法来检查它。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)