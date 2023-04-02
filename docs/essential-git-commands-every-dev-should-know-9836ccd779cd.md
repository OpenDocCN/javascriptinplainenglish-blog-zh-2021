# 每个开发人员都应该知道的基本 Git 命令

> 原文：<https://javascript.plainenglish.io/essential-git-commands-every-dev-should-know-9836ccd779cd?source=collection_archive---------16----------------------->

## 我每天使用的 11 个 Git 命令

![](img/7f9f67cef561a4c50646ac9de0c2a0f9.png)

So many branches — Photo by [Ron Whitaker](https://unsplash.com/@ronwhitaker?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/branch?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当我开始我的职业生涯时，我总是害怕丢失我的代码更改。有时，我会将代码复制到文本文件中，以确保不会遗漏任何东西。

这不是一个很好的实践。如果你知道如何正确使用 git，你就不会有这些疑虑。

Git 拥有让你安全所需的一切。还有更多。

让我们开始吧。

## 1.检查一个新的分支

显然，我必须为我开始的每个任务使用一个新的分支:

```
git checkout -b <new_branch_name>
```

该命令创建一个新分支，并自动将其设置为活动状态。

## 2.选择文件进行提交

这是我喜欢 GUI 的少数情况之一。在 VS 代码(或任何其他更好的 IDE/文本编辑器)中，您可以很容易地看到更新的文件，并选择您想要包含在提交中的文件。

但是如果您想使用 CLI 来完成:

```
git add .
```

此命令将转移所有已更改的文件。

如果您想选择单个文件:

```
git add <path/to/file>
```

## 3.做出承诺

暂存一些文件后，您需要提交它们:

```
git commit -m "Some changes"
```

如果您打开了一些不允许您提交的预提交规则(如林挺)，您可以通过传递`--no-verify`标志来覆盖它们:

```
git commit -m "Some changes" --no-verify
```

## 4.还原所有更改

有时候，我会尝试代码。过了一会儿，我意识到这不是一条正确的道路，我需要撤销我所有的更改。

一个简单的命令是:

```
git reset --hard
```

## 5.查看最新提交

通过键入以下命令，我可以很容易地看到我的分支上发生了什么:

```
git log
```

我可以看到提交散列、消息、作者和日期。

## 6.从远程分支提取更改

当我签出一个已经存在的分支(通常是`main`或`development`)时，我需要获取并合并最新的变更。

有一个简单的说法:

```
git pull
```

有时，如果您在一个新创建的分支中，您还需要指定源分支:

```
git pull origin/<branch_name>
```

## 7.撤消本地未推送的提交

我做了承诺。该死的。这里有点不对劲。我需要再做一个改变。

不用担心:

```
git reset --soft HEAD~1
```

此命令将恢复您上次提交的内容，并保留您所做的更改。

`HEAD~1`意味着你的脑袋指向了比当前更早的一次提交——这正是你想要的。

## 8.撤消推式提交

我做了一些改变，并把它们推到远程。然后，我意识到这不是我想要的。

为此，我使用:

```
git revert <commit_hash>
```

请注意，这将在您的提交历史中可见。

## 9.隐藏我的更改

我正在开发这个特性，我的队友让我进行紧急代码审查。

显然，我不想丢弃我的更改，也不想提交它们。我不想创建一堆无意义的提交。

我只想检查他的分公司，然后回到我的工作上。

为此:

```
// stash your changes
git stash// check out and review your teammate's branch
git checkout <your_teammates_branch>... code reviewing// check out your branch in progress
git checkout <your_branch>// return the stashed changes
git stash pop
```

`pop`这里似乎很熟悉？是的，这就像一个堆栈。

也就是说，如果你连续做了两次`git stash`，中间没有`git stash pop`，它们会相互叠加。

## 10.将您的分支重置为远程版本

我搞砸了一些事情。一些失败的提交，一些失败的 npm 安装。

无论我做什么，我的部门都不再运转良好。

远程版本工作正常。让我们把它变得一样！

```
git fetch origin
git reset --hard origin/<branch_name>
```

## 11.从其他分支选取提交

有时，我想应用来自其他分支的提交。为此，我使用:

```
git cherry-pick <commit_hash> 
```

如果我想选择一个范围:

```
git cherry-pick <oldest_commit_hash>^..<newest_commit_hash>
```

# 结论

老实说，我并不是每天都使用所有这些命令，但是我确实经常使用它们。

我更喜欢 CLI，因为我们永远无法用 GUI 涵盖所有选项。

此外，您会发现大多数教程只使用 CLI。如果你不熟悉它，你将很难理解它们。

我在这里介绍了基础知识——但是无论你需要做什么——只要谷歌一下。

我确信你会很容易找到答案。

*更多内容看*[***plain English . io***](http://plainenglish.io)