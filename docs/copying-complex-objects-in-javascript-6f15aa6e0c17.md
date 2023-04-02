# 在 JavaScript 中复制复杂对象

> 原文：<https://javascript.plainenglish.io/copying-complex-objects-in-javascript-6f15aa6e0c17?source=collection_archive---------10----------------------->

## 克隆类实例和其他复杂类型

![](img/d73c8d8b44f9818af8866b5d53f62872.png)

Photo by [Francesco Tommasini](https://unsplash.com/@tomma5588?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/relfection?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## TL；博士；医生

使用`Object.getOwnPropertyDescriptor`并遍历原型链。

有许多关于如何克隆对象的文章。今天，使用[扩展操作符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)通常是复制简单对象的首选方式。理解 spread 语法有一些限制是很重要的。

主要缺点是不能复制访问器方法。`Object.assign`也有同样的问题。在使用访问器方法的系统中，这不是可选的。第二个问题是方法不能被复制。为了创建类实例和其他复杂对象的深层副本，我们需要另一个解决方案。我创建了一个简单的复制方法来遍历继承链，你可以在这里查看。源代码如下。

在这个例子中，我使用`Object.getOwnPropertyDescriptor`来获取所有属性，包括那些**而不是** [枚举](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Enumerability_and_ownership_of_properties)的属性。然后我们遍历继承链，重复这个过程。我们使用`Object.defineProperty`添加特殊处理来克隆我们的访问器方法。这捕获了所有的变量、访问器和方法，产生了原始文件的完美副本！

> 注意:TypeScript 不枚举访问器方法！

在较新版本的 TypeScript 中，所有的访问器方法都是[而不是](https://github.com/microsoft/TypeScript/issues/38587)枚举的。这导致许多开发人员创建 decorators 作为临时的解决方法。它还破坏了几个依赖于能够自省对象的代码库，包括我的。当您想要获取一个对象的所有属性，甚至是那些没有被枚举的属性时，这种解决方案也是有用的。