# JavaScript 中的高阶函数

> 原文：<https://javascript.plainenglish.io/higher-order-functions-in-javascript-4bd164d1df23?source=collection_archive---------10----------------------->

## 通过示例了解 JavaScript 中的高阶函数。

![](img/d19c3186874a74d4a9737f51457bdd17.png)

Photo by [Mimi Thian](https://unsplash.com/@mimithian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 中的高阶函数是以其他函数(回调)作为参数的函数。它们非常有用，因为它们可以使代码更干净，并允许我们轻松地用数组实现某些操作。

在本文中，我们将看看 JavaScript 中您应该知道的重要高阶函数。所以让我们开始吧。

# 为每一个

方法`forEach`是 JavaScript 中重要的高阶函数之一，因为它采用回调函数作为参数。它用于遍历数组元素。

回调函数可以接受三个参数:

*   数组中的元素(必需)。
*   数组中元素的索引(可选)。
*   数组本身(可选)。

让我们来看一个例子:

```
let numbers = [1, 4, 6, 8, 9];//ES5 syntax.
numbers.**forEach**(**function(number)**{
  console.log(number);
});/* output: 
1
4
6
8
9
*///ES6 syntax.
numbers.**forEach**(number => console.log(number));/* output: 
1
4
6
8
9
*/
```

正如您在上面看到的，方法`forEach`循环遍历数组中的每个元素，并在控制台中打印输出。它不会改变原始数组。

为了简单起见，我们只使用了回调函数中的第一个参数。因此，如果您愿意，可以添加另外两个可选参数。

# 地图

高阶函数`map()`有点类似于`forEach`。它用于遍历数组元素，但它返回一个新数组，其中包含我们应用于它的回调函数的结果。

回调需要像`forEach`一样的三个参数:

*   数组中的元素(必需)。
*   索引(可选)。
*   数组(可选)。

这里有一个例子:

```
let numbers = [1, 4, 6, 8, 9];//ES5 syntax.
numbers.**map**(function(**number**){
  return **number * 2**;
}); 
//output: [2, 8, 12, 16, 18]// ES6 syntax.
numbers.**map**(**number** => **number * 2**);
//output: [2, 8, 12, 16, 18]
```

如您所见，我们使用 map 方法遍历数组中的每个数字，并将其乘以 2。结果，我们得到一个新的数组，其中包含乘以 2 的数字。

所以高阶函数`map()`不会改变原始数组`numbers`，而是返回一个新数组。

如果你想知道`map`和`forEach`的区别，可以看看我下面的文章:

[](/the-difference-between-foreach-and-map-in-javascript-f369c3207e50) [## JavaScript 中 ForEach 和 Map 的区别

### JavaScript 方法:forEach VS map 及示例。

javascript.plainenglish.io](/the-difference-between-foreach-and-map-in-javascript-f369c3207e50) 

# 过滤器

高阶函数`filter`也采用一个回调函数，有三个参数，像`map`和`forEach`。它遍历数组元素，然后返回一个新数组，该数组只包含满足我们传递给回调函数的条件的元素。所以我们用这个方法从数组中过滤元素。

这里有一个例子:

```
let numbers = [1, 4, 6, 8, 9];//ES5 syntax.
numbers.**filter**(function(**number**){
  return **number > 4**;
});
//output: [6, 8, 9]// ES6 syntax.
numbers.**filter**(**number** => **number > 4**);
//output: [6, 8, 9]
```

正如您在上面看到的，方法`filter`遍历数组元素，它返回一个只包含大于 4 的元素的新数组。所以它不改变原来的数组`numbers`。

同样，为了简单起见，我们只使用回调的第一个参数。如果需要，您可以添加其他参数。

# 减少

方法`reduce()`是一个高阶函数，它将另一个回调函数作为其参数。

回调本身有四个参数:

*   累加器(强制)用于返回前一次迭代中回调函数的值。
*   元素值(必需)。
*   元素索引(可选)。
*   然后是数组本身(可选)。

reduce 方法用于在遍历数组中的每个元素后将数组缩减为单个值。

以下示例使用 reduce 方法获取数组中所有数字的总和:

```
let numbers = [1, 4, 6, 8, 9];//ES5 syntax.
numbers.**reduce**(function(**accumulator**, **value**){
  return **accumulator + value**;
});
// output: 28// ES6 syntax.
numbers.**reduce**((**accumulator**, **value**) => **accumulator + value**);
// output: 28
```

如果你想要更多关于方法`reduce`和更多其他高阶函数的解释，你可以看看我下面的文章:

[](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) [## 举例说明 JavaScript 中的 Reduce 方法

### 通过示例了解 JavaScript 中的 reduce 方法。

javascript.plainenglish.io](/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) [](/the-methods-some-and-every-in-javascript-8b303a36eaae) [## JavaScript 中的一些和所有方法

### 了解一些高阶函数。

javascript.plainenglish.io](/the-methods-some-and-every-in-javascript-8b303a36eaae) 

# 结论

高阶函数在 JavaScript 中非常重要和有用。它们允许您轻松地使用数组，并使您的代码更加整洁。除此之外，在使用 React 和 Vue 等框架时，您也会需要它们。

感谢您阅读这篇文章。希望你觉得有用。