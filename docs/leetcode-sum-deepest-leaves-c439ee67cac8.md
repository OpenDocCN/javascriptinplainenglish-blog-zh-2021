# LeetCode:夏天最深的叶子

> 原文：<https://javascript.plainenglish.io/leetcode-sum-deepest-leaves-c439ee67cac8?source=collection_archive---------15----------------------->

## 使用层次顺序遍历的 JavaScript 解决方案

![](img/7414e31ecffd5d76dc03bf63c70e57c4.png)

成为算法大师的秘诀是什么？嗯，我不知道，我甚至还没有完成一个 LeetCode 难题。但是我会告诉你我在这方面做得更好的策略:**看到存在的每一个问题**。

好吧，那显然不可能。但是越看越好！此外，你并不真的需要看到每一个问题，而是每一种类型的问题。你听说过“没有原创的想法”这句话吗？显然，马克·吐温说过。我不得不谷歌一下。但这也是算法背后的想法。它们都使用其他算法中的某种概念。从太阳底下没有新东西的想法中得到安慰。一旦你解决了一个问题，你实际上可能已经解决了几个。

这是我最近解决的一个 Leetcode 算法。我以前从未见过这个问题，但我很快就解决了。只需要写一两行新代码。都是因为我之前见过类似的东西。

# 问题:最深的叶子和

这是一个 LeetCode 中难度的问题。给定二叉树的`root`，返回其最深叶子的值的总和*。例如，给定二叉树:`[1,2,3,4,5,null,6,7,null,null,null,null,8]`返回的是`15`*

```
 1
     / \
    2   3
   / \   \
  4   5   6
 /         \
7           8
```

下面显示了二叉树节点的定义:

```
function TreeNode(val, left, right) {
    this.val = (val===undefined ? 0 : val)
    this.left = (left===undefined ? null : left)
    this.right = (right===undefined ? null : right)
}
```

## 我的思考过程:

于是我开始思考我想怎么解决这个问题。我看着这棵树，意识到，如果这棵树可以按层次分解，我只对树的最底层感兴趣。

然后我的思绪立刻回到了我已经解决的过去的问题。我记得做过一道题，我必须按层次顺序打印出树的节点。这正是我所需要的。一种逐层遍历树的方法。然后，我可以计算最低层的总和，并返回该值。

所以我用我的解决方案来解决之前的问题，稍微调整一下，瞧！我不费吹灰之力就找到了解决方案。我在重复利用我已经完成的工作。重用子问题的解决方案。

这里有一个我写的关于二叉树层次顺序遍历的博客的链接

## BFS 算法:

1.  首先，让我们为 BFS 初始化我们的队列(根节点在里面),并初始化 **sum** 。
2.  在 while 循环中(一直运行到队列为空)，我们定义了一个 **for 循环**。for 循环将在最后一级末尾对队列中的每个元素运行。这意味着我们将增加“I ”,直到它达到队列长度。
3.  在 for 循环之前，一定要将每个级别的总和设置为零，以重新初始化总和。
4.  在 for 循环中，从队列顶部删除一个节点，并将其值添加到级别 sum 中。如果有孩子，将他们添加到队列中。
5.  一旦一个级别的所有节点都被访问过(for 循环的结尾)，我们就简单地移动到树的下一个级别(如果有的话)。继续步骤，直到队列为空。
6.  在函数结束时，只需返回 sum 值，因为这是在最低级别计算的。

## JavaScript 代码解决方案:

```
var deepestLeavesSum = function(root) { let queue = [root]
   let sum=0
   while (queue.length != 0){
      sum =0
      const n = queue.length

      for (let i = 0; i < n; i++){
         let curr = queue.pop()
         sum+=curr.val
         curr.left && queue.unshift(curr.left)
         curr.right && queue.unshift(curr.right)
      }
   }
   return sum};
```

当我在 LeetCode 上提交这段代码时，我得到了以下结果:

*   运行时间:112 毫秒，比 49.46%的 JavaScript 在线提交速度快
*   **内存** : 48.6 MB，不到 JavaScript 在线提交量的 54.50%

# 时空复杂性分析；

由于每个节点至少被访问一次，时间复杂度为 O(n)。空间复杂度也是 O(n ),因为在最坏的情况下，队列可以包含所有的叶节点。

# 参考资料:

[](https://leetcode.com/problems/deepest-leaves-sum/) [## 最深的叶子夏天- LeetCode

### 提高你的编码技能，迅速找到工作。这是扩展你的知识和做好准备的最好地方…

leetcode.com](https://leetcode.com/problems/deepest-leaves-sum/) [](https://medium.com/swlh/binary-tree-level-order-traversal-a12df61a85d0) [## 二叉树层次顺序遍历

### LeetCode 问题的 Javascript 解决方案

medium.com](https://medium.com/swlh/binary-tree-level-order-traversal-a12df61a85d0) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)