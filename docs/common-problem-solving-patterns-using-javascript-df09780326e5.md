# 使用 JavaScript 的常见问题解决模式

> 原文：<https://javascript.plainenglish.io/common-problem-solving-patterns-using-javascript-df09780326e5?source=collection_archive---------5----------------------->

![](img/aae5d6a1960e7fb070e2905f5312d975.png)

我正在自学数据结构和算法，目前正在学习柯尔特·斯蒂尔在 Udemy 上发布的课程。作为一名训练营的毕业生，我没有传统的算法课程，也没有计算机科学中数据结构的理论和应用。到目前为止，这是一个令人大开眼界的课程，我正以缓慢但稳定的速度前进。Colt 一贯警告学生，材料有时可能很密集，不要匆忙通过课程，但他设法将材料分解成易于理解的概念，并展示了真正深入流行算法和数据结构的一步一步的实现。

我发现将这门课程与 Codewars、HackerRank 和 LeetCode 等编码挑战网站结合使用确实有助于我的理解。我的学习风格包括亲自动手和尝试挑战，因此实现一个数据结构或在代码挑战中使用一个数据结构对我的学习经验非常有帮助。

下面，我将介绍 3 种解决问题的模式，我发现它们在尝试编码挑战时经常出现。

1.  计数式频率计
2.  多个指针
3.  推拉窗

# 计数式频率计

一个示例编码挑战如下:“给定两个字符串，确定每个字符串是否是另一个的变位词。变位词是通过重新排列不同单词或短语的字母而形成的单词或短语。

不使用任何数据结构，使用上面的例子。我们将采用的方法是使用一个对象来跟踪输入字符串中每个字母的出现。

*在后面的章节中，您将了解到我们存储各种键:值对的“对象”被称为哈希表。它们会增加复杂性，因为键:值对可以包含所有数据类型和其他数据结构。*

```
function validAnagram(str1, str2){
   if (str1.length != str2.length ) { return false } const FC1 = {}
   const FC2 = {} for ( let val of str1){
      FC1[val] = ( FC1[val] || 0 ) + 1
   } for ( let val of str2){
      FC2[val] = ( FC2[val] || 0 ) + 1
   }
   for ( let key in FC1 ) {
      if ( !(key in FC2)) { return false }
      if ( FC2[key] !== FC1[key] ) { return false }
   }
   return true;
}
```

有多种方法可以解决这种类型的问题，但是如果我们用 BigO 符号来描述这种解决方案，我们可以将时间复杂度描述为 O(3n ),从而简化为 O(n)和

# 多个指针

对于这个编码挑战，实现一个接受排序数组并返回数组中唯一值的整数的函数。

一个有多个指针的问题通常表示遍历一个数组，一个指针可以从开始、中间、结尾或者你逻辑上指定的任何地方开始。像上面的问题一样，将指针错开，以便将一个元素与下一个元素进行比较是很常见的。一个元素是“读”元素，另一个是“写”元素，使用这种方法，您还可以就地编辑数组。

```
function countUniqueValues(array){
   let p1 = 0
   let p2 = 1 if ( array.length === 0) { return 0} for (let i = 0; i < array.length; i++ ) {
      if (array[p1]===array[p2]) {
         p2++}
      if ( array[p1] !== array[p2]) {
         p1++;
         array[p1] = array[p2];
      }
   }
   return p1
}
```

这种方法防止了嵌套循环，并允许 O(n)运行时，而不是嵌套循环导致的 O(n)运行时。上述解决方案也具有 O(1)的空间复杂度，因为该算法仅利用了 2 个指针变量。

*请注意，使用指针时，常见问题不再需要 2 或 3 个指针，您可能需要重新考虑您的方法。此外，这种方法通常需要一个排序的数组才能工作。*

# 推拉窗

我发现这种模式是最不直观的，并且发现使用这种模式的问题不像上面的 2 个那样普遍。然而，在分解更复杂的问题时，保留这种模式是有用的。

窗口可以被认为是需要跟踪的数据、数组或字符串的子集。可以通过改变我们希望查看的索引或位置来增大或减小窗口。以下示例涉及在给定未排序数组和子数组大小的情况下最大化子数组。

创建一个接受未排序整数数组和一个整数的函数。返回子数组中与输入整数相等的连续元素的最大值。

```
function maxSubarraySum(array, num){

   if (array.length < num) { return null}

   let maxSum = 0
   let tempSum = 0 for ( let i=0; i < num; i++) {
      tempSum+=array[i]
   } maxSum = tempSum for ( let j=num; j < array.length; j++ ){
      tempSum = tempSum - array[j-num] + array[j]
      if (tempSum > maxSum) { maxSum = tempSum }
   }

  return maxSum
}
```

如果您研究上面的解决方案，基本设置是第一个循环启动窗口，而第二个循环将窗口“滑动”到输入数组中。这个问题的简单解决方案通常涉及嵌套循环来测试元素的每个组合，但是像上面这样的简单设计允许一次 O(n)和恒定的空间复杂度 O(1 ),因为我们只使用了 2 个额外的变量。

有许多问题模式，但这是我在柯尔特·斯蒂尔的课程中第一次接触到的三种。当学习像数据结构和算法这样的材料时，我再怎么强调学习一门课程的重要性也不为过。到目前为止，我非常享受这个过程，并计划继续我的学业，并就我遇到的话题写博客。

*更多内容尽在*[plain English . io](http://plainenglish.io/)