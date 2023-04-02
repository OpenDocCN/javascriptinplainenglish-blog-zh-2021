# 举例说明 JavaScript 中的 Reduce 方法

> 原文：<https://javascript.plainenglish.io/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6?source=collection_archive---------4----------------------->

## 通过示例了解 JavaScript 中的 reduce 方法。

![](img/b84042285b2ab74aaa14e9bedef91b57.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

reduce 方法是 JavaScript 函数式编程模式中重要的高阶函数之一。高阶函数基本上就是以另一个函数为自变量的函数。很多初学者很难理解 JavaScript 中的 reduce 方法，这就是我决定写这篇文章的原因。

在本文中，我们将通过一些实例来学习 JavaScript 中的 reduce 方法。让我们开始吧。

# reduce 方法的作用

JavaScript 中的方法`reduce()`用于数组。它在迭代完每一项后将数组缩减为一个值。该方法将回调函数作为参数。

回调函数接受四个参数。第一个参数被称为累加器，它从上一次迭代中获得回调函数的返回值，第二个参数是正在处理的当前元素，第三个参数是该元素的索引，第四个参数是调用`reduce`的数组。最后两个参数是可选的，我们只在需要的时候使用它们。

让我们看一个简单的例子:

下面的例子使用方法`reduce()`获得所有数组编号的总值:

```
const arr = [29, 46, 86.5];

const sum = arr.**reduce**((total, value) => **total + value**);
console.log(sum);
// 161.5
```

正如您在示例中看到的，reduce 方法使用了前两个强制参数，total 和 current 值。它像在 for 循环中一样迭代数组中的每个数字。当循环开始时，总值是最左边的数字(29)，当前值是它旁边的数字(46)。我们希望将当前值添加到总数中。

对数组中的每个值重复计算，但每次当前值都变为数组中的下一个数字，向右移动，直到数组中不再有数字。然后它返回总数。

如果您对 ES6 不熟悉，下面是使用 ES5 语法的相同示例:

```
var arr = [29, 46, 86.5]; 

var sum = arr.reduce( function(total, value){
  return **total + value**
});

console.log(sum); // 161.5
```

# 累加器

除了回调函数，`reduce`还有一个额外的参数，它接受累加器的初始值。如果不使用第二个参数，则跳过第一次迭代，第二次迭代将数组的第一个元素作为累加器传递。

下面是同样的例子，累加器作为`reduce`的第二个参数:

```
const arr = [29, 46, 86.5];

const sum = arr.reduce((total, value) => total + value**, 0**);
console.log(sum);
// 161.5
```

将数字 10 设置为累加器:

```
const arr = [29, 46, 86.5];

const sum = arr.reduce((total, value) => total + value**, 10**);
console.log(sum);
// 171.5
```

如您所见，累加器被添加到数组值的总数中。

# 对象化简方法

下面是一个使用`users`数组上的`reduce`返回所有用户年龄总和的例子。

```
const users = [
  { name: 'John', age: 34 },
  { name: 'Mehdi', age: 19 },
  { name: 'Alex', age: 10 }
];

const sumOfAges = users.reduce((sum, user) => sum + **user.age**, 0);
console.log(sumOfAges); // 63
```

在另一个例子中，看看如何返回一个对象，该对象包含作为属性的用户名和作为值的年龄。

```
const users = [
  { name: 'John', age: 34 },
  { name: 'Mehdi', age: 19 },
  { name: 'Alex', age: 10 }
];

const usersObj = users.reduce((obj, user) => {
  **obj[user.name] = user.age;
  return obj;** }, {});
console.log(usersObj); // { John: 34, Mehdi: 19, Alex: 10 }
```

为了简单起见，示例只使用了回调函数中的第一个和第二个参数。

# 结论

对于 JavaScript 中的函数式编程，reduce 方法非常重要和有用。它与数组一起使用，不改变原始数组。我鼓励您从 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 文档中了解更多信息。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，还可以* [*订阅*](https://exciting-musician-9042.ck.page/60477323b8) *我们的简讯。*

*这里还有一篇有用的文章需要检查:*

[](https://medium.com/javascript-in-plain-english/the-arguments-object-in-javascript-explained-with-examples-34197acb68a5) [## 举例说明 JavaScript 中的 Arguments 对象

### 通过实例了解 arguments 对象。

medium.com](https://medium.com/javascript-in-plain-english/the-arguments-object-in-javascript-explained-with-examples-34197acb68a5)