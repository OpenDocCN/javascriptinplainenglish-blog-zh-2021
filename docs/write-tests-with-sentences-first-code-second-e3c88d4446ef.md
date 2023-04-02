# 首先用句子写测试，然后是代码

> 原文：<https://javascript.plainenglish.io/write-tests-with-sentences-first-code-second-e3c88d4446ef?source=collection_archive---------10----------------------->

## 不要一头扎进去，先写一个大纲，然后把它翻译成代码

![](img/ec2758c002162f284495b61dba83e7a8.png)

Photo by [Ben White](https://unsplash.com/@benwhitephotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 问题

在软件中，命名经常被认为是最难的部分之一。据我所见，编写测试也在上面！我看到人们一直在考试中挣扎。他们变得不知所措或沮丧，只是跳过它，这对每个人来说都是一件坏事。

命名很难，因为开发人员很少得到命名指南。随着时间的推移，他们学会了一些技巧和窍门，并制定了一些策略来简化命名。测试也是如此。

下面是我在编写测试时喜欢使用的一个策略。我鼓励我的团队也使用这种方法，并取得了巨大的成功。

## *前奏*

首先，这里概述的策略适用于大多数语言。下面的例子是用 Javascript 编写的，代码例子假设 [Jest](https://jestjs.io/) 是测试库。

第二，这不是 [TDD](https://en.wikipedia.org/wiki/Test-driven_development) 。TDD 完全是另外一种动物，超出了本文的范围。

第三，更有经验的开发人员可能会注意到这看起来非常类似于[小黄瓜](https://cucumber.io/docs/gherkin/reference/)。你的眼睛没有骗你，这个策略用了类似的词。

第四，我相信比我聪明得多的人已经创造了这些策略。我，以及我周围的人，不可能是唯一一个这样想写测试的人。如果你知道更好的来源，或者你以前见过，请在评论中告诉我。

# 规定

命名很难，因为有太多的选择。测试很难，因为人们很少谈论策略、指导方针，甚至从哪里开始。当然，信息是有的，但是我发现初学者很难理解并实际运用它。他们经常被看起来像外国人的语法吓跑，如果这没有吓走他们，他们就会陷入为`describe`或`test`块写什么的困境。

我已经通过首先把测试分成句子找到了成功。在我们写一行代码之前，我们首先写下我们想要覆盖的内容。我们应该把注意力集中在逻辑分支上，不要被代码所困扰。至少，现在还不是。

每组测试应该有三个部分:`topic`、`state(s)`和`expected result(s)`。

主题:我们正在测试的东西。这可能是一个函数、一个类方法、一个反应组件等等

**状态:**这些是*主题*可能会处理的变化。可以有任何数量的这些，也可以有`States`的扩展。

**预期结果**:给定特定的输入，我们应该预期特定的结果。

![](img/fa76148a4c879b08f7e38bffa650bb24.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 从句子开始

我鼓励我的团队从看起来有点像伪代码的句子开始。这对那些不习惯写作测试的人很有帮助。本练习允许您在担心如何编写代码进行测试之前，先专注于确定测试什么。

让我们看看这个结构是什么样子的。

```
topic
- when (a specific state)
  - should (the expected result)
```

对于更复杂的状态，我们稍微扩展一下，如下所示

```
topic
- when (a specific state)
  - and (and extension to this state)
    - should (the expected result)
  - and (and extension to this state)
    - should (the expected result)
```

这里有一些我们还没有谈到的关键词。这些词很重要，应该总是用来开始每个句子。

**When:** 这是`State`的第一个变型。
*例:“当传递负数时”、“当道具未定义时”、“当月亮满时”等。*

**和:**是亲本`State`的延续。`State`中可能出现的另一个问题或逻辑分支。
*例:“and # currentarchitem 为空字符串”，“and # currentarchitem 包括#name”等*

**应:**期待我们预计这里会发生什么？这个句子可能看起来和你最后的断言相似。
*例:“不应抛出”，或“应返回并实例 Foo”，“应返回错误”等。*

每个句子都应该简短且独特。如果您发现您的测试描述超过 120 个字符，那么它们太长了。

在我看来，就结构而言，你真的不需要更多。我鼓励你将`when`和`and`嵌套在不超过 3-4 层的深度。有了这些，你就有了可读性、上下文和简单性。这很容易维护，并且在编写测试时对每个人都有内在的期望。这导致了相同性，然后导致了可维护性。🎉

![](img/abb860184ce8d27b57b6308c99080fcc.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 写一些测试

既然我们已经研究了这个理论，让我们把它付诸实践吧！看看下面的小函数。我们将在一些测试中使用该函数作为`Topic`函数，这样我们就可以知道在现实生活中这些函数是如何工作的。

A simple max function. *Yes, there is a javascript built-in that does this already. For demonstration purposes only.*

这里我们有一个叫做`max`的简单函数，它接受两个值，比较它们，并返回两者的最大值。这个函数中有一些我们需要测试的逻辑。用*句子而不是编码*，让我们开始吧。

首先考虑一些可能的逻辑分支，然后用我们上面谈到的词来解释它们。开始往往是最难的部分，所以让我们从小处着手。我们甚至不会关心这里的`expectations`，只关心`states`的一部分。

这里我们应该关心的逻辑分支是什么？这不需要完美，甚至不需要完整，我们只需要一个起点。

```
max
- when `valueOne` is equal to `valueTwo`
- when `valueOne` is less than `valueTwo`
- when `valueOne` is greater than `valueTwo`
```

这似乎有点太容易了，对吗？让我们继续添加一些伴随这些状态的`expectations`。

```
max
- when `valueOne` is equal to `valueTwo`
  - should return `valueOne`- when `valueOne` is less than `valueTwo`
  - should return `valueTwo`- when `valueOne` is greater than `valueTwo`
  - should return `valueOne`
```

你有它！我们有一些可以翻译成代码的句子。这些句子 ***读起来像英语*** 而不是伪代码。去吧，现在就给自己读一段。

读起来不错，不是吗😉

这里有我漏掉的条件吗？(*提示:* **是**)。你能找到它们并写出你自己的句子吗？

## 将句子翻译成测试

使用我们已经写好的句子，我们现在可以把它们翻译成看起来像真实测试文件的东西:

信不信由你，这只是足够运行的代码！Jest 会为`[test.todo()](https://jestjs.io/docs/api#testtodoname)`块输出不同的颜色，所以这其实是有效代码！就个人而言，我喜欢用这种方式来搭建我的测试。

然而，使用`todo`除了给出一个待办事项列表之外，并不能给我们提供更多信息，所以让我们用一些真实的测试来填充这些列表:

你可以看到，进行这些测试不需要太多代码。我们已经完成了最困难的部分，通过写句子来确定我们在这里用代码写的大部分内容。首先做这一部分，使得编写测试相当简单。

我将在此提出一些其他的个人偏好，您的收获可能会有所不同:

*   使用一个名为`result`的变量来存储测试项的输出
*   当有意义时，使用一个名为`expectedResult`的变量来存储，你猜对了，预期的结果

这样做可以让你的测试读起来很好

```
expect(result).toEqual(expectedResult)
```

这有一个额外的好处，A)如果将来代码发生变化，有一个可靠的地方来改变预期，B)保持断言超级干净。

我们拥有的是一个非常好的开始！这些测试读起来很好，给了你一些不错的测试覆盖率。然而，仍有一些改进的余地。为了让我们的测试*读起来更好，我们应该给那些数字增加一些含义，而不是使用神奇的数字。*

*将输入移动到变量中给了它们上下文。这些数字现在有了意义。给这些东西起个名字可以很容易理解正在发生什么，更重要的是，上下文是什么。它让任何人都很容易看到这些测试并理解发生了什么。*

## *结论*

*你有它！首先用句子编写测试，然后将它们转移到代码中。它让这个过程变得可预测，不那么可怕，而且容易教。*

```
*topic -> when -> should*
```

*每次我写测试都是这样开始的。我充实了逻辑分支，然后是期望块，然后开始填充测试代码。当我为我的团队规划新工作时，我也做同样的练习，在一些新的案例中，我把这些句子包含在实际的标签中。我迫不及待地想知道事情会如何发展，敬请关注！*

## *参考*

*   *https://martinfowler.com/bliki/TwoHardThings.html*
*   *【https://en.wikipedia.org/wiki/Test-driven_development *
*   *[https://cucumber.io/docs/gherkin/reference/](https://cucumber.io/docs/gherkin/reference/)*
*   *[https://jestjs.io/](https://jestjs.io/)*
*   *[https://jestjs.io/docs/api#testtodoname](https://jestjs.io/docs/api#testtodoname)*

**更多内容请看*[***plain English . io***](http://plainenglish.io/)*