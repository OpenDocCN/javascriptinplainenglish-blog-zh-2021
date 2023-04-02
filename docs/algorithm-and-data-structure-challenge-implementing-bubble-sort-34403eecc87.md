# 算法和数据结构挑战—实现冒泡排序

> 原文：<https://javascript.plainenglish.io/algorithm-and-data-structure-challenge-implementing-bubble-sort-34403eecc87?source=collection_archive---------15----------------------->

## JavaScript 中的冒泡排序挑战 freeCodeCamp 的一个面试准备问题的解决方案。

![](img/c040a7201453f2e2eedba757ce371413.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

首先，让我们看看什么是算法。

> 根据[大英百科全书](https://www.britannica.com/science/algorithm)，算法是解决明确定义的计算问题的特定程序。

算法和数据结构使我们能够重新连接我们的思维和解决问题的技术。这更像是给我们的大脑做俯卧撑，以一种我们可以解决问题的方式来参与和思考。

算法和数据结构主要涉及处理一组给定的数据，并让它根据我们定义的或给定的算法做一些事情。

在这次挑战中，我们将解决 [freeCodeCamp](https://www.freecodecamp.org/learn/coding-interview-prep/algorithms/implement-bubble-sort) 关于面试准备的挑战。

## **挑战**

给定一个未排序的项目数组，我们希望能够返回一个排序后的数组。我们将看到几种不同的方法来做到这一点，并了解这些不同方法之间的一些权衡。虽然大多数现代语言都有类似这样的内置排序方法，但理解一些常见的基本方法并学习如何实现它们仍然很重要。

这里我们将看到冒泡排序。冒泡排序方法从一个未排序的数组的开头开始，并向末尾“冒泡”未排序的值，遍历数组，直到它被完全排序。它通过比较相邻的项目并在它们顺序不对时交换它们来做到这一点。该方法继续循环遍历数组，直到没有交换发生，此时数组被排序。

这种方法需要通过阵列进行多次迭代，并且对于平均和最坏的情况具有二次时间复杂度。虽然简单，但在大多数情况下通常是不切实际的。

## **指令**

编写一个函数 ***bubbleSort*** ，它将一个整数数组作为输入，并按照从最小到最大的排序顺序返回这些整数的数组。
***bubble sort***应该是函数。

*   ***bubbleSort*** 应该返回一个排序后的数组(从最小到最大)。
*   ***bubbleSort*** 应该返回一个除了顺序不变的数组。
*   ***bubbleSort*** 不要用内置的 ***。*排序()**方法。

## **解决方案**

```
function bubbleSort(array) {// Only change code below this linereturn array;// Only change code above this line}bubbleSort([1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]);
```

我们得到了一个数组，而解决方案想要的是我们重新排列给定的数组，使它从最小到最大开始。

例如，我们可以在数组中循环，比较数字，如果一个给定的数字较大，就跳到下一个，用一个较小的数字替换它的位置。

***方案一***

```
function bubbleSort(array) {for(let i=0;i<array.length -1 ;i++){for(let j=0;j<array.length -1 - i; j++){if(array[j]> array[j+1]){const bSort=array[j];array[j]=array[j+1];array[j+1]=bSort;}}}return array;}console.log(bubbleSort([1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92]));
```

在我们的控制台上，我们将对数组进行排序，如下所示。

```
[ 1, 1, 2, 2, 4, 8, 32, 43, 43, 55, 63, 92, 123, 123, 234, 345, 5643 ]
```

***要注意什么***

我们的解是不是纯函数？。一个纯函数不应该改变或变异所提供的参数。

我们的函数，如果我们登出数组的参数，我们会发现它改变了数组，这并没有使它表现得像一个纯粹的函数。

为了解决这个问题，我们可以对参数做一个简单的复制，它是如下所示的数组。

```
function bubbleSort(array) {const ShallowArray = array.slice();for(let i=0;i<ShallowArray.length -1 ;i++){for(let j=0;j<ShallowArray.length -1 - i; j++){if(ShallowArray[j]> ShallowArray[j+1]){const bSort=ShallowArray[j];ShallowArray[j]=ShallowArray[j+1];ShallowArray[j+1]=bSort;}}}return ShallowArray;}
```

***slice()*** 方法返回数组中选定的元素，作为一个新的数组对象。

现在如果我们 ***console.log*** 提供参数，我们会注意到我们的数组没有变异。

```
//our sorted array[ 1, 1, 2, 2, 4, 8, 32, 43, 43, 55, 63, 92, 123, 123, 234, 345, 5643 ]//our parameter array
[ 1, 4, 2, 8, 345, 123, 43, 32, 5643, 63, 123, 43, 2, 55, 1, 234, 92 ]
```

现在我们的函数表现得像一个纯函数。热爱函数式编程的人，会发现这个很有用。

这是每周系列算法和数据结构挑战的第一篇文章。看看下一个挑战。

如果你对这个挑战有更好的解决方案，请在评论区告诉我。

感谢您阅读本文到目前为止。如果你发现它有用，请不要犹豫分享。

## **更多阅读:**

[](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [## 5 个 Chrome 扩展来加速你的开发

### 5 个有用的 Chrome 扩展，帮助开发者提高工作效率，完成更多工作。

javascript.plainenglish.io](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) [## 作为一名开发人员，我在构建投资组合时学到了什么

### 你也可以从中学习。

javascript.plainenglish.io](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)