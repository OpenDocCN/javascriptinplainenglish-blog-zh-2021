# 如何构建单元测试

> 原文：<https://javascript.plainenglish.io/how-to-structure-a-unit-test-9c87f287d1de?source=collection_archive---------4----------------------->

## 编写单元测试的最佳实践

![](img/7f16597d8c2a421185519504494c5656.png)

[source](https://unsplash.com/photos/PP5nO5gcLdA?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)

## 我不喜欢写测试。

大部分开发人员也不喜欢，但是软件开发不是好恶的问题。它包括制造尽可能好的产品。这关系到很多东西——生意、金钱、名誉，在某些情况下，还有生命。

据[复地集团](https://fortegrp.com/the-importance-of-unit-testing/):

> 单元测试确保所有代码在部署之前都符合质量标准。这确保了质量至上的可靠工程环境。在产品开发生命周期的过程中，单元测试节省了时间和金钱，并帮助开发人员更高效地编写更好的代码。

不可否认，一些开发人员做出了努力，但是他们最终写出了无结构的、难以辨认的和不可理解的测试。

在本文中，我们将看看使用 **Arrange-Act-Assert** 模式构建单元测试的适当方式。

语言和框架:JavaScript 和 Jest。

***什么是 3A 模式关于* :**

3A 模式是一种常见的单元测试模式。它是一种安排和组织测试代码以使单元测试清晰易懂的方法，包括将每个单元测试功能分成三个部分:安排、动作和断言。

*   **Arrange:** 这是初始化对象和设置要传递给被测函数的数据值的地方。如果我们打算使用模拟，这也是设置模拟的最佳位置。
*   **Act:**Act 部分调用被测函数。
*   **断言:**这是验证被测函数的行为是否如预期的那样的地方。

***空谈是廉价。给我看代码:***

让我们创建一个简单的函数，它接受两个参数—一个数字和一个数组，并根据数组中是否存在该数字返回一个布尔值:

我相信代码简单明了。在第一次函数调用时，`5`存在于数组中，因此，`true`被返回。在第二次调用时，`5`在数组中不存在，于是，`false`被返回。

***测试***

请确保在运行测试命令之前从 npm 安装 Jest。

使用 *3A* 模式整齐地排列每个测试功能。在*排列*部分，我创建了我需要的变量并给它们赋值。在 *Act* 部分，我调用了`isNumberInArray`，并将返回值赋给`value`。在*断言*部分，我验证了`value`与我们分配给`expected`的值相同。当我们运行测试命令— *npm test* 时，我们的测试通过。

# 测试最佳实践

Vasya Drobushkov 就这个话题写了一篇优秀的文章，所以我只是想指出一些我在他的文章中找不到的最佳实践。

*   **避免多个 Arrange、Act 和 Assert 部分:**当一个测试函数包含多个由 Assert 分隔的 Act 部分，并且可能包含 Arrange 部分时，这样的测试就不能再称为单元测试了。

例如:

多个动作违背了单元测试的意图。重构包含多个动作和断言的测试。每一个动作都应该被提取出来进行测试。这样，您的测试将会快速、简单且易于理解。

*   **避免 if 语句:**一个单元测试应该简单易懂，但是当你使用`if`语句的时候，就表明你的测试一下子验证了很多东西。这样的测试应该分成几个测试。
*   **Act 部分不应该超过一行:**如果 Act 部分超过一行，这表明您的代码或您可能调用的公共 API 的设计有问题。Act 部分通常是单行代码。
*   避免不可读的测试:人们不应该浪费时间试图弄清楚你的测试是做什么的。这就是 3A 模式派上用场的地方。3A 模式使你的测试具有可读性和可理解性。
*   避免在测试中使用逻辑:在你的测试套件中使用逻辑会增加引入 bug 的机会，而你最不希望发现 bug 的地方就是你的测试套件。避免使用逻辑条件，如`for`、`if`、`while`和`switch`。
*   避免魔术串:单元测试不应该包含魔术串。命名变量可以让测试的读者将注意力集中在测试上，而不是实现细节上。

**推荐内容**

[](https://betterprogramming.pub/unit-testing-best-practices-9bceeafe6edf) [## 单元测试最佳实践

### 可以帮助您编写更好的测试的实用建议列表

better 编程. pub](https://betterprogramming.pub/unit-testing-best-practices-9bceeafe6edf) [](https://fortegrp.com/the-importance-of-unit-testing/) [## 更好的代码，更快:你应该使用单元测试的 8 个理由

### 一些开发人员低估了编写单元测试的重要性。以下是单元测试的五个好处…

fortegrp.com](https://fortegrp.com/the-importance-of-unit-testing/) 

`Chinedu Ikechi can be found on Twitter under the handle [@Chinedu__Ikechi](https://twitter.com/Chinedu__Ikechi).`