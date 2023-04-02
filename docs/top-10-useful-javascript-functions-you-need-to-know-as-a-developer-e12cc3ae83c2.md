# 作为开发人员，您需要知道的 10 个最有用的 JavaScript 函数

> 原文：<https://javascript.plainenglish.io/top-10-useful-javascript-functions-you-need-to-know-as-a-developer-e12cc3ae83c2?source=collection_archive---------4----------------------->

## **充分利用 JavaScript 的必备功能**

![](img/feb0c8db649490606ef83a6937069ca2.png)

Image from [freepik](https://www.freepik.com/free-vector/programmers-using-javascript-programming-language-computer-tiny-people-javascript-language-javascript-engine-js-web-development-concept-bright-vibrant-violet-isolated-illustration_10782951.htm#page=1&query=javascript&position=1)

> “JavaScript 是一个皮套，里面有一把非常非常锋利的刀。那把刀可以切任何东西，有了它，你可以做任何事情。你可以杀死一只熊。你可以抓鱼。你可以把一块木头削成一匹小马。它甚至是一根牙签。”—尼克·摩根

无论是后端还是前端，JavaScript 无处不在。无论是互联网上超过 90%的网站，还是移动开发等应用开发领域，甚至是机器学习，几乎所有东西都在 JavaScript 上运行。

成为一名精通 JavaScript 的开发人员需要的不仅仅是写代码——它需要技能、特定的心态，最重要的是，它需要很好地掌握重要的概念。

[](https://betterprogramming.pub/6-must-know-javascript-concepts-you-shouldnt-miss-as-a-web-developer-95dc180deb48) [## 作为一名 Web 开发人员，你不应该错过的 6 个必须知道的 Javascript 概念

### 用五分钟时间了解最基本的 JS 概念

better 编程. pub](https://betterprogramming.pub/6-must-know-javascript-concepts-you-shouldnt-miss-as-a-web-developer-95dc180deb48) 

所以，这里是作为一个成功的开发者应该知道的前 10 个 JavaScript 函数。

# 1.过滤器( )

`filter()`是一个非常有用的函数，在许多情况下都有应用。filter 方法创建一个新的数组，其中填充了通过由`callback()`函数实现的测试的所有数组元素。

`filter()`方法在内部遍历每个数组元素，然后将每个元素传递给`callback()`函数——如果`callback()`函数返回`true`，它会将该元素包含在返回的数组中。

**语法:**

```
array.filter(callback(element, index, arr), thisValue)
```

**例如:**

在这个例子中，`filter()` 方法创建了一个新的数组，它只包含那些满足`Positive()`函数所检查的条件的元素。

**输出:**

```
[49, 567, 100, 704]
```

# 2.地图( )

不了解`map()`方法，完全不可能了解重要的 JavaScript 函数！

JavaScript 中的`map()`方法创建一个新的数组，其结果是为每个数组元素调用一个函数。简单地说，`map()`将自己附加到一个数组中，并帮助将每一项转换成另一项，从而产生一个新的数组。

**语法:**

```
array.map(function(currentValue, index, arr), thisValue)
```

**例如:**

在下面的例子中，我们可以使用`map()`方法将所有数组元素转换成 60。

**输出:**

```
[Number: 60]
[Number: 60]
[Number: 60]
[Number: 60]
```

# 3.一些( )

JavaScript `some()`方法测试数组中的某个元素是否通过了由提供的函数实现的测试。如果测试通过，它返回`true()`。否则，返回`false`。

**语法:**

```
array.some(callback[, thisObject]);
```

**例如:**

**输出:**

```
false
```

# 4.每隔( )

方法检查数组的所有元素是否满足给定的条件。该条件由作为参数传递给它的方法提供。

**语法:**

```
arr.every(callback(element[, index[, array]])[, thisArg])
```

**示例:**在下面的示例中，`every()`方法检查数组中的每个元素是否都是正数，因为所有数组都包含正元素和零个负元素，所以返回值为`true`。

**输出:**

```
true
```

# 5.减少( )

大多数 JavaScript 开发人员都避免使用`reduce()`,因为它在概念和执行上都很难理解。

`reduce()`方法将数组简化为单个值，并为数组的每个值执行一个提供的函数(从左到右)，累加器用于存储函数的返回值。

**语法:**

```
array.reduce( function(total, currentValue, currentIndex, arr), 
initialValue )
```

**例如:**

在下面的例子中，`reduce()`方法对数组的每个元素执行一个`reducer`函数(由您提供),产生一个输出值。

**输出:**

```
18
23
```

# 6.扁平( )

`flat()`方法是一种内置的数组方法，在 JavaScript 的函数式编程范例中大量使用。

这个方法基本上将一个给定的数组展平成一个新创建的一维数组，还连接给定多维数组的所有元素，并展平到指定的深度。

**语法:**

```
arr.flat([depth])
```

**例子:**

在下面的例子中，我们使用了`Infinity`来递归展平数组到任意深度。

**输出:**

```
[ 1, 2, 3, 4, 5 ]
[ 1, 2, 3, 4, [ 5, 6 ] ]
[ 1, 2, 3, 4, 5, 6 ]
[
  1, 2, 3, 4,  5,
  6, 7, 8, 9, 10
]
[ 1, 3 ]
```

# 7.填充( )

`fill()`是 JavaScript 中预定义的函数，用指定的静态值填充给定数组的元素。它基本上将数组中的所有元素都变成一个静态值，从起始索引(默认为`0`)到结束索引(默认为`array.length`)。

**语法:**

```
arr.fill(value, start, end)
```

**示例:**

**输出:**

```
Array [1, 2, 0, 0]
Array [1, 5, 5, 5]
Array [6, 6, 6, 6]
```

# 8.findIndex()

`findIndex()`方法接收一个函数作为参数，并将它应用于数组。它基本上返回满足测试函数的元素的索引，如果没有元素通过测试，则返回-1。

**语法:**

```
array.findIndex(function(currentValue, index, arr), thisValue)
```

**例如:**

**输出:**

```
2
0
```

# 9.排序( )

`sort()`方法对数组元素进行排序，然后返回排序后的数组。当比较两个值时，`[sort()](https://www.w3schools.com/js/js_array_sort.asp)` [方法](https://www.w3schools.com/js/js_array_sort.asp)将值发送给比较函数，并根据返回值对值进行排序。

**语法:**

```
arr.sort(compareFunction)
```

**例如:**

在这个例子中，`sort()`方法根据应用于每个元素的函数对数组的元素进行排序。

**输出:**

```
904,91,98,75,28
904,91,98,75,28
```

# 10.shift()

`shift()`通过删除数组中的第一个元素来减少数组的长度。然后，它返回删除的元素。

**语法:**

```
arr.shift()
```

**例如:**

**输出:**

```
56
356,667,304
```