# JavaScript 迷你代码挑战

> 原文：<https://javascript.plainenglish.io/mini-code-challenge-fb9da97bf9b8?source=collection_archive---------14----------------------->

## 一个小的 JavaScript 难题演练。

![](img/ea7de010d5e7b268f2e468280178fc25.png)

Photo by [Amit Jain](https://unsplash.com/@amitjain0106?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

不久前我遇到了这个迷你代码挑战。科技公司有时会在允许程序员面试之前，用这种问题来测试他们的能力。

这个特殊的挑战是在 JavaScript 中，但是如果你喜欢数学，你会做得很好！

这是个难题:

The original challenge.

去吧，试着自己解决。

你有答案吗？

太好了！让我们一步一步地看下面，看看我们是否达成了相同的解决方案。

# 我们从哪里开始？

让我们分解前几个声明，以及变量是如何初始化的。

在这个程序中发生的第一件事是我们初始化`x`和`y`。还要注意，我们用`let`声明这些变量；这意味着我们可以在程序的后面重新定义它们的值。

```
let x = 2;
let y = 8;
```

然后我们初始化`a`。该变量使用`const`声明；这实际上是一个*常量*，我们以后不能改变它。它被认为是只读的。

```
const a = function(b) {
  return function(c) {
    return x + y + Math.abs(b) + c;
  };
};
```

现在我们已经定义了这些，我们跳过稍后能够编辑的那一行(在`// ***** Statement will go here *****`)。

然后，我们的程序将使用我们对`a`和`x`的定义来初始化`fn`。

```
const fn = a(x);
```

让我们用一些替换来看看`fn`到底会是什么。

*如果你不熟悉 JavaScript，使用* `*//*` *注释掉这一行，这样它就不会在代码中运行。我在一些代码片段中使用它来提醒我们自己，当我们勾画出解决方案的路径时，我们从哪里开始。*

```
// const x = 2
// const a = function(b) {
//   return function(c) {
//     return x + y + Math.abs(b) + c;
//   };
// };
// const fn = a(x)const fn = function(2) {
  return function(c) {
    return x + y + Math.abs(2) + c;
  };
};
```

`Math.abs(2)`的值就是`2`，我们就用那个吧。

```
const fn = function(2) {
  return function(c) {
    return x + y + 2 + c;    <-- Change Math.abs(2) to just 2
  };
};
```

最终，该函数将返回另一个返回最终计算结果的函数。我们来简化一下。

```
const fn = function(c) {
  return x + y + 2 + c;
};
```

# 现在我们有进展了！

这是我们的整个计划，这一次是对`fn`的分解。

现在我们已经使用替换进行了简化，让我们更仔细地看看我们打印的数字输出。

```
console.log(fn(Math.random() * 10);
```

当这一行代码像这样堆叠在一起时，有点难以理解。为了更容易理解，让我们把它分解成一些变量。

```
const input = Math.random() * 10;console.log(fn(input));       <-- pull out "Math.random() * 10"
```

让我们把这个功能也拿出来:

```
const input = Math.random() * 10;const printedNumber = fn(input);console.log(printedNumber);    <-- pull out fn(input)
```

还记得我们更新的`fn`的定义吗？又来了:

```
const fn = function(c) {
  return x + y + 2 + c;
};
```

函数`fn`将返回计算结果`x + y + 2 + c`，其中`c`是传递给函数的任何内容。在我们的例子中，`c`将是`input`。

让我们用一些替换来看看`fn`将会出现在我们的`printedNumber`中:

```
// const printedNumber = fn(input);
const printedNumber = x + y + 2 + input;
```

我们已经定义了我们的`input`。记得吗？

```
const input = Math.random() * 10;
```

我们可以再次替代！

```
// const printedNumber = x + y + 2 + input;const printedNumber = x + y + 2 + Math.random() * 10;
```

唷！干得好。这是我们现在所处的位置，有几件事情定义得更清楚了。

# **看 x 的时间到了**

还记得我们宣布`x`的时候吗？程序使用了`let`，这意味着我们可以改变这个值。

在我们可以编辑的行之后，再次定义`x`的值*。这意味着我们知道它的价值不会改变。*

我们可以再次简化！

```
// x = 4;
// const printedNumber = x + y + 2 + Math.random() * 10const printedNumber = 4 + y + 2 + Math.random() * 10
```

我们知道`4 + 2 = 6`，所以我们将简单的整数相加。

```
const printedNumber = y + 6 + Math.random() * 10
```

# 现在我们有可以利用的东西了！

我们的目标是什么？

> 使打印的数字始终在 **10** 和 **20** 之间

…我们知道…

```
printedNumber = y + 6 + Math.random() * 10;
```

所以让我们把它看作一个范围:

```
10 < ( printedNumber ) < 20
```

鉴于我们对`printedNumber`的定义，我们可以再次代入:

```
10 < ( y + 6 + Math.random()*10 ) < 20
```

让我们把这个范围分成两个界限:

```
// Minimum Boundary Edge
10 = y + 6 + Math.random() * 10// Maximum Boundary Edge
20 = y + 6 + Math.random() * 10
```

# **Math.random()**

如果我们查找`Math.random()`的定义，当我们求解新的边界方程时，我们可以决定如何处理它。

> [Math.random()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/random) 函数返回一个浮点伪随机数，范围为 0 到小于 1(包括 0，但不包括 1)

我们可以将值`0`和`1`视为`Math.random()`的`minimum`和`maximum`值。为了更好地理解，我们将把这些代入我们的方程。

## **最小边界边缘**

对于最小边界边缘，我们将替换为`Math.random() = 0`。

```
10 < y + 6 + Math.random() * 1010 = y + 6 + 0 * 10        <-- Substitute 0 for Math.random()10 = y + 6                 <-- 6 + 0 is 64 = y                      <-- Move 6 to the other side (10 - 6)
```

## 最大边界边缘

对于最大边界边缘，我们将替换为`Math.random() = 1`。

```
20 > y + 6 + Math.random() * 1020 = y + 6 + 1 * 10        <-- Substitute 0 for Math.random()20 = y + 16                <-- 6 + 10 is 164 = y                      <-- Move 16 to the other side (20 - 16)
```

在我们的代码中设置了`y = 4`后，我们打印的数字将始终在`10`和`20`之间。

# **解决方案？y = 4**

尽管如此，我们可以将单行语句放在原始代码中。

# 等等…我们怎么知道改变 y 而不是 x？

在我们有机会添加一行代码后，程序本身也发生了变化。然而，我们也可以考虑编辑`x`，这将改变`fn`初始化中`b`的值。

你可以用我们上面学到的东西，通过反复试验来确定`x`不是一个可以改变的值。

我们可以有把握地决定，如果`y = 8`不改变，我们的印刷数字有可能不会落在我们的 10 到 20 范围内。

# 结论

你怎么想呢?我们能可靠地说`y = 4`为我们的最终解决方案吗？

如果我们回头看看我们对`Math.random()`的定义，我们可能会记得它产生的值是*包括 0。这意味着我们的随机数*可能*实际上等于零。*

我们没有找到让我们留在这里的价值:

```
10 < printedNumber < 20
```

…我们最后会有这样的结局吗？

```
10 <= printedNumber < 20
```

你怎么想呢?获得面试的正确答案是`y = 4;`吗？

*更多内容请看*[*plain English . io*](http://plainenglish.io/)