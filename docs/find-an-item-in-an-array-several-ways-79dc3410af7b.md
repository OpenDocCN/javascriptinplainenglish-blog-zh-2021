# 在 JavaScript 中查找数组中项目的几种方法

> 原文：<https://javascript.plainenglish.io/find-an-item-in-an-array-several-ways-79dc3410af7b?source=collection_archive---------13----------------------->

![](img/4e85dbd31be1627fb75edea8623544ad.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们在编码时执行的一个非常常见的操作是试图确定数组中是否存在一个元素或项目。

这可能很简单，比如确定数字 5 是否存在于整数数组中，或者试图找出字符串`"Hello"`是否存在于字符串数组中。稍微复杂一点的是确定一个对象是否在一个数组中，这通常以一种简单的方式来完成，通过一些唯一的键来标识每个对象。

在搜索数组时，并不是所有的技术都是一样的。在这种特殊的情况下，数组的顺序会影响我们找到一个项目的速度。

# 在未排序的数组中查找项目

如果我们需要在一个未排序的数组中找到一个项目，实际上没有太多其他选择，我们必须查看每一个项目。没有不看每一件物品就能知道的神奇方法。在 Javascript 中，我们可以通过许多不同的方式来实现这一点。下面是一些不同的实现。

你可以看到实际上有很多方法，还有其他的方法可以推导出来，这里没有画出来。这些是在数组中查找项目的最常见的方法。总的来说，所有这些都导致了线性的运行时复杂度(O(N))，除非我们有一个有序的数组，否则没有真正的改善。这种情况我们接下来会去拜访。

# 对排序后的数组执行搜索

在未排序的数组上执行搜索会导致线性运行时复杂性。这其实已经很不错了，但是我们必须经常问自己，我们还能做得更好吗？

在我们已经排序数据的情况下，答案是肯定的。一旦我们知道数据已经排序，我们实际上可以开始消除一些结果。还记得我之前说过，如果不查看所有项，我们不可能知道一个项是否在数组中吗？当我们有一个排序的数组时，这不再适用，因为我们能够进行一些消去。

我所描述的特定类型的搜索是二分搜索法。它使用递归来工作，对于每个函数调用，它获取数组中的中间元素，并检查它是否是有问题的元素。如果是的话，你的工作就完成了。如果不是，您现在可以将您正在寻找的元素与您当前正在查看的元素进行比较。根据它是更小还是更大，您可以对数组中必须包含该值的另一部分进行递归，从而有效地消除其他结果的一半。请参见下面的实现。

让我们先忽略基本情况。我们做的第一件事是找到中间项的索引。我们通过简单地将长度除以 2，然后对结果进行地板处理，使得没有任何小数。然后，我们检查这是否是我们正在寻找的项目。

在这个例子中，为了简单起见，我们使用数字。如果它是项目，我们返回它，我们知道它包含在数组中。如果不是这个项目，我们需要决定如何进行最好。因为我们正在处理排序的数据，我们需要做一些比较来决定我们应该在中间元素的哪一边递归。有了数字就简单了，我们可以做一个数字比较来确定这一点。当处理字符串或对象时，您需要更多地考虑这种比较，比如增量 id，或者根据用户对象的名字排序，无论您的应用程序需要什么。

现在，为了简单起见，我们可以坚持使用数字，因为在这一点上更多的是学习概念。如果基于数字比较，要查找的数字大于中间的元素，那么我们知道它必须在当前元素之后的索引位置。如果它比中间的元素小，我们知道它一定包含在比中间的元素低的索引位置。

这样，我们调用相同的函数，这次传入截断的数组。注意截断是用 Array.Slice 完成的。我更喜欢这种技术，因为它不会改变原始引用。这种情况会一次又一次地发生，直到我们找到我们要找的项，或者我们最终用一个空数组调用函数。

这就把我们带到了基本情况。随着我们不断地拆分，我们只剩下数组中的一项。如果这不是项，那么我们用一个空数组再次调用函数，我们的基本情况被命中，我们返回 null，表明在数组中没有找到该项。这比我们以前的解决方案优化了很多，因为我们最终只看到以前一半的数据。这使我们的解决方案达到了对数运行时间复杂度或 O(logN)。

# 我们能做得更好吗？

到目前为止，我们已经看到了几种在未排序的数组中快速查找项目的方法。我们注意到这些可以在 O(N)运行时复杂度下运行，这很好。我们探索了当我们的数据被排序时，我们如何能够做得更好，并使我们的运行时间复杂度降低到 O(logN)。但是分类数据是有成本的。

我们可以确保当项目被插入到数组中时，它们被插入以保持排序。在这种情况下，插入将花费 O(N)时间(在某些情况下可以通过使用 O(logN)的特定数据结构进行优化)，但是因为条目保持它们的排序，所以我们可以使用二分搜索法在 O(logN)中进行搜索。

如果我们需要对此进行改进呢？在这种情况下，这不是关于一些花哨的算法，而是一种不同的思维过程。想象一下，我们可以通过某种对索引位置的引用来确定一个项是否在数组中？

这是很多代码，其中很大一部分是示例，所以让我们深入研究一下。

首先，我想承认这个解决方案不是 100%真正的常数时间，为了实现真正的常数时间，我们需要完全放弃数组，而使用链表。这将允许我们不存储索引位置，而是在内存中存储节点的引用。这是最佳解决方案，也是实现 LRU 缓存的基础。

在这种特殊情况下，由于我们的其他解决方案是专门针对阵列设计的，所以我想尝试一种类似的解决方案，直接处理阵列。

深入到类中，一般的想法是，每次用户调用`insert`时，我们都将项目添加到数组的末尾(而不是开头，因为这会有潜在的性能差异)，并将索引位置存储在一个对象中。通过这样做，我们现在可以访问`has`方法，该方法在恒定时间内执行。它只是在对象中查找，以确定数组中是否存在该值。所以现在我们有了一个持续的方法来查看数组中是否存在条目。

我们应该检查我们需要为拥有这个恒定时间付出的代价。争论的主要问题是关于驱逐。如果我们只是一直做插入，那么这是非常快速和伟大的。但是当我们开始移除时，我们看到了第一个问题。如果我从数组中移除一个条目，就需要进行一些重新索引。这对我们来说没什么大不了的，因为重新索引意味着我们的参考地图不再正确。

为了纠正这一点，我们需要执行 O(N)运算。我们可以通过对数据执行循环并将所有新的索引位置存储到参考图中来减少图中的坏索引。这种重新索引导致我们不断的时间查找，以 O(N)移除为代价。也许这是为我们的应用程序支付的合理价格。

# 我们可以通过垃圾收集来改善这种情况吗？

我们还没有在课堂上讨论这个垃圾收集方法。其目的是试图通过清除来缓解这一问题。我们只需简单地将索引处的数据设置为未定义，并将其从参考图中移除，而不是拼接或移除整个索引，从而导致 O(N) work 重新索引。

现在，没有进行重新索引，我们在映射中的索引已经准备好了，我们可以继续不断地插入、删除和不断地检查数组中是否有该项。听起来真不错！

但是我们有一个问题。本质上，通过添加和删除项目，我们总是使我们的地图更大，我们的阵列更大。随着时间的推移，这可能会导致严重的内存问题。这就是垃圾收集背后的想法。你只需支付 O(N)价格，但只是在某个确定的阈值。这里我用 10，因为我不想有一些大的例子，但这个数字会高得多，基于现代的内存限制。

在这种情况下，只有当数组中存在 X 个空点时，才需要重新索引。这是一个很好的折中方案，可以保持良好的运行时复杂性，但要意识到该解决方案涉及到一些内存约束。

# 结论

总的来说，有很多方法可以找到数组中的元素。大多数时候，JavaScript 提供的内置方法将满足我们的需求。但是，当我们寻找最优解时，探索尝试优化在数组中查找项目的不同方法是很有趣的。

在数组中实现一个完整的类来获得常量时间查找值得吗？是的，如果形势需要的话。在大多数情况下，只需遍历数组就可以很好地伸缩，这种更复杂的实现是不必要的。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)