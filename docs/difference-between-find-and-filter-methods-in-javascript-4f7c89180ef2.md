# JavaScript 中 find()和 filter()方法的区别

> 原文：<https://javascript.plainenglish.io/difference-between-find-and-filter-methods-in-javascript-4f7c89180ef2?source=collection_archive---------6----------------------->

## JavaScript 中的 find()和 filter()方法有什么区别

![](img/570effb8b24d26d09b30ad0e5c04c1fa.png)

Photo by [Andrew Neel](https://unsplash.com/@andrewtneel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 在 ES6 上有很多数组方法。每种方法都有独特的用法和优点。

而开发应用程序大多使用数组方法来获取特定的值列表，并获取单个或多个匹配项。

在列举两种方法的区别之前，我们先逐一了解一下方法。

# JavaScript 数组查找()

ES6 `*find()*` 方法返回通过测试函数的第一个元素的值。如果没有满足测试函数的值，则返回`undefined`。

**语法**

[*箭头功能*](https://medium.com/swlh/es6-arrow-functions-in-javascript-54f244f6c7cd) 用在下面的语法中。

```
find((element) => { /* ... */ } )
find((element, index) => { /* ... */ } )
find((element, index, array) => { /* ... */ } )
```

我们有一个带有`name` `age`和`id`属性的用户对象列表，如下所示:

```
let users = [{
    id:1,
    name: 'John',
    age: 22
}, {
    id:2,
    name: 'Tom',
    age: 22
}, {
    id:3,
    name: 'Balaji',
    age: 24
}];
```

下面的代码使用`find()`方法查找第一个年龄大于 23 岁的用户。

```
console.log(users.find(user => user.age > 23));//console
//{ id: 3, name: 'Balaji', age:24}
```

现在我们要找到第一个年龄为 22 岁的用户

```
console.log(users.find(user => user.age === 22));//console
//{ id: 1, name: 'John', age:22}
```

假设没有找到匹配意味着它返回`undefined`

```
console.log(users.find(user => user.age === 25));//console
//undefined
```

在 [MDN web 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/find)上了解更多`find()`方法

# JavaScript 数组过滤器()

`filter()`方法创建一个新数组，其中所有元素都通过了测试函数。如果没有元素满足测试函数，返回一个`empty`数组。

**语法**

```
filter((element) => { /* ... */ } )
filter((element, index) => { /* ... */ } )
filter((element, index, array) => { /* ... */ } )
```

我们将为过滤器示例使用相同的`users`数组和测试函数。

下面的代码使用`filter()`方法来查找第一个年龄大于 23 岁的用户。

```
console.log(users.filter(user => user.age > 23));//console
//[{ id: 3, name: 'Balaji', age:24}]
```

现在我们要过滤年龄为 22 岁的用户

```
console.log(users.filter(user => user.age === 22));//console
//[{ id: 1, name: 'John', age:22},{ id: 2, name: 'Tom', age:22}]
```

假设没有找到匹配意味着它返回一个`empty`数组

```
console.log(users.filter(user => user.age === 25));//console
//[]
```

在 [MDN web 文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)上了解更多`filter()`方法

# `find()`和`filter()`的区别

1.  **高阶函数**

这两个函数都是高阶函数。

2.**通过测试功能**

`find()`返回第一个元素

返回一个包含所有通过测试函数的元素的新数组

3.**如果没有值满足测试函数**

`find()`返回`undefined`

`filter()`返回一个`empty`阵

如果我遗漏了任何不同之处，请添加您的评论。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*