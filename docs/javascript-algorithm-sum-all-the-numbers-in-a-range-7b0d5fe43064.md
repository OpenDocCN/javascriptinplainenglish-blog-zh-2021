# JavaScript 算法:对一个范围内的所有数字求和

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-sum-all-the-numbers-in-a-range-7b0d5fe43064?source=collection_archive---------3----------------------->

## 让我们使用 JavaScript 来获得一个范围内所有数字的总和。

![](img/d0a3a4eb18593e752d1f5bfd0691fda1.png)

Photo by [Clément Hélardot](https://unsplash.com/@clemhlrdt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将尝试解决一个算法，返回一个范围内所有数字的总和。让我们开始吧。

# 说明

我们有一个名为`sumAll`的函数，它接受一个数组作为参数。

这里有一个例子:

```
function sumAll(arr) { // Your code here.}sumAll([1, 4]); //should return 10.
sumAll([1,5]); //should return 15.
sumAll([5,1]); //should return 15.
sumAll([5,5]); //should return 5.
```

正如您在上面看到的，该函数将表示数字范围的数组作为其参数。我们的任务是获取该范围内的所有数字并返回它们的总和。例如，`sumAll([5,1])`应该返回`15`，因为 1 到 5(包括 1 和 5)之间的所有数字之和是`15`。

JavaScript 中有很多方法可以解决这个算法。其中之一是使用循环来获取范围内的所有数字。我们将在下面讨论所有这些。

# 求解算法

我解决这个算法的方法是首先使用一个 for 循环来获取我们作为数组传递给函数的范围内的所有数字。

例如，假设我们有一个范围`[1,5]`，我们想得到这个范围内的所有数字，包括 1 和 5。我们可以在下面的例子中做到这一点:

```
let i = 1;for(let i = 1; i <= 5; i++){
 console.log(i);
}
//returns: 1 2 3 4 5
```

如你所见，你只需要有一个最小值(1)和一个最大值(5)。通过使用 for 循环，可以很容易地得到两个值之间的数字。

对于我们的算法，我们首先需要定义数组中的最小值和最大值，因为它们不会总是按顺序出现。比如你可以有[5，1]而不是[1，5]。我们可以使用`Math.min`和`Math.max`来做到这一点。

看看下面的例子:

```
**function** **sumAll**(arr) {
 //max value of arr.
 let max = **Math.max(arr[0], arr[1])**;//min value of arr.
 let min = **Math.min(arr[0], arr[1])**;
}
```

因为我们有了最小值和最大值，现在我们只需要使用一个 for 循环来获取所有的数字，并将它们放入另一个数组中，以获取所有这些数字的总和，因为这是我们这个算法的目标。

这里有一个例子:

```
**function** **sumAll**(arr) {
 //max value of arr.
 let max = Math.max(arr[0], arr[1]);//min value of arr.
 let min = Math.min(arr[0], arr[1]);//Create an empty array.
let newArr = [];//Using a for loop.
 for(**let i = min; i <= max; i++**){
  //push all the numbers to the new array.
  **newArr.push(i)**;
 }}
```

如您所见，我们获得了该范围内的所有数字，并将它们推到一个新数组中。例如，如果范围`arr`是`[5,1]`，则`newArr`将是`[1,2,3,4,5]`。

现在我们唯一需要做的就是使用 reduce 方法得到`newArr`中所有数字的总和。这样一来，我们的算法就解决了。

如果你不熟悉 reduce 方法，你可以看看我下面的文章:

[](https://medium.com/javascript-in-plain-english/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) [## 举例说明 JavaScript 中的 Reduce 方法

### 通过示例了解 JavaScript 中的 reduce 方法。

medium.com](https://medium.com/javascript-in-plain-english/the-reduce-method-in-javascript-explained-with-examples-6232b85e47f6) 

下面是一个如何得到`newArr`中所有数字总和的例子:

```
let sum;
sum = newArr.reduce((a,b)=> a + b);
```

这是我们算法的完整解决方案:

```
**function** **sumAll**(arr) {
 //max value of arr.
 let max = Math.max(arr[0], arr[1]);//min value of arr.
 let min = Math.min(arr[0], arr[1]);//Create an empty array.
let newArr = [];//Using a for loop.
 for(**let i = min; i <= max; i++**){
  //Push all the numbers to the new array.
  **newArr.push(i)**;
 }// Get the sum of all the numbers inside newArr.
let sum;
sum = newArr.**reduce**((a,b)=> a + b);// finally, just return the sum.
 **return sum;** }sumAll([1,4]); // returns 10.
sumAll([11,15]); //returns 65.
```

就这样，现在函数返回一个范围`arr`中所有数字的总和。

# 结论

算法是练习你解决问题能力的好方法。这就是我解决这个简单算法的方法。如果你知道其他解决的方法，请告诉我。

感谢您阅读这篇文章。希望你觉得有用。

## 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，也可以* [*订阅*](https://mehdiouss.ck.page/) *我的快讯。*

*下面是另一篇有用的文章，请点击链接查看:*

[](https://medium.com/javascript-in-plain-english/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba) [## 10 个令人敬畏的前端开发工具来提高您的生产力

### 你可能需要用到的有用的前端开发工具。

medium.com](https://medium.com/javascript-in-plain-english/10-awesome-front-end-development-tools-to-boost-your-productivity-b1d2efc4c4ba)