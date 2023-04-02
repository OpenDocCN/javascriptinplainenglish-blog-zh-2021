# 开始第一份工作时，你应该记住的 6 个步骤

> 原文：<https://javascript.plainenglish.io/6-git-steps-you-should-remember-when-joining-a-new-company-7dd7da5fbcb2?source=collection_archive---------9----------------------->

## 入职时应该知道的基本 git 命令和流程。

![](img/9d0e2435b5f0d5473e7726beab75dbf9.png)

是啊！你终于得到了这份工作。你通过了所有的技术面试，展示了惊人的软技能，完成了一个地狱般的技术测试，并像一个处于人质危机中的联邦调查局特工一样谈判你的工资。

你盯着电脑，也许是你的第一天，第三天，第八天。时候到了，你被分配了一张票。

你已经为此做好了准备，但是当你一打开终端，疑虑就开始蔓延。嘿，这是你的老朋友冒名顶替综合症(你以为你摆脱他了)。当在采访中被问及是否熟悉版本控制/git 时，你笑得像编码之神，心想“谁不熟悉”。

![](img/b004ea443b383a51e0755d4c90b94e3b.png)

但也许，只是也许你知道的没有你想象的那么多。也许在你的上一个公司，3 个人的初创公司专注于创建虚拟胡子，没有必要遵循 git 的最佳实践，你是唯一的前端，没有人真正关心，或者也许这是你的第一份工作，你所做的一切都是你自己的项目，即使你开始创建分支并编写有意义的提交消息，随着时间的推移，你最终会对所有提交编写“wip ”,并直接在 master 上工作。

首先，不要慌。这发生在我们最好的人身上。你不想成为一个问基本问题的人(相信我，这是你比任何人都想得多的事情，尤其是在最初的几天/几周)。所以，记得完成这些步骤，确保你遵循了新公司的指导方针。

## 1.GIT 拉

是的，这是我所知道的最基本的东西，但是你不希望在你的第一个 PR 上看到合并冲突，仅仅是因为你忘记从你的原始分支(develop/master)拉，并且你的代码没有更新。

```
git pull origin master
```

## 2.创建新分支

您已经更新了您的本地分支，现在您想要实际创建您将工作的分支，您将最终推动并创建 PR 的分支。

分支的命名是至关重要的，确保你遵循团队使用的惯例。这很可能与您正在处理的票证/故事有关。但是也许他们会添加是一个缺陷还是一个特性等等。对此要非常彻底，问一问，问完之后再问一次，这样你就能确定你的名字是正确的。

```
git checkout -b yourworkbranch
```

## 3.Git 提交

这是另一个关键步骤。有很多关于你应该如何写适当的提交信息的指南，你的公司可能会遵循一个特定的惯例，所以再次问，做笔记，并且要彻底。

```
git add .
git commit -m “Follow commit message guidelines”
```

## 4.Git rebase

您已经准备好推送代码并发出第一个拉取请求。但是等一下，你现在和其他开发人员在一个团队中工作，当你在编写代码的时候，你猜怎么着，他们也在工作！所以现在你当地的主支行不是最新的。不要惊慌，按照以下步骤操作:

*   提交当前分支中的更改
*   检查您当地的主要分支机构(可能是开发或硕士)
*   从远程源分支提取最后的更改
*   查看您正在处理的分支
*   做一个重置基础(git 重置基础大师)

```
git add .
git commit -m “Follow commit message guidelines”
git checkout master
git pull origin master
git checkout yourworkbranch
git rebase master
```

点击这里阅读 rebase 和 merge [之间的区别](https://www.perforce.com/blog/vcs/git-rebase-vs-merge-which-better#:~:text=Git%20rebase%20and%20merge%20both%20integrate%20changes%20from%20one%20branch%20into%20another.&text=Git%20rebase%20moves%20a%20feature,new%20commit%2C%20preserving%20the%20history.)

## 5.Git squash(可选)

您的工作分支是最新的，您准备好推送了，所以您首先提交，加上最后一次提交，您现在有三天的提交时间，您应该推送它们吗？让我们思考一下这个问题。

您一直在开发一个新的特性，现在理想情况下，当您的分支最终与主分支合并时，您可能希望看到提交消息中详细说明的特性、错误等的顺序。您不希望您的提交日志被不相关的提交消息污染。

```
871adf console logs again     
0c3317 wip
87871a Clean console logs
643d0e Refactor throttle
afb581 Clean console logs
4e9baa Debounce did not work back to throttle
d94e78 Change to debounce 
6394dc Add throttle to queries 
```

这就是壁球的由来。将你所有的承诺压缩成一个遵循公司惯例的承诺，这将完美地解释你过去三天都做了些什么！

为了挤压，你应该做一个交互式的 rebase，其中 N 是你想要挤压的提交的数量。

```
git rebase -i HEAD~N
```

点击该命令后，您选择的文本编辑器应该会显示您想要压缩的提交列表。按照说明选择采摘或挤压[这里](https://www.git-tower.com/learn/git/faq/git-squash/)关闭编辑器，你就可以开始了。

## 6.Git 推送

是时候了。不要害怕！推送并创建相应的拉取请求(同样，遵循如何创建特定于新公司的拉取请求的惯例)。

请记住，如果您的本地和远程分支有不同的提交历史，您将不得不强制您的 git 推送

```
git push origin yourworkbranch — force
```

现在，另一个完整的过程将开始，这保证了一个不同的职位，代码审查。如果你不得不根据评论修改代码(这是完全正常的),只需再次经历这些步骤，你就成功了(你甚至不需要再次创建 PR，它会自动更新)

## 结论

不要害怕问你的同事，每个公司的情况都有很大的不同。

***Git 拉取→创建分支→Git 提交→Git rebase → Git 挤压→Git 推送***

反复练习这一流程，你就会烂熟于心。

这就是你在新公司开始使用 git 的方式。我希望这能减轻你完成第一张罚单的压力！

还有记住，你 ***是*** 一个编码神。

![](img/ec63a5b70218ac5e92ce7240fb2dce69.png)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)