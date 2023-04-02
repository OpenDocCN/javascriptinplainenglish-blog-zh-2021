# JavaScript 算法:排序联合

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-sorted-union-3c36744efb27?source=collection_archive---------5----------------------->

## 让我们使用 JavaScript 来解决排序并算法

![](img/a78c2258d3e7aafd77f4ddbb46434cae.png)

Photo by [Tudor Baciu](https://unsplash.com/@baciutudor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

解决算法是提高你解决问题能力的最好方法之一。这也允许你用特定的编程语言来练习你的编码技能。求解算法需要遵循一系列步骤，以便解决问题或实现特定结果。这就是为什么把你的算法分解成小部分总是更好的原因，这使得解决它更容易。

在本文中，我们将尝试使用 JavaScript 的力量来解决排序并算法。让我们开始吧。

# 说明

排序联合算法是将一组数字数组统一到一个由*个唯一的*个数字组成的数组中。

这里有一个例子:

```
//    **Before**                  ** =>**   **After**
[1, 2, 3], [5, 2, 1]           **=>** [1, 2, 3, 5]//    **Before**                  ** =>**   **After**
[1, 3, 2], [5, 2, 1, 4], [2, 1]**=>** [1, 3, 2, 5, 4]
```

我们有一个名为`uniteUnique`的函数，它可以接受一组数组作为它的参数`arr`。

这里有一个例子:

```
function **uniteUnique**(arr) {
 //Your code here.}
uniteUnique**([1, 3, 2], [5, 2, 1, 4], [2, 1], [5,7,5,7])** //Should return [ 1, 3, 2, 5, 4, 7 ]uniteUnique**([1, 2, 3], [5, 2, 1])** //Should return [ 1, 2, 3, 5 ]//The same thing applies to all arrays of numbers you will pass as an argument for this function.
```

正如您在上面看到的，该函数接受两个或多个数组，并按照最初提供的数组的顺序返回一个新的唯一值数组。最终数组中没有重复项。

现在，在滚动到我们的解决方案之前，我真的鼓励你想一想使用 JavaScript 实现上述指令的一些方法。总是试着把问题分解成小部分，并专注于每一部分，让事情对你来说更容易。

# 求解算法

我解决这个算法的方法是首先使用 arguments 对象来获取所有传递给函数的参数(数组)。

下面是 JavaScript 中 argument 对象的一个简单示例:

```
function uniteUnique(arr) {
 console.log(**arguments**);
}uniteUnique**([1, 2, 3], [5, 2, 1]);**
```

*输出:*

```
{ '0': **[ 1, 2, 3 ]**, '1': **[ 5, 2, 1 ]** }
```

如您所见，arguments 对象允许我们获取传递给函数`uniteUnique`的所有参数。这将使我们能够使用 for 循环遍历该参数的对象，以便将所有数字数组推入另一个空数组。

之后，将数组推入一个新的空数组，我们可以用`flat()`展平这个新数组，并使用 set 对象删除重复的数字。

下面是我们解决这个算法的步骤:

*   我们创建了一个新的空数组，将在其中推送数组。
*   我们使用 for 循环迭代从 arguments 对象获得的数组，以便将它们推到新的空数组中。
*   我们使用扁平化方法来扁平化数组。
*   最后，我们使用 set 对象删除重复的数字，并在数组中拥有唯一的值。

*完成上述步骤:*

让我们创建一个名为`containerArr`的新的空数组，并使用一个 for 循环来迭代从 arguments 对象获得的数组，以便将它们推送到新的空数组中:

```
function uniteUnique(arr) {//Create an empty array.
let containerArr = [];// loop over the arguments object to push the arrays.
for(let i = 0; i < arguments.length; i++){
 containerArr.push(arguments[i]);
}console.log(containerArr); //output: [ [ 1, 2, 3 ], [ 5, 2, 1 ] ]
}uniteUnique([1, 2, 3], [5, 2, 1]);
```

现在我们需要展平数组`containerArr`并使用 set 对象删除重复的数字，以获得唯一的值。

看看下面的例子:

```
let flattedArr =  containerArr.**flat()**; //output:[ 1, 2, 3, 5, 2, 1 ][**...new Set(flattedArr)**]; //output: [ 1, 2, 3, 5 ]
```

这是我们算法的完整解决方案:

```
function uniteUnique(arr) { //Create an empty array.
 let containerArr = **[]**;// loop over the arguments object to push the arrays.
for(let i = 0; i < **arguments.length**; i++){
  containerArr.push(**arguments[i]**);
}//Using the flat method.
let flattedArr =  containerArr.**flat()**;//Remove duplicates.
return [**...new Set(flattedArr)**];}uniteUnique([1, 2, 3], [5, 2, 1]); //returns [ 1, 2, 3, 5 ]uniteUnique([1, 2, 3], [5, 2, 1, 4], [2, 1], [6, 7, 8]); //returns [1, 2, 3, 5, 4, 6, 7, 8].
```

就这样，现在函数按顺序返回唯一数字的统一数组。

# 结论

算法是练习你解决问题能力的好方法。这就是我解决这个简单算法的方法。如果你知道其他解决的方法，请告诉我。

感谢您阅读这篇文章。希望你觉得有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*下面是另一篇有用的文章，请点击链接查看:*

[](https://medium.com/javascript-in-plain-english/the-difference-between-foreach-and-map-in-javascript-f369c3207e50) [## JavaScript 中 ForEach 和 Map 的区别

### JavaScript 方法:forEach VS map 及示例。

medium.com](https://medium.com/javascript-in-plain-english/the-difference-between-foreach-and-map-in-javascript-f369c3207e50)