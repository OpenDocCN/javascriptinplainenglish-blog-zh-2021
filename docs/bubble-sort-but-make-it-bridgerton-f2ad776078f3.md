# 冒泡排序——但要让它成为布里奇顿

> 原文：<https://javascript.plainenglish.io/bubble-sort-but-make-it-bridgerton-f2ad776078f3?source=collection_archive---------7----------------------->

## JavaScript 算法演练

阿尔戈斯，阿尔戈斯，阿尔戈斯！有趣的东西！不，我不是在讽刺，我非常喜欢这种逻辑！不过，当我碰到二叉树和其他数据结构时，请随意@我，因为我可能会唱不同的调子。目前，我仍在研究更简单的算法，所以一切都很顺利！

![](img/c5b419f3a9fe816b887b94ef52c67edf.png)

yasss kween! yaaaas

与摄政时代的大多数伦敦上流社会不同，冒泡排序是最低效的算法之一。其低效的运行时间 O(n)只有 Daphne 和 Anthony Bridgerton 无法点燃一个炉子来加热他们的牛奶。你不希望 Bridgerton 兄弟出现在厨房里，就像你不希望对更大的数组使用冒泡排序一样(如果你最终要使用它的话)。就像有更适合厨房的人一样，也有更适合排序列表的算法。在我们进一步发展之前，必须先解决这个问题。

![](img/6a8d6872f34a55a94d0d953c595d4986.png)

#winning

冒泡排序的要点是比较数组中每对相邻的值。在遍历数组时，必须检查每一对数字。如果第一个值大于第二个值，那么你们交换位置。每次迭代后，最大值存放在最右边。

布里奇顿崩溃:如果我们有一系列的羽毛长筒大衣摆在女王面前，按照社会地位进行分类，而普鲁登斯意外地摔倒了，她的社会地位也直线下降(她现在是与她的姐妹们相比价值最低的羽毛长筒大衣)。

![](img/7ca2bbfad9d5031ce5fb4c5f1eb7202d.png)

a Featherington faux pas, indeed!

```
let Featheringtons = ["Philipa","Prudence","Penelope"]if (Philipa > Prudence), then we will swap their positions. 
```

当比较 Philipa 和 Prudence 的前两个值时，Prudence 的值较低，因此将与 Philipa 交换位置，Philipa 在问候女王时设法保持直立。这将是新的数组。

```
let Featheringtons = ["Prudence", "Philipa","Penelope"]
```

为了清楚起见，如果我们对一个数组进行升序排序，算法将从比较第一对值 Philipa 和 Prudence 开始。由于菲丽帕的地位比普律当丝高，他们将交换位置，而普律当丝现在在列表的最前面——我们想要最低的值。然后我们进入下一对，菲利帕和佩内洛普。它将对它们进行比较，并相应地对它们进行排序，如此等等，直到数组排序完毕。

布里奇顿迭代:[ **菲丽帕，普律当丝**，佩内洛普]→[普律当丝，**菲丽帕，佩内洛普**→[普律当丝，佩内洛普，菲丽帕]

数值迭代:[ **5，3 【T5，4】→[3**，5，4**→[3，4，5]**

既然我们已经了解了要点，那就让我们进入实质吧。

```
let array = [95, 31, 19, 7]

function bubbleSort(arr){
  let swap = (arr, a, b) => ([arr[a], arr[b]] = [arr[b], arr[a]])
  let swapped
  for(let i = arr.length; i > 0; i --){
    swapped = false
    for(let j = 0; j < i - 1; j++){
      if(arr[j] > arr[j+1]){
        swap(arr, j, j+1)
        swapped = true
      }
    }
    if(!swapped)break
  }
  return arr
}
```

1.  在编写冒泡排序函数时，我喜欢做的第一件事是立即定义一个“交换”函数来交换数组中的元素。交换函数接受 3 个参数:数组、索引 1 和索引 2。

```
let swap = (arr, a, b) => ([arr[a], arr[b]] = [arr[b], arr[a]])
```

它将采用 index1 和 index2 的原始顺序并交换它们，如上所示。

我选择将我的交换函数封装在我的冒泡排序函数中的一个变量中，但是你也可以编写一个单独的助手函数，在你的冒泡排序函数中调用，如果这样对你更有意义的话。

2.接下来，我创建一个*交换的*变量，以便以后在我的代码中使用。这将被设置为一个布尔值，以检查在完成内部循环后是否已经交换了数字。

3.现在我们开始我们的外环。这个循环将向后遍历数组**。我们从末尾开始，因为如前所述，数组[3](数组的最后一个索引)是我们的最大值 95 将在内部循环的第一次迭代结束时结束的位置。我们最初设定*将*换成假。(我们稍后会再讨论这个问题。)**

```
let array = [95, 31, 19, **7**]

function bubbleSort(arr){
  let swap = (arr, a, b) => ([arr[a], arr[b]] = [arr[b], arr[a]])
  let swapped
  **for(let i = arr.length; i > 0; i --){
    swapped = false
  }**
}
```

4.接下来是我们的内部循环，它从数组的开头开始迭代，意在使用条件语句比较每对值。如果 currentElement > nextElement，我们将调用方便的交换函数。请记住，普律当丝让女王做了一个不悦的鬼脸，她的值最低，所以她和她姐姐被交换到了阵的最前面。这也适用于此。由于交换已经被执行，我们现在更新我们的*交换的*变量为真。在下面的例子中，95 和 31 将在内部循环的第一次迭代后互换。

```
let array = [**95, 31**, 19, 7]

function bubbleSort(arr){
  let swap = (arr, a, b) => ([arr[a], arr[b]] = [arr[b], arr[a]])
  let swapped
  for(let i = arr.length; i > 0; i --){
    swapped = false
    **for(let j = 0; j < i - 1; j++){
      if(arr[j] > arr[j+1]){
        swap(arr, j, j+1)
        swapped = true
      }
    }**
  }
  return arr
}
```

5.在这里，如果数组已经按升序排序，我们会尽最大努力打破内部循环，为这个极其复杂的时间算法增加一些效率。通过使用 bang 运算符检查*是否交换了*，我们是说如果*没有交换*，就脱离这个内环。请记住，我们只交换 if current tele>next ele，所以如果这个条件从未得到满足，那是因为数组已经按升序排序了。因此，我们不再需要循环，可以脱离它。

```
let array = [95, 31, 19, 7]

function bubbleSort(arr){
  let swap = (arr, a, b) => ([arr[a], arr[b]] = [arr[b], arr[a]])
  let swapped
  for(let i = arr.length; i > 0; i --){
    swapped = false
    for(let j = 0; j < i - 1; j++){
      if(arr[j] > arr[j+1]){
        swap(arr, j, j+1)
        swapped = true
      }
    }
    **if(!swapped)break**
  }
  **return arr**
}
```

将数组返回到 for 循环的外部，以确保所有迭代都已完成，并且您已经完成了！

![](img/4ffba4f8dac716a4207bb96d1da46e51.png)

Splendid!