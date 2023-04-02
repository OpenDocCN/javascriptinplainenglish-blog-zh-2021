# CodeWars 社区面临的挑战

> 原文：<https://javascript.plainenglish.io/a-challenge-for-the-codewars-community-5c6945e92e1?source=collection_archive---------21----------------------->

## 人类的复杂性比算法的效率更重要

![](img/9f9b44b06927b7c9daf67a6fb24cf3bd.png)

Photo by [Shahadat Rahman](https://unsplash.com/@hishahadat?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/complexity?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 前言

我们大多数人都知道 Big-O 符号和算法效率的重要性。如果您已经处理了足够多的次优代码导致瓶颈的场景，那么您会对效率有更好的认识。成为一个更好的程序员是一个必不可少的经历，但是这种现象不应该对我们有太大的影响。

强调为机器编写代码并不总是最有效的。铁杆程序员可能会害怕这个想法，但我们应该首先考虑人类，其次才是机器，以建立一个可持续的平台。

感谢摩尔定律，增加物理资源永远比增加人力资源更便宜。这个行业已经发展到了这一点不仅被认可而且被强调的地步。

> 任何傻瓜都能写出计算机能理解的代码。优秀的程序员编写人类能够理解的代码。— [马丁·福勒](https://www.goodreads.com/quotes/6341736-any-fool-can-write-code-that-a-computer-can-understand#:~:text=%E2%80%9CAny%20fool%20can%20write%20code%20that%20a%20computer%20can%20understand,code%20that%20humans%20can%20understand.%E2%80%9D)

# 介绍

我发现自己处于一个令人兴奋的位置，30 岁在国外提前退休。提到这一点也很重要，在被驱逐回我的祖国南非之前，我有 3 个月的时间去寻找下一个机会。

凭借 10 多年的开发经验，我决定挑战自我，提升技能以满足市场需求。技术领域变化频繁，涉足自己不太熟悉的领域令人望而生畏。

这让我走上了信息超载的道路，因为每个机会都有其技术堆栈的味道，有些我很熟悉，有些我以前从未遇到过。尽管我相信我的经验使我更容易掌握其他技术，但我仍然发现潜入不熟悉的领域很有挑战性。

我发现自己的处境驱使我去了 [CodeWars](https://www.codewars.com/) 。

# CodeWars 概述

他们建立了一个奇妙的平台，在这里你可以用你选择的编程语言挑战你解决问题的技能。

> **通过挑战达到精通**——通过在真实代码挑战中与其他人一起训练来提高你的技能。
> 
> 来自[https://codewars.com](https://www.codewars.com/)的主页

一个可以用你喜欢的语言解决挑战的平台是一个伟大的创举！

# 挑战

社区的重点似乎是为每个挑战找到最有效的解决方案。我不反对这一点，因为所有的解决方案都应该考虑效率。然而，在实践中，这种方法有一些引人注目的问题。

想出一个需要更少计算复杂性的解决方案通常会导致更多的人工复杂性。显然，这取决于你的团队和信息共享的程度。以最近的挑战为例。

# 挑战示例—折叠阵列

在这个形中，你必须写一个方法，通过中间的 x 倍折叠一个给定的整数数组。

*一个例子说了一千多个字:*

```
Fold 1-times:
[1,2,3,4,5] -> [6,6,3]

A little visualisation (NOT for the algorithm but for the idea of folding):

 Step 1         Step 2        Step 3       Step 4       Step5
                     5/           5|         5\          
                    4/            4|          4\      
1 2 3 4 5      1 2 3/         1 2 3|       1 2 3\       6 6 3
----*----      ----*          ----*        ----*        ----*

Fold 2-times:
[1,2,3,4,5] -> [9,6]
```

如您所见，如果数字的计数是奇数，中间的数字将保持不变。否则，折叠点在中间的数字之间，所以所有的数字都会以某种方式相加。

该数组将始终包含数字，并且永远不会为空。参数 runs 将始终是一个大于 0 的正整数，表示您的方法要进行多少次折叠。

*   如果只有一个元素的数组被折叠，它将保持不变。
*   不应修改输入数组！
*   编码愉快，请不要忘记投票和排名这个形！:-)
*   我创造了其他的形。喜欢编码和挑战的可以看看。

来源:https://www.codewars.com/kata/57ea70aa5500adfe8a000110

## 基于“效率”的顶级解决方案

这个解决方案值得称赞。这位名叫 [Jan2107](https://www.codewars.com/users/Jan2107) 的开发者只用了 8 行代码就解决了这个难题。干得好，你值得表扬！毫无疑问，这是最有效的解决方案。

```
export function foldArray(array: number[], runs: number): number[] {
  const arr2 = [...array]
  while (runs > 0) {
    arr2.map(
      (val, i, arr) => 
        i + 1 === array.length ? 
          val : arr[i] = val + arr.pop()
    );
    runs--;
  }
  return arr2;
}
```

## 我的解决方案，基于“可读性”

令人尴尬的是，这是我的解决方案。肯定没那么有效率。然而，即使有了更好的解决方案，我还是会选择可读性更好的解决方案。

```
export function foldArray(array:number[], runs:number):number[] {
  const mid = Math.floor(array.length / 2)
  let folded: number[] = [] // Walk through half of the array to calculate the fold
  let currentIndex: number = 0
  for (currentIndex = 0; currentIndex < mid; currentIndex++) {
    folded.push(
      array[currentIndex] + 
      array[array.length - (currentIndex + 1)]
    )
  } // Append middle if odd
  if (array.length % 2 === 1) {
    folded.push(array[mid])
  } // Recurse if more runs needed (and possible)
  if (runs > 1 && array.length > 1) {
    folded = foldArray(folded, runs - 1)
  } return folded;}
```

这两种解决方案的结果是一样的，因为基本的逻辑几乎是一样的。当然，您可以通过降低计算复杂度来绕过一些 CPU 周期。但是对人类来说更符合逻辑吗？你能有足够的信心把它交给别人，让他们正确解读吗？

> 伟大的代码读起来像伟大的散文。当你第一次读它的时候，它是简洁的，有表现力的，清晰的。它试图尽可能地保持线性，引导读者经历艰难的转变，因为他们知道一个错误的举动可能会彻底失去他们。好的代码使用理解其受众的语言和词汇，它的目标是具有单一主要思想的功能，就像一篇有说服力的文章的段落。— [马修·比肖夫](https://medium.com/u/e730706421a2?source=post_page-----5c6945e92e1--------------------------------)

# 指导方针

在没有意识到的情况下，经验会教会你一些基本的准则。学习这些知识，成为更好的程序员。

## 为改变而设计

解决问题的时候，要时刻问自己:“规则变了怎么办？”。基于这一前提设计解决方案将使将来应用更改变得更加容易。

我曾在硬编码国家税值的平台上工作过，这不是一个有趣的挑战。

## 平衡可读性和效率

不清醒时编码。或者像你的团队喝醉了一样编码。我们都经历过陷入丑陋的代码，让你感觉像是在“给流浪汉洗澡”——[保罗·彼得森](https://medium.com/u/66db03bee129?source=post_page-----5c6945e92e1--------------------------------)。尝试从这些经验中学习，并致力于编写更干净的代码。

## 不要对代码行如此挑剔

如果罗伯特·弗罗斯特过于关注代码行，那么《未选择的道路》就不会如此受欢迎。他可以只写:“不要做绵羊，要独一无二。”

*旁注:诗歌可能不是编写漂亮代码的最佳比喻。代码应该是简洁的、可理解的和高效的(按照这个顺序)。*

相反，从诗歌中获取灵感，在一段逻辑上盖上你的印章，让下一个人的诗歌之旅更加愉快。简明扼要。可以理解。最后，要有效率。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)