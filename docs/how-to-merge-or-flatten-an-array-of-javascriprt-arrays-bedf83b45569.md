# 如何合并或展平一个 JavaScript 数组的数组？

> 原文：<https://javascript.plainenglish.io/how-to-merge-or-flatten-an-array-of-javascriprt-arrays-bedf83b45569?source=collection_archive---------15----------------------->

![](img/bc9235f6b83c3fa455c9ca41bc558847.png)

Photo by [Hernan Lucio](https://unsplash.com/@hernanlucio?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望合并或展平 JavaScript 数组的数组。

在本文中，我们将研究如何合并或扁平化 JavaScript 数组。

# 数组.原型.串联

`concat`方法让我们将数组中的项目作为参数添加到调用它的数组中。

例如，我们可以写:

```
const arrays = [
  ["1"],
  ["2"],
  ["3"],
  ["4"],
  ["5"],
  ["6"],  
];
const merged = [].concat(...arrays);
console.log(merged);
```

我们将`arrays`中的条目扩展到`concat`方法。

来自`arrays`中数组的所有条目将被添加到它所调用的空数组中并返回。

因此，我们得到`[“1”, “2”, “3”, “4”, “5”, “6”]`作为`merged`的结果。

# 数组.原型.平面

ES2019 附带了`flat`方法，让我们可以根据需要展平任意级别的数组。

例如，我们可以写:

```
const arrays = [
  ["1"],
  ["2"],
  ["3"],
  ["4"],
  ["5"],
  ["6"],  
];
const merged = arrays.flat(1);
console.log(merged);
```

然后我们得到和以前一样的结果。

我们将 1 传递给`flat`以将数组展平一级。

如果我们不传入一个参数，那么它会递归地展平，直到没有数组需要展平。

# 编写我们自己的函数

此外，我们可以编写自己的函数来递归展平数组。

例如，我们可以写:

```
const arrays = [["1"], ["2"], ["3"], ["4"], ["5"], ["6"]];const flatten = (arr) => {
  return arr.reduce((flat, toFlatten) => {
    if (Array.isArray(toFlatten)) {
      return flat.concat(...flatten(toFlatten));
    }
    return flat.concat(toFlatten);
  }, []);
};
const merged = flatten(arrays);
console.log(merged);
```

创建`flatten`功能。

我们检查`toFlatten`是否是`reduce`回调中的数组。

`reduce`让我们将多个数组中的项目组合成一个数组。

如果是，那么我们返回调用的返回值`flat.concat`，将`flatten(toFlatten)`展开到`concat`中作为参数。

否则，我们只返回`flat.concat(toFlatten)`的结果，因为`toFlatten`不是一个数组。

这意味着我们可以将它直接放入`flat`数组。

`reduce`的第二个参数是`reduce`在放入任何东西之前的初始返回值。

# 结论

展平或合并嵌套数组最简单的方法是使用数组附带的`flat`方法。

我们也可以使用`concat`方法来展平嵌套数组中的一层。

另一种选择是创建我们自己的函数来展平数组。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)