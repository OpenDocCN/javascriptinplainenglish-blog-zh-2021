# 你正在处理遗留代码的 3 个迹象

> 原文：<https://javascript.plainenglish.io/3-signs-that-youre-dealing-with-legacy-code-977291667b4c?source=collection_archive---------12----------------------->

![](img/9d1cba462d0b749922e31345dc158704.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

开发人员经常谈论遗留代码。似乎每个人都有自己对遗产的定义。如果你问支持 TDD 方法的人，你可能会得到这样的答案:遗留代码是任何缺乏自动化测试的代码。

其他人将其定义为缺乏文档支持的代码，因此任何人都很难维护它。

一个非常模糊的定义是，遗留代码是除你之外的其他人写的任何代码。

我认为上述每一个定义背后都有真理，但是它有助于分解遗留代码到底是什么。因为只有当我们意识到某件事的时候，我们才能真正做些什么。我认为大多数开发人员都同意遗留代码通常是有问题的，不应该保存太久。

# 1.该代码缺乏支持

缺乏支持可能意味着以下情况之一:

a)代码缺乏对自动化测试的支持。当谈到自动化测试时，您通常指的是三者之一:单元测试、集成测试和端到端测试。

b)该规范缺乏书面文件的支持。

c)代码缺乏对口头文档的支持。

在任何情况下，代码都没有得到足够的支持，以至于任何对代码没有深入了解的开发人员都无法轻松地使用它。代码严重依赖于它的作者，不容易被其他人继承。

每当你发现自己写的代码让周围的人很难理解和阅读，并且他们经常问你这个问题，你可能会考虑是否应该重写这些代码。在某些情况下，由于特性的实际复杂性，重写它可能不会使它变得更好。但是尽管如此，如果特性是复杂的，它仍然应该在自动化测试和文档方面得到支持。

# 2.一般的开发人员害怕对代码进行修改

这与第一个迹象有些关联。这里的要点是，如果代码和作者之间存在紧密的依赖关系，那么除非被强迫，否则很可能没有人会尝试去接触它。

当任何开发人员能够阅读、完全理解代码，能够跟随程序的流程，甚至毫无畏惧地调整和修改代码时，代码就被认为是干净的。如果人们试图避开你写的那部分代码，那么很有可能你已经产生了遗留代码。遗留代码是最终成为难以偿还的技术债务的一部分。

最坏的情况是遗留代码需要被扔掉，因为没有人能够处理它，甚至阅读它。这是为了让软件在未来继续工作而必须更换的时候。人的需求变了，软件也要跟着变。

# 3.编写代码的平台和工具不再受其创建者的支持

尽管这可能不像前面提到的遗留代码的两种迹象那样普遍，但它仍然可能发生，尤其是在技术发展比以往任何时候都更快的时代。几年前被大肆宣传的框架或语言可能已经不再被认为是相关的了。

我认为，即使某个框架不再受其创建者的支持，代码也可以用于生产，只要该框架是成熟的，并且它通常是一个稳定的框架，并具有定制它的能力。但是随着技术越来越老，越来越少的开发人员会喜欢使用它。

# 处理遗留代码的三种方法

毫无疑问，代码可能会有味道，可能会很难处理。事实上，作为一名开发人员，你将在职业生涯中面临遗留代码，这也是不可避免的。我们可以抱怨事情有多糟糕，挠头想知道为什么代码是以某种方式编写的。但是，就我个人而言，我认为更健康的做法是将注意力转移到如何处理遗留代码，并在这样的环境中工作，同时保持头脑清醒，而不是被项目的糟糕性质所吸引。

我完全理解处理遗留代码的痛苦，有时表达出来是有帮助的。但更重要的是，我们需要记住，作为一名工程师，我们的工作主要是随着时间的推移改进事情，并以成熟的方式处理问题。

在旧系统中处理遗留代码时，需要记住以下三点:

## 1.尽最大努力不要破坏软件的现有部分。

少即是多。有时，您可能会发现自己在追踪一个 bug，并在几乎一个完整的工作日内上下滚动一堆文件，结果只是通过添加一两行代码来修复这个 bug。无论尝试改变这里或那里的事情有多么诱人，试着保持专注，只做解决现有问题所需的最小改变。

## 2.尝试以不影响其他地方代码的方式改进代码

如果有改进的空间，那么重构可能不是一个坏主意。但是，仍然非常重要的是，你可以对你的重构保持信心，并且知道它不会影响其他任何事情。在最好的情况下，代码已经被测试过了，如果你不小心破坏了什么，测试会对你大喊大叫。

## 3.通过测试来增加代码的测试覆盖率

这不仅有助于你理解遗留代码，而且也提高了软件的安全性和质量。

测试也可以作为代码实现的技术文档。很多时候，你可以通过一套描述代码的测试来理解代码应该做什么。

# 最后的话

每个人都有权对遗留代码发表自己的意见。了解代码何时面临变成遗留的风险以及如何防止这种情况发生是一件很有用的事情。但是底线是遗留代码随处可见——在公司项目、开源项目中，你能想到的都有。即使是最大的科技公司也有一些纯粹的遗留代码。专业工程师的角色是能够应对这样的环境，并充分利用每一种情况。