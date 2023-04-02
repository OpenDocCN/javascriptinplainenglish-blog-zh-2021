# 如何用 JavaScript 获取和设置一个数据属性的值？

> 原文：<https://javascript.plainenglish.io/how-to-get-and-set-the-value-of-a-data-attribute-with-javascript-f0a1bd44063d?source=collection_archive---------2----------------------->

![](img/0217c892ac1db0c68cba48fcf52f22dd.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用`data-`属性，我们可以存储我们想要存储在 HTML 元素中的数据。

我们可能希望在我们的 web 应用程序中获得这些值。

我们可以用 JavaScript 来做这件事。

在本文中，我们将看看如何用 JavaScript 获取和设置元素的`data-id`属性值。

# getAttribute 方法

获取属性值的一种方法是使用本机可用的`getAttribute`方法。

例如，如果我们有下面的 HTML:

```
<div id='apple-tree' data-fruit='12'></div>
```

我们可以通过编写调用`getAttribute`来返回`data-fruit`属性的值；

```
const plant = document.getElementById('apple-tree');
const fruitCount = plant.getAttribute('data-fruit');
```

`fruitCount`应该是`'12'`，因为这是`data-fruit`属性的值。

为了改变`data-fruit`属性的值，我们可以写:

```
plant.setAttribute('data-fruit','10');
```

# 使用`dataset Property`

HTML 元素节点对象带有`dataset`属性，让我们获得以`data-`前缀开始的属性值。

例如，我们可以写:

```
const plant = document.getElementById('apple-tree');
console.log(plant.dataset.fruit)
```

为了获得`data-fruit`属性的值，我们使用了`plant.dataset.fruit`属性。

该属性也可以赋值，因此我们可以通过编写以下代码来设置`data-fruit`属性的值:

```
plant.dataset.fruit = 10
```

# jQuery

jQuery 让我们以各种方式获得以`data-`开头的属性值。

获取该值的一种方法是使用`data`方法。

例如，我们可以写:

```
console.log($('#apple-tree').data().fruit)
```

获取`data-fruit`属性的值。

`data`返回一个对象所有的`data-`属性名称，去掉了`data-`前缀。

对应的值是添加到元素中的属性值。

此外，我们可以写:

```
console.log($('#apple-tree').data('fruit'))
```

做同样的事情。

# 结论

我们可以通过使用`data-`属性在元素中存储数据。

我们可以用普通的 JavaScript 或 jQuery 获取和设置它们的值。

*更多内容看* [*说白了就是*](http://plainenglish.io/) *。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*