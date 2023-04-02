# ELI5:冒泡排序算法️🛁

> 原文：<https://javascript.plainenglish.io/eli5-bubble-sort-algorithms-%EF%B8%8F-78bbce018846?source=collection_archive---------14----------------------->

先说算法。今天，我将(像你 5 岁时一样)分解什么是冒泡排序算法，如何用 JavaScript 实现它，以及何时使用它。准备好了吗？我们走吧！

![](img/8d828ebc7b501e2f215ed81efc5c6a40.png)

Photo by [Drew Beamer](https://unsplash.com/@drew_beamer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 什么是冒泡排序算法？🛁

冒泡排序算法是对算法的完美介绍，因为它易于可视化。这不是最有效的算法。然而，这是你学习算法的第一步。

# 冒泡排序算法的特征📝

*   适合排序无序列表>>有序列表
*   轻松比较两个项目，并在必要时交换位置
*   使用循环的可靠算法

# 代码:实现冒泡排序⌨️

用 JavaScript 写的冒泡排序算法是什么样子的？下面我给你写出来:

```
function bubbleSortAlgo(arr) {
    let swap;
    let n = arr.length-1;
    let x = [...arr];
    do {
        swap = false;
        for (let i = 0; i < n; i++) {
            if (x[i] > x[i+1]) {
               let temp = x[i];
               x[i] = x[i+1];
               x[i+1] = temp;
               swap = true;
            }
        } n--;
    } while (swap);
 return x; 
}
```

哇，这个算法有很多进展。让我们来分解每一部分。

我做的第一件事是创建一些变量:

```
 let swap;
```

当**为真时，****交换**变量将指示我们的数组是未排序的。这将允许我们的 do/while 循环运行并执行它的排序魔术。

```
 let n = arr.length-1;
```

变量 **n** 代表数组的长度。你会看到，在我们完成循环的完整**后，我们将 n 减 1。我们这样做是因为在一次遍历数组后，末尾的项被排序。在以后的通行证中没有必要检查那个项目。因此，我们可以减少数组的长度，这也将减少下一次排序所需的时间。**

公平地说，节省的时间微乎其微，把这个加进去似乎有点傻。然而，我认为这是一个很好的实践，在未来的情况下，节省时间的措施是一个平稳运行的计划至关重要。

```
 let x = [...arr]
```

对于 **x** 变量，我选择使用[扩展语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax#spread_in_array_literals)创建一个全新的独立版本的 **arr** 参数。我这样做是为了确保原始数组(arr)保持不变。只有 **x** 将实现我们的冒泡排序算法的改变。

```
do {
        swap = false;
        for (let i = 0; i < n; i++) {
            if (x[i] > x[i+1]) {
               let temp = x[i];
               x[i] = x[i+1];
               x[i+1] = temp;
               swap = true;
            }
        } n--;
    } while (swap);
```

我们代码的主要部分是 **do/while** 循环。每次我们进入 do/while 循环时，我们都将 **swap** 变量设置为 false。当 swap 为 false 时，表示没有对我们的数组进行任何更改。这是个好消息，因为它表明到目前为止我们的数组已经排序了。

接下来，我们使用数组的当前长度 **n** 为循环创建一个**。在 for 循环中，我们检查相邻的项目对。如果项目已排序，我们什么也不做。如果它们没有被正确排序，我们就交换它们的位置，并将交换变量设置为 true。**

通过将我们的交换变量设置为 true，我们知道我们至少需要对数组再做一次检查。do/while 循环将再次运行，因为我们的交换变量为 true。

在最后一次遍历数组时，我们将永远不会进入 for 循环。因此，交换变量将保持设置为 false。然后，我们可以退出 do/while 循环。最后，我们可以返回数组 x。

让我们来看看实际情况。下面是一个使用伪代码的示例:

```
let myArray = [1, 4, 3];
bubbleSortAlgo(myArray);// FIRST PASS
set swap to false.
enter for loop.
compare 1 and 4, is 1 greater than 4? no! move to the next pair.
compare 4 and 3, is 4 greater than 3? yes! change places.
swap is set to true.
decrement n by 1.
we've reached the end of our array.
swap is true, continue do/while loop.the array currently looks like this: [1, 3, 4]// SECOND PASS
set swap to false.
enter for loop.
compare 1 and 3, is 1 greater than 3? no!
remember we decremented n? we've reached the end of our for loop.
no changes made, swap is still set to false.
exit do/while loop.
return x.
algorithm is complete!!!final array: [1, 3, 4]
```

![](img/a9be601a5d9442791a2e050ff96714d0.png)

Photo by [Deleece Cook](https://unsplash.com/@deleece?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我们什么时候使用冒泡排序？🧐

冒泡排序是对数据列表(也称为数组)进行排序的最佳选择。尤其是在学习算法和工作面试的时候。实际上，它在工作代码中并不是不太受欢迎的，因为它是低效的。还有更快、更智能的排序算法(下一节将详细介绍)。

当您需要比较相邻的项目，并在必要时交换它们的位置时，此算法非常有用。

# 结论💭

冒泡排序算法是比较大量数据并根据您定义的条件对它们进行排序的绝佳方式。正如我在介绍中提到的，它更多的是一种教育工具，因为有更有效的排序算法(quicksort、timsort、merge sort)。

您可以在这里了解更多关于线性搜索数据结构[的信息，以及它在大 O 符号中的时间复杂度。](https://en.wikipedia.org/wiki/Bubble_sort)

# ELI5 算法系列📚

*   [ELI5:冒泡排序算法🛁](https://haleepagel.medium.com/eli5-bubble-sort-algorithms-%EF%B8%8F-78bbce018846)
*   [ELI5:线性搜索算法🕵️‍♀️](https://haleepagel.medium.com/eli5-linear-search-algorithms-%EF%B8%8F-%EF%B8%8F-6f79cf9b3bb7)
*   [ELI5:二分搜索法树🌲](https://haleepagel.medium.com/eli5-binary-search-trees-fd560f81b553)

感谢阅读！我叫 Halee Pagel(与 Cali Bagel 押韵)，是日本东京的一名软件工程师。你可以在推特上找到我，我主要用它来喜欢科技迷因和 MLB 的更新。✌️