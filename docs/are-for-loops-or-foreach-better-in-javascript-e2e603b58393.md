# JavaScript 中 For 循环和 ForEach 哪个更好？

> 原文：<https://javascript.plainenglish.io/are-for-loops-or-foreach-better-in-javascript-e2e603b58393?source=collection_archive---------8----------------------->

![](img/a70279e67f71291963bc3e269267a30f.png)

Photo by [Mathew Schwartz](https://unsplash.com/@cadop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 你应该选择哪一个，为什么

当我审查一个代码时，我看到人们在他们的代码中不断混合**代表**和**代表**。要么是搞混了，要么是分不清 for 和 forEach。根据经验法则，除了少数情况，您应该始终使用 forEach。在这篇文章中，我将解释什么时候你应该做出那些例外。这对`**Array.map**`也有效。

## 基本语法

在继续之前，让我们快速浏览一下这两种语法。

**为循环:**

```
for ([initialExpression]; [conditionExpression];[incrementExpression]) {
  statement|s
}const array = [1, 2, 3, 4, 5];
for (let index = 0; index < array.length; index++) {
  console.log(array[index]);
}
```

**ForEach 循环:**

```
arr.forEach(callback(currentValue[, index[, array]]) {
  // execute something
}[, thisArg]);const array = [1, 2, 3, 4, 5];
array.forEach((item) => {
  console.log(item);
});
```

在上面的示例中，两个代码都将打印数字的对数序列。ForEach 采用功能方法来解决问题。ForEach 接受一个函数回调，并对数组中的每个值执行。 **forEach** 方法看起来比 **For 循环**更简洁。但是有些情况下我们需要 for 循环，或者我们可以说 for 循环比 forEach 好。我们来探索一下。

**1。循环到一个值范围:**假设你必须循环一些特定次数的代码(假设 100)。这里不能用 forEach。因为对于 ForEach，你需要一个数据数组。可以使用**数组(100)。fill(0)到**创建一个用 0 填充的数据数组。但这是一个额外的头痛。

```
// Sum of the first 99 natural numberslet sum = 0;
for (let index = 0; index < 100; index++) {
  sum += index;
}
```

使用 forEach 的相同代码

```
let sum = 0;
Array(100)
  .fill(0)
  .forEach((_, index) => {
    sum += index;
  });
console.log(sum); // 4950
```

这里代码的复杂度很高( **O(2n)** )。因为我们循环了两次。一个用来填充数组，另一个用来迭代数组以收集自然数。

**2。除了 1 之外的增量索引:**这是另一个很好的例子，此时应该使用 for 循环而不是 forEach。这将降低代码的复杂性。

例如，假设您有一个数据数组，您必须执行收集数据对。

```
let numbers = [0, 1, 2, 3, 4, 5, 6, 7];
let pairs = [];
for (let index = 0; index < numbers.length; index += 2) {
  pairs.push([numbers[index], numbers[index + 1]]);
}console.log(pairs); // [ [ 0, 1 ], [ 2, 3 ], [ 4, 5 ], [ 6, 7 ] ]
```

请注意，我们可以跳过(递增)任何数量的索引。如果你必须使用 forEach 循环做同样的事情，你必须有一些逻辑每次跳过第二个数字。

```
let numbers = [0, 1, 2, 3, 4, 5, 6, 7];
let pairs = [];numbers.forEach((item, index) => {
  if (index % 2 === 0) {
    pairs.push([item, numbers[index + 1]]);
  }
});
console.log(pairs); // [ [ 0, 1 ], [ 2, 3 ], [ 4, 5 ], [ 6, 7 ] ]
```

![](img/9144ff22dc5f724b7f5e4aa7515f7570.png)

**3。条件中断/继续循环:**由于某种原因如果你的代码要求条件中断循环。For 循环比 forEach 更好使用。这是因为打破 forEach 循环是痛苦的。我写了一整篇文章来解释如何打破循环。

```
let numbers = [0, 1, 2, 3, 4, 5, 6, 7];for (let index = 0; index < numbers.length; index++) {
  if (numbers[index] > 5) {
    break;
  }
  console.log(numbers[index]); // 0, 1, 2, 3, 4, 5
}
```

类似的代码如果你必须使用 forEach 来写，你必须抛出一个错误并捕捉它。

```
let numbers = [0, 1, 2, 3, 4, 5, 6, 7];const printValueTill5 = (v) => {
  if (v % 5 == 0) {
    **throw new Error("index is greater than 5");**
  }
  console.log(v);
};
try {
  numbers.forEach(printValueTill5);
} catch {}
```

**4。在块中工作，分割数组:**另一个好的用例可能是当你必须在数据块中工作时。所以你可以从第一次迭代剩下的地方开始索引。

例如，假设您必须合并两个数组，并且您不确定这两个数组的大小。

```
const array1 = [1, 3, 5, 7, 8, 9, 10];
const array2 = [2, 4, 6];
const merged = [];let index = 0;
for (; index < array1.length && index < array2.length; index++) {
  merged.push(array1[index]);
  merged.push(array2[index]);
}// loop over array1, if left any
for (; index < array1.length; index++) {
  merged.push(array1[index]);
}// loop over array2, if left any
for (; index < array2.length; index++) {
  merged.push(array2[index]);
}console.log(merged); // [1,2,3,4,5,6,7,8,9,10]
```

我甚至想不出用 forEach 写同样的代码。

**5。使用嵌套循环:**forEach 循环的另一个挑战是使用嵌套循环。嵌套 forEach 会导致非常难看的循环。同时也很容易导致回调地狱。

例如，填充 2D/3D 阵列。

```
let matrix = [];for (let i = 0; i < 3; i++) {
  matrix[i] = [];
  for (let j = 0; j < 3; j++) {
    matrix[i][j] = [i, j];
  }
}
console.log(matrix);/*
[
  [ [ 0, 0 ], [ 0, 1 ], [ 0, 2 ] ],
  [ [ 1, 0 ], [ 1, 1 ], [ 1, 2 ] ],
  [ [ 2, 0 ], [ 2, 1 ], [ 2, 2 ] ]
]
*/
```

## 结论

也许使用 raw for 循环很棘手，容易出错。但是 for 循环有它自己的位置。它让您完全控制**数据**、**指标**和**条件**流程。同时基于上面的例子，我们可以假设每当你的工作需要更多的与索引/条件表达式的交互时。可以使用 for-loop。对于其余情况，使用 **forEach** 进行数据优先使用。

谢谢欣赏我的努力。它鼓励我比以前写得更多更好。

我知道这很艰难，但我还是会为你加油