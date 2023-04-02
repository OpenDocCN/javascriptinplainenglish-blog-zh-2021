# 如何处理柏树中的选择器

> 原文：<https://javascript.plainenglish.io/dealing-with-selectors-in-cypress-8b9ac0dfe240?source=collection_archive---------1----------------------->

![](img/bb5c6c6385b6d62011efc33b8e612bed.png)

Photo by [Aleksey Boev](https://unsplash.com/@alanveob?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

自从我开始使用柏树已经有一段时间了，我没有发现太多关于使用选择器的信息。

柏树文档没有超出[建议](https://docs.cypress.io/guides/references/best-practices.html#Selecting-Elements)使用“稳定的”属性选择器而不是脆弱的 CSS 选择器，也没有提出组织和重用选择器的方法。

本文的目的是填补这一空白，并发现到目前为止有哪些可用的方案。

**0。使用硬编码选择器**

使用选择器最简单的方法是在所有地方对它们进行硬编码。

不用说，这不是处理选择器的最佳方式，因为:

*   您不能重用硬编码在测试代码中的选择器
*   如果选择器中断，您需要更新测试代码中该选择器的所有出现
*   选择器可能不表示它确切定位了哪个元素(例如`div > .item`不提供关于它所查询的元素的目的的任何线索)

鉴于这种方法的所有缺点，我会说这是使用选择器的最不可取的方式。

**1。将选择器存储在常数中**

接近 **#0** 的明显改进是将选择器存储在常量中，然后通过引用来使用它们——这是重用选择器的最简单方法:

我们甚至可以将这些选择器添加到某个对象(命名空间？)来强调这些选择器是密切相关的，然后通过访问我们的特定页面/小部件的选择器的“名称空间”来使用它们:

**优势:**

*   这样的选择器可以被重用(只需通过引用来访问任何一个选择器)
*   如果选择器命名正确，就很容易理解它所指向的元素的功能/目的
*   如果选择器坏了，您只需要在一个地方修复它

**Cons:**

*   虽然可以定义一个“复合”选择器来查询另一个元素中的一个元素(例如，父元素中的子元素)，但是它有点麻烦和不方便:

**2 .定义选择元素的自定义功能**

假设您足够幸运，能够访问被测应用程序的代码库。在这种情况下，您可以将测试属性添加到要交互的元素中，然后定义一个自定义命令，该命令将使用如下测试 id 来查询这些元素:

另外，您可以让 TypeScript 知道(如果您使用它的话)Cypress API 已经被扩展:

现在，通过使用这个自定义命令，我们可以通过将选择器提取到单独的函数中来重用它们:

我们的测试将如下所示:

由于我们定义的命令支持“相对”选择器，我们也可以搜索其他元素中的元素:

值得注意的是，这种方法可能会导致不可靠的测试(在极少数情况下)。事情是这样的， [**柏命令只重试断言**](https://docs.cypress.io/guides/core-concepts/retry-ability.html#Only-the-last-command-is-retried) 之前的最后一个命令。实际上，这意味着如果你有一堆嵌套的`find`命令，如下例所示

```
cy.get(<root>).find(<parent>).find(<children>).shold(<assertion>)
```

并且断言失败，Cypress 将只重试断言前的最后一个命令(上例中的`.find(<children>)`)。因此，如果第一个`find`命令(`.find(<parent>)`)针对错误的父元素执行，您的测试将会失败。有关此行为的详细解释，请参见[官方文档](https://docs.cypress.io/guides/core-concepts/retry-ability.html#Only-the-last-command-is-retried)。

同样值得注意的是，在 200+ E2E 测试中，我只看到这种情况发生了两次，而且这两次测试只在 CI 容器中失败(正如文章中提到的)。

这种方法的优点和缺点与前一种方法非常相似:

**优点:**

*   这种方法允许您定义一次选择器，然后通过调用查询元素的函数来使用它们
*   如果您的“选择器函数”命名正确，就很容易推断出它们返回什么元素
*   如果一个选择器坏了，只有一个地方需要修复

**缺点:**

*   这种方法在 99%的情况下都有效，但是在某些情况下，您可能会遇到令人不愉快的剥落

我已经使用这种方法很长时间了，但是它似乎不是最好的解决方案，因为有可能引入一个不可靠的测试(即使它很肤浅)，并且使用函数来选择元素的测试代码似乎有点麻烦。

**3。将选择器存储在页面对象中**

是的，我知道，Cypress 团队认为 [PageObject](https://martinfowler.com/bliki/PageObject.html) 是一个反模式，根据[文章](https://www.cypress.io/blog/2019/01/03/stop-using-page-objects-and-start-using-app-actions/)，你应该避免使用它。理由是 PageObject 模式“引入了另一个间接层”，并阻止您在“隔离”状态下测试您的特性。虽然这些都是有效的观点，但是“孤立测试”并不是我大部分时间都需要的。相反，我更喜欢测试覆盖多个页面的完整流程，这正是 PageObject 模式派上用场的地方。我认为该模式有助于组织和重用选择器(以及其他一些东西)。

据我所知，在 Java 的“自动化世界”中，将选择器存储在类/接口中并使用注释声明性地定义它们是一种常见的技术。以下是使用 [atlas](https://github.com/qameta/atlas) 选择器的代码示例:

我没有找到任何允许在 Cypress 中做类似事情的库，所以我写了自己的库。它被称为 [cypress-selectors](https://www.npmjs.com/package/cypress-selectors) ，它使您能够声明性地定义您的选择器(就像上面的例子一样)。

让我们来看一些例子。首先，让我们定义一个类，并声明性地定义我们的选择器:

接下来，让我们在“示例”测试中使用这些选择器:

如您所见，您可以通过访问一个类的成员来查询元素——就这么简单。

该库允许通过`attribute`、`class`、`id`、`xpath`、`type`和 jQuery `selector`选择元素。

它还支持查询另一个元素中的元素(复合选择器):

正如您在上面的例子中看到的，您可以为一个元素分配一个“别名”,然后在另一个选择器中引用它来指定它的父元素。

除了方法#1 和#2 的“优点”,还有几个优点:

*   这种方法允许您以声明方式定义选择器
*   您可以通过访问成员或 PageObject 类来查询元素
*   指定选择器的“父代”很容易
*   这种方法没有方法#2 中描述的问题——该库不构建一个`find`命令链，而是按照文档的建议合并查询[。](https://docs.cypress.io/guides/core-concepts/retry-ability.html#Merging-queries)

在过去的几个月里，我一直在我的项目中使用这种方法，我对结果很满意——测试代码简洁易读。在上述四种方法中，这一种对我来说似乎是最佳的。查看文档，了解更多关于 https://anton-kravchenko.github.io/cypress-selectors/图书馆的信息。

每种方法都有自己的优点，由您决定哪种方法最适合您。欢迎在评论中分享你的想法，祝你编码愉快！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)