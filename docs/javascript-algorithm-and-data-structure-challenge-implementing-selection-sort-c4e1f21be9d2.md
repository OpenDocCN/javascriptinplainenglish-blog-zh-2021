# JavaScript 算法和数据结构挑战—实现选择排序

> 原文：<https://javascript.plainenglish.io/javascript-algorithm-and-data-structure-challenge-implementing-selection-sort-c4e1f21be9d2?source=collection_archive---------18----------------------->

## JavaScript 中的选择排序挑战 freeCodeCamps 的一个编程挑战的解决方案。

![](img/c4070c0b88be639ab581ff19178fe908.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们一直在学习如何解决来自各种平台的算法和数据结构的挑战，只是为了提高我们解决问题的技术。

如果您错过了最后一项挑战，请查看以下链接:

[](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) [## JavaScript 算法和数据结构挑战——Fizz Buzz

### JavaScript 中的 Fizz Buzz challenge 黑客团队的一个编程挑战的解决方案。

javascript.plainenglish.io](/javascript-algorithm-and-data-structure-challenge-fizz-buzz-5ef81800cb99) 

## **挑战:**

这里我们将实现选择排序。选择排序的工作方式是选择列表中的最小值，并将其与列表中的第一个值交换。然后，它从第二个位置开始，选择剩余列表中的最小值，并与第二个元素交换。它继续遍历列表并交换元素，直到到达列表的末尾。现在列表已排序。选择排序在所有情况下都具有二次时间复杂度。

说明:

编写一个函数 selectionSort，它将一个整数数组作为输入，并以这些整数的数组的形式返回，这些整数按从最小到最大的顺序排序。

注意事项:

我们在幕后调用这个函数；我们使用的测试数组在编辑器中被注释掉了。尝试日志数组，看看你的排序算法在行动！

*   selectionSort 应该是一个函数
*   selectionSort 应该返回一个排序后的数组(从最小到最大)
*   selectionSort 应返回一个除顺序外不变的数组。
*   selectionSort 不应使用内置的。sort()方法

```
function selectionSort(array) { // change code below this line
 return array;
 // change code above this line
}toSort = [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]; 
```

## **我们的解决方案**

```
function selectionSort(array) {// change code below this line
 for (let index = 0; index < array.length — 1; index++) {
 let leastElement = index;
 for (let j = index + 1; j < array.length; j++) {
 if (array[j] < array[leastElement]) {
 leastElement = j;
 }
 }
 // const temp = array[index];
 // array[index] = array[leastElement];
 // array[leastElement] = temp;
 // we can refactor the above code as shown below
 [array[index], array[leastElement]] = [array[leastElement], array[index]];}
 return array;
 // change code above this line}toSort = [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92];
console.log(selectionSort(toSort));
```

## **解说**

我们将执行第一次迭代，在提供的数组中找到一系列最小的元素。然后我们会找到数组中下一个最小的数，它是数组的长度减 1。

一旦我们用数组中最小的元素交换了第一个元素，那么一切都是有序的，所以我们不需要再返回。然后我们将执行另一个循环。对于这个内部循环，还记得在我们最初的 For 循环中，我们已经找到了数组中最少的元素，现在为了找到下一个最小的数，我们需要找到下一个数，在我们的例子中是 index + 1。

简单地说，在第一次迭代之后，我们的一些数字将会被锁定。此外，我们已经声明了索引的最小元素，以类似于给定数组中最少交换数字的位置。然后，我们可以使用条件 if 语句来测试相关的条件。

我们将测试 j 索引处的数组是否小于最小索引处的数组，然后我们将把索引中的最小元素设置为 j，这将一直进行下去，直到数组循环结束。

现在我们需要交换数组中的元素。我们将用最少的元素来改变当前的迭代。在这里，我们可以引入一个临时变量，并将其设置为索引处的数组，然后我们继续将它交换为最小元素处的数组，同样，将至少元素处的数组交换为临时变量。

正如我们从上面的解决方案中看到的，它不是一个纯函数。为什么不呢？尝试注销原始数组，我们可以看到它改变了原始数组，这对纯函数式编程不好。

## **更多重构:**

我们可以对数组进行浅层复制，并使用浅层复制的数组来代替提供的数组。我们可以使用。slice()方法。这个数组方法使我们能够对原始数组进行浅层复制。

如果你想了解更多关于数组方法的知识，请查看下面的链接。

[](/8-javascript-array-methods-you-should-know-81947c9e46de) [## 你应该知道的 8 种 JavaScript 数组方法

### JavaScript 中的数组方法你需要用例子来了解。

javascript.plainenglish.io](/8-javascript-array-methods-you-should-know-81947c9e46de) 

```
function selectionSort(array) {// change code below this lineconst shallowCopy = array.slice();
 for (let index = 0; index < shallowCopy.length — 1; index++) {
 let leastElement = index;
 for (let j = index + 1; j < shallowCopy.length; j++) {
 if (shallowCopy[j] < shallowCopy[leastElement]) {
 leastElement = j;
 }
 }
 // const temp = array[index];
 // array[index] = array[leastElement];
 // array[leastElement] = temp;
 // we can refactor the above code as shown below
 [shallowCopy[index], shallowCopy[leastElement]] = [shallowCopy[leastElement], shallowCopy[index]];}
 return shallowCopy;
 // change code above this line}toSort = [1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92];
console.log(selectionSort(toSort));
console.log(toSort); 
```

我们的函数现在表现得像一个纯函数。请查看下面的片段进行确认。
【1，1，2，2，4，8，32，43，43，55，63，92，123，123，234，345，5643】

## **最后的想法**

感谢您到目前为止阅读了这篇文章，我希望您发现这篇文章有助于解决这个挑战。

你有更好的解决方案或有任何疑问，我希望在评论区听到你的意见？

## **更多阅读:**

[](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [## 5 个 Chrome 扩展来加速你的开发

### 5 个有用的 Chrome 扩展，帮助开发者提高工作效率，完成更多工作。

javascript.plainenglish.io](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) [## Vue.js 您应该采用的最佳实践

### 使用 Vue.js 时的最佳实践

javascript.plainenglish.io](/vue-js-best-practices-you-should-adopt-3f3b3a8abace) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)