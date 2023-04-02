# 文档和良好的代码可以拯救生命

> 原文：<https://javascript.plainenglish.io/documentation-and-good-code-save-lives-3a25c93c8582?source=collection_archive---------14----------------------->

## 阅读别人的代码是如何妨碍我工作的，以及如何解决这个问题。

![](img/de88a7f465b326a51676d43ce0ef40c5.png)

Photo by Derek Lee on Unsplash

大学教授总是会给他们的学生布置带有预先编写好的代码的作业，供他们使用和构建。这是学习真正的行业技能的好方法，因为大多数开发人员不一定从零开始从事项目。他们得到了包含数百行代码的文件，几乎没有任何文档。当某种形式的文档出现时，它是类似于`updated on <this date>`或`developed by <this professor>`的东西。比糟糕的文档更糟糕的是糟糕的函数和变量命名约定。

关于命名，作用域和局部变量是最糟糕的。有没有遇到过这样的人，他在没有任何上下文的情况下编写变量名，如`test`或`a`？也没有记录吗？

这不是发生在大学或新兵训练营的事情。但是最终在工作的时候，你会遇到这些类型的开发人员，他们写的代码质量很差，阻碍了开发过程，给整个团队带来了问题。由于这种糟糕的实践，你会遇到这样的情况:唯一能够修复 bug 的人可能就是最初编写它的人。

那么我们作为开发者如何改掉这个坏习惯呢？

以下是我在学校学到的和从工作中得到的一些建议。这些不一定是行业惯例或约定，但是它们可以帮助您、您的团队、您的项目合作伙伴，或者使您的任务更容易管理。

# 1.有特定的命名约定

作为开发人员，我们听说过 Snakecase、Pascalcase 和最著名的 Camelcase。在某些情况下，我们用首字母大写或所有字母大写来命名全局变量。但是您不应该就此止步，只使用一些命名约定。

如何区分项目的全局状态和组件中的状态？每当给变量和函数命名时，我都遵循一条严格的规则:

我宁愿使用长的描述性的变量和函数名，而不是短的非描述性的变量和函数名。

我说的不是像`currentUserEmailFromCookieSessionWhenLoggedIn`这样的名字，很明显这太长太多了。

在着手一个当前的或新的项目之前，和你的团队或小组想出命名惯例。钩子的命名惯例是什么？全局函数怎么样？你如何识别一个项目的全局状态和一个组件的状态？

当我从事辅助项目时，我的项目的全局状态和组件的状态看起来像这样:

*   `GLOBAL_STATE`:项目的全局状态
*   `state`:部件的状态

它变得比这更复杂，但这只是一个一般的想法，你可以把它融入到你的项目中。我有时喜欢混合多种命名约定，这样 Snakecase 变量的含义与 Camelcase 变量完全不同。

# 2.解释你做了什么

理解如何编写自己的代码很容易，但是几个月或几年后，当你不得不回去修复一个错误时，就不容易了。

利用您的 IDE 的扩展和工具！我将 VSCode 用于我所有的开发乐趣，并下载了大量的扩展以使我的生活更加轻松。

用 JavaScript 开发时，我使用 VSCode 的文档支持快捷方式。在 Javascript 中的函数上方键入`/** enter`，VSCode 将创建一个总结您的函数的文档片段。

[](https://code.visualstudio.com/docs/languages/javascript#_jsdoc-support) [## 使用 Visual Studio 代码进行 JavaScript 编程

### 充分利用 Visual Studio 代码进行 JavaScript 开发

code.visualstudio.com](https://code.visualstudio.com/docs/languages/javascript#_jsdoc-support) 

在注释的末尾，不要忘记添加`@return`来指定变量类型和返回的内容。

一个技巧是添加正在返回的数据的结构！

示例:

```
/**
 * This code does something
 * @params { string } some_variable This variable is something
 * @return { Array } some_other_variable This is a return variable
 * [
 *  { ID: 0, name: 'John Doe' }
 * ]
 */
function something(some_variable) { ... return some_other_variable }
```

# 3.应用软件开发原则

如果你像我一样，有时会忘记写文档，那么最好掌握一两条软件开发原则。

你工作的公司可能会要求你一直使用一个特定的原则，但对于那些与团队合作或参与团队项目而没有一套原则的人来说，这里有几个原则可以考虑:

所有这些原则都是不言自明的，所以我不会说得太详细。

## D.R.Y(不要重复自己)

你得注意你写的东西！回到大学时代，当我可以很容易地写一个 switch 语句时，我会写 10 个 if 语句。

如果你发现一个函数和你之前写的太像了，你会怎么把两者结合起来？把它们组合在一起可以吗？减少重复代码的数量比试图改变你能写多少代码更重要。

## K.简单明了

让你的代码尽可能简单。你不需要所有的链式函数来展示你的代码有多复杂，你只是在给你自己和你的团队制造麻烦。

有一个看起来太复杂的函数吗？把它拆开，开始把链式函数赋给变量，让别人理解你。当你不能展示你如何帮助其他开发者理解你的代码时，没有人喜欢炫耀。

## Y.(你不需要它)

当开始一个新项目时，有时我们被驱使着让事情看起来“很酷”，而忘记了每个项目的大图:最小可行产品(MVP)。

是的，当有人登录他们的帐户时，有一个动画看起来很酷，但是登录有效吗？我们对它们的认证正确吗？有 cookie 会话吗？cookie 会话加密了吗？当有人创建一个帐户时会发生什么？他们的密码是散列的吗？

这些问题比在用户登录时添加动画或添加新功能要大得多。我们需要解决那些会给我们项目的功能带来更大问题的事情，而不是让事情看起来很漂亮。

# 4.创建 README.md 文件

如果你仍然觉得你的代码太复杂，那么我建议你写一个 README.md 文件来概述你是如何构建你的代码的架构的。

几乎所有你能在 GitHub 上找到的库都有一个 README.md 文件，里面有指令、结构和如何使用库的例子。

如果您不知道如何编写一个好的 README.md 文件，这里有一些关于如何编写的好文章:

 [## 初学者指南写一个牛逼的自述✍

### 嘿初学者，

meakaakka.medium.com](https://meakaakka.medium.com/a-beginners-guide-to-writing-a-kickass-readme-7ac01da88ab3) [](https://betterprogramming.pub/how-to-write-a-readable-readme-590ae6124f69) [## 如何写一篇可读的自述

### 不要用 READMEs 来混淆开发者

better 编程. pub](https://betterprogramming.pub/how-to-write-a-readable-readme-590ae6124f69) [](https://www.freecodecamp.org/news/how-to-write-a-good-readme-file/) [## 如何为你的 GitHub 项目写一个好的自述文件

### 如果你正在阅读这篇文章，这可能意味着你已经在将资源库推送到 GitHub，甚至可能…

www.freecodecamp.org](https://www.freecodecamp.org/news/how-to-write-a-good-readme-file/) 

# 5.代码审查

代码审查就像车主换油一样。给汽车换油可以保持发动机润滑，防止过热。换油还可以清除污垢和碎屑。

开发人员需要清除那些可能会让你的团队陷入困境的污垢和碎片。代码审查有助于你发现自己的坏习惯，尤其是如果你是一家公司的初级员工。

代码评审并不是批评你的工作有多糟糕，或者你作为一名开发人员有多糟糕。他们是一只引导的手，推动你成为下一代开发者的下一代前辈。你的前辈会确保你明白如何写出和他们一样好，甚至比他们更好的代码。

当我写这篇文章的时候，我很羡慕我正在做的项目是如何被很好地记录下来的。它很老了，但是写它的人已经退休很多年了，我坐在我的办公桌前试图修复一个过时的功能。每个函数的每个文档都写得非常清楚，我真的不需要跟踪很多代码。

*更多内容看*[***plain English . io***](http://plainenglish.io/)