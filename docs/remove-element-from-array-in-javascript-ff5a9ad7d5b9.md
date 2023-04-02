# 在 JavaScript 中从数组中移除元素

> 原文：<https://javascript.plainenglish.io/remove-element-from-array-in-javascript-ff5a9ad7d5b9?source=collection_archive---------16----------------------->

## 如何在 JavaScript 中从数组中移除元素

![](img/19c445d1c99c14e8ddbe6baf041aaabb.png)

A balloon flying away (being removed) from an array.

您应该知道四种可以用来从 JavaScript 数组中移除元素的数组方法:

*   **shift** —从数组的**开头**处删除
*   **弹出** —从数组的**端**移除
*   **拼接** —从数组中的特定**索引**(位置)中删除
*   **filter**—通过编程从数组中移除**元素****(基于您定义的标准)**

# **如何从 JavaScript 数组的开头移除元素**

**如何移除 JavaScript 数组的第一个元素？**

**`shift()`函数删除 JavaScript 数组的第一个元素，返回该元素，并更新 length 属性。**

```
let arr = ['a', 'b', 'c', 'd'];arr.shift(); // returns "a"console.log(arr); // ["b", "c", "d"]
```

**如果我们想从`arr`获取第一个值，我们可以做一些类似`let val = arr.shift();`的事情。**

**`shift()`函数不带任何参数。它只是从数组中删除第一个值。**

**然后，数组中的剩余值向前移动。换句话说，原来在索引位置 1 的东西现在会在索引位置 0。**

**如果没有元素，或者数组长度为 0，函数返回`undefined`。**

# **如何从 JavaScript 数组的末尾移除元素**

**`pop()`函数移除数组的最后一个元素，返回该元素，并更新 length 属性。**

```
let arr = ['a', 'b', 'c', 'd'];arr.pop(); // returns 'd'console.log( arr ); // ['a', 'b', 'c']
```

**如果我们想从`arr`获取第一个值，我们可以做一些类似`let val = arr.pop();`的事情。**

**像`shift()`函数一样，`pop()`不接受任何参数。它只是从数组中删除最后一个值。**

**如果数组为空，`pop()`函数将返回`undefined.`**

# **如何用 splice()移除 JavaScript 数组元素**

**`splice()`函数可用于添加或删除数组中的元素。**

**这需要两个参数。第一个参数指定开始添加或移除元素的位置。第二个参数指定要删除的元素数量。**

**让我们看一个例子:**

```
let arr = ['a', 'b', 'c', 'd'];let splicedArr = arr.splice(1,3);console.log(splicedArr) // ['b, 'c', 'd']console.log(arr) // ['a']
```

**查看`let splicedArr = arr.splice(1,3);`，传递给`splice()`的`1`的第一个参数表示我们想要开始的索引位置。因此`1`的索引位置将是`'b'`。`3`的第二个参数表示我们想从`'b'`的位置取 3 个值。因此，`splicedArr`返回`['b', 'c', 'd']`。**

# **如何使用 filter()通过值从 JavaScript 数组中移除项**

**`filter()`返回一个新的数组，而不是改变现有的数组。**

**`filter()`函数接受单个参数，这是一个回调函数，每次`filter()`遍历使用它的数组元素时都会被触发。**

**这个回调函数可以接受三个参数。第一个参数是数组中的当前值。第二个参数是当前数组索引。第三个参数是完整的数组。第一个参数是必需的，而第二个和第三个参数是可选的。**

**当`filter()`函数根据标准从数组中删除值时，与之比较的标准必须返回`true`或`false`。在比较数组中的每个值时，返回`true`的值将被添加到返回的新数组中，而返回`false`的值将不会被添加。**

**例如:**

```
let array = [1, 2, 3, 4, 5];let filtered = array.filter(value => value > 3);console.log(filtered) // [4, 5];
console.log(array) // [1, 2, 3, 4, 5];
```

**如您所见，`filtered`返回的值高于`array`中的`3`值，而原始的`array`变量保持不变。**

# **结论**

**我们讨论了所有 JavaScript 开发人员都应该知道的四种有用的数组方法。这样做，您将能够根据不同的需求移除元素。**

**我希望你已经发现这是有用的。如果是这样，一定要在评论中让我们知道你的想法。**

***更多内容尽在* [***说白了***](http://plainenglish.io)**