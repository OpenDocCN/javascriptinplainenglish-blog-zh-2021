# Git 分支:创建、切换到、列出和删除

> 原文：<https://javascript.plainenglish.io/git-branches-create-switch-to-list-delete-8b4c2ed7b189?source=collection_archive---------12----------------------->

## 了解 git 分支，有例子。

![](img/6b80ced0a3176fa8c61f7a5a24ab9a68.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Git 是一个分布式版本控制系统，用于在软件开发过程中跟踪源代码的变化。它是为协调程序员之间的工作而设计的，但也可以用来跟踪任何一组文件中的变化。

Git 的一些目标包括速度、数据完整性和对来自[**维基百科**](https://en.wikipedia.org/wiki/Git) 的分布式非线性工作流的支持

GIT 中的分支使开发人员能够同时处理不同的组件，这要感谢 GIT 简化了这个过程。

短篇故事。

> 以建造房屋的建筑工人为例。一些工人将铺地板，一些人粉刷墙壁，一些人准备水泥和一些抹灰。这些都是以完成房子的主要意图。

这同样适用于开发人员，因为开发人员的 git 分支之间简单高效的协作非常方便。

在本文中，我们将研究和学习 Git 中的分支。

*   创建 GIT 分支。
*   删除 GIT 分支
*   分支之间的切换
*   提交对 GIT 分支的更改

## **创建 GIT 分支**

为了从 ***主*** 创建一个分支，我们可以使用下面的命令。

```
git branch <name of your branch here>
```

第一个命令将使用分支后提供的名称创建一个分支

或者您可以使用命令

```
git checkout –b <name of your branch here>
```

这个 git 命令将嵌套这两个命令。首先，它将创建一个具有指定名称的分支，然后它将自动切换到该分支。

记住不要包含< >符号，否则 GIT 会提示你一个错误。

**列出分支机构**

要查看存储库中的可用分支，请运行以下命令:

```
git branch -a
```

## **删除 GIT 分支。**

我们可以在本地(在我们的系统中)或远程(GITHUB 存储库)删除一个 GIT 分支。

要在本地删除分支，我们使用命令。

```
git –d <branch name to delete here>
```

要删除远程分支，我们使用下面的命令。

```
git –D <branch name to delete>
```

这将删除一个分支，无论其合并状态如何。***–D***命令将协调执行 ***—删除*** 和 *** —强制执行**命令。

要删除远程分支(GITHUB 存储库),我们可以使用命令

```
git push origin –d <branch to be deleted>
```

该命令将从存储库中删除远程分支。

## **分支切换**

分支之间的切换非常容易。

首先，要列出给定存储库中所有创建的分支，正如我们上面看到的，我们可以使用命令。

```
git branch –a
```

它将列出给定存储库中所有创建的分支。

**提交更改。**

要提交对 git 的更改，我们将使用以下命令

```
git commit
```

这将打开您的默认编辑器，有时可能是 VIM 编辑器。然后，您将编写一个与您的提交相关的小插图。

另一种避免 VIM 编辑器的简写方法是，我们可以使用***–m***命令标志。

这将提交更改，并在花括号中提供消息

```
git commit –m “this is my initial commit”
```

## **出发前**

GIT 是一个非常强大的版本控制软件。了解并掌握它，在软件开发中非常得心应手。

感谢你阅读这篇文章，如果你觉得有帮助，请分享。

再次感谢你。

直到下一次和平和保持安全。

## **更多阅读:**

[](/4-backend-javascript-frameworks-to-check-out-if-you-are-a-frontend-developer-bb09cfa6d25b) [## 4 个后端 JavaScript 框架，看看你是不是前端开发人员

### 想学后端？然后查看这些框架。

javascript.plainenglish.io](/4-backend-javascript-frameworks-to-check-out-if-you-are-a-frontend-developer-bb09cfa6d25b) [](/why-you-should-consider-contributing-to-open-source-f8210d48804d) [## 为什么你应该考虑为开源做贡献

### 为开源做贡献的好处。

javascript.plainenglish.io](/why-you-should-consider-contributing-to-open-source-f8210d48804d) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)