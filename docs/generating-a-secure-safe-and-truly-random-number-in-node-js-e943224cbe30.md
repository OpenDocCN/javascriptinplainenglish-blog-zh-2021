# 在 Node.js 中生成加密安全的真正随机数

> 原文：<https://javascript.plainenglish.io/generating-a-secure-safe-and-truly-random-number-in-node-js-e943224cbe30?source=collection_archive---------6----------------------->

![](img/9a98b54ddf9d736ddf46b92c021e5acf.png)

Photo by [Riho Kroll](https://unsplash.com/@rihok?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*这篇文章有 Node.js 的例子，但适用于大多数编程语言。*

在寻找随机性时，您可能会找到的第一个函数是`*Math.random()*` ，它生成一个范围在[0，1) *(包括 0，但不包括 1)* 内的伪随机数。不幸的是，它不提供密码安全的随机数。因此，你不应该使用它，除非一旦你读了这篇文章，你决定这是一个可行的选择。

开始我们的旅程，我们可能遇到的第一件事是随机的类型:

*   真正随机的:没有模式或算法可以创造它们，因此它们是不可能预测的。关于这些是否存在存在争议。
*   **不可预测**:不是真正的随机，而是不可能预测。这通常是你正在寻找的安全选择。因为只要无法预测，它是如何产生的并不重要。
*   **不规则**:这是大多数人对随机的误解。这只是一些你无法在简单的视图中识别出模式的数据。这不是真正的随机，甚至是不可预测的。

不规则数据生成速度最快。当需要可再现的和统计上高质量的伪随机数时，应该使用它。例如在科学研究中，能够复制结果是很重要的。或者在运行测试时，某个种子值可能会导致 bug。

**但是，如果攻击者能够预测即将到来的值，那么就不应该使用不规则数据。**

不可预测的生成速度较慢，这可能是大多数解决方案所需要的。不可预测的数据由 *CSPRNG* 产生。

# RNG 的类型(随机数生成器)

*   **CSPRNG** : *密码安全伪随机数发生器。*是一个伪随机数发生器，它产生不可预测的值，使得**对所有用例**都是安全的。
*   **PRNG**伪随机数发生器。这是一个超类，包含了不规则值的生成器。
*   **RNG** : *随机数发生器*。包含 *PRNG* s 和*的超类是真正的随机*生成器吗？

因此你应该使用 CSPRNG 来产生各种代币、秘密、抽奖、彩票和种子。只有当你知道你在做什么的时候才使用剩下的。

# 偏见

Node.js 中最广为人知的 *CSPRNG* 是生成所需字节数的`*crypto.randomBytes*` 。因此我们才得到了一种生成安全随机数的方法。结局？号码

直接使用`*crypto.randomBytes*`会导致你的价值观产生偏差。这方面的一个例子是使用模运算符从生成的字节中获取一个较小的数字。

> 设 randomNumber = randomByte % 50

因为一个字节有 256 个不同的值，所以使用模运算符会增加选取较低值的机会。

上面的代码是一个错误生成随机数的完美例子，代表了这种常见的错误。在此示例中，您将生成以下范围:

这意味着在 6 和 49 之间的**数在此范围内有 **5 个对应值**，而在 0 和 5** 之间的**数有 **6 个对应值**。因此，虽然介于 6 和 49 之间的数字有 1.95%的几率被选中，但介于 0 和 5 之间的数字有 2.34%的几率被选中。**

这只是让你的随机值再次变得不安全的方法之一。

![](img/4c02da5b970a2dd5798ff791d997146b.png)

Photo by [Jon Tyson](https://unsplash.com/@jontyson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 铆钉铆合

那么，如何生成安全的随机数呢？也许你现在最好的选择是使用一个解决这个问题的库。在 Node.js 中，我们有:

*   用于在 : [随机数-csprng](https://www.npmjs.com/package/random-number-csprng) 范围内生成随机数
*   **对于 API 密钥或令牌来说，你最好的选择可能是 uuid，如果是这样，你可能会寻找 T2 函数。**

**但是考虑到你不应该在任何情况下修改结果，因为你可能会再次落入陷阱。**

**关于此主题的更多信息:**

*   **[Stephan t . lava vej 关于 C++中的 *rand()* 和生成随机数的精彩演讲。](https://www.youtube.com/watch?v=LDPMpc-ENqY)**

***更多内容请看*[***plain English . io***](http://plainenglish.io/)**