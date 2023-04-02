# 7 个最常见的 Git 错误

> 原文：<https://javascript.plainenglish.io/7-most-common-git-mistakes-eefdd5a5b0?source=collection_archive---------3----------------------->

## 以及如何轻松解决它们

![](img/900ad46a7a1b10542a543631a5af54ef.png)

很多新手容易犯错，尤其是刚开始的时候。这是完全正常的，因为 Git 会变得非常复杂，这取决于项目的大小。在本文中，我想通过向您展示 7 个最常见的 Git 错误，更具体地说是 Git 问题，以及如何轻松解决它们，来加速您学习 Git 的成功。

它从 7 个最常见的 Git 错误及其解决方案开始:

# 1.放弃对本地文件的更改

作为一个程序员，每天都会发生意想不到的错误。为了快速解决错误，我们疯狂地摸索代码。不幸的是，这些代码更改并不总是最佳的。因此，快速撤销您所做的更改会很有帮助。

使用“git checkout”命令，您可以将文件重置为其原始状态:

```
# Reset directory "myCode"
git checkout - myCode
```

# 2.撤消本地提交

您已经创建了四个新的提交，现在才意识到其中一个提交包含一个主要错误。哎呀！

不要惊慌。如果想撤销一个或多个提交，可以使用“git reset”命令。该命令知道三种不同的模式(软、硬、混合):

```
# Undo the last four commits, keep changes
git reset HEAD ~ 4

# Undo the last four commits, discard changes
git reset --hard HEAD ~ 4
```

**注意:**使用“硬”模式时要小心一点。一旦执行“git reset — hard ”,工作树和索引就会被重置。所有更改都将永远丢失！

# 3.从 Git 中移除文件，而不完全删除它

您经常将一个不属于暂存区的文件添加到那里(git add)。您可以在这里使用命令“git rm”。但是，这也会从文件系统中删除该文件。

但是，如果您想将文件保留在文件系统中，您可以使用*" git reset<filename>"*将它从暂存区中移除。然后将文件添加到。gitignore，这样您就不会在将来错误地将其打包回暂存索引中。事情就是这样:

```
git reset Dateiname
echo Dateiname >> .gitignore
```

# 4.随后编辑提交消息

每个程序员都会在提交时犯一个错误。幸运的是，使用“git commit-amend”命令很容易纠正提交消息。事情就是这样:

```
# Start the standard text editor to edit the commit message
git commit --amend

# Sets the new message directly
git commit --amend -m "My new commit message
```

# 5.推送前更改本地提交

最后一点，你要知道“修改”这个选项。如果您想要更改上次提交，这很有用。但是如果要更正的提交不是最后一个呢？为此，您可以使用“git rebase-interactive”。

您必须在这里输入您的遥控器(通常是“原点”)和分支名称。

```
git rebase --interactive origin branchName
```

运行上面的命令将使用以下文本运行您的默认文本编辑器:

```
pick 9g2020f New feature ready
pick 23js34cc My commit
# Rebase 9g2020f..23js34cc onto 9g2020f
#
# Commands:
# p, pick = use commit
# r, reword = Used commit, but changed commit message
# e, edit = Use commit, but stop "amend"
# s, squash = use commit, but merge with last commit
# f, fixup = like "squash", but removes this commit message from the history
# x, exec = execute command (via the command line)
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
```

上面您会看到一个本地提交列表，后面是可用命令的解释。只需选择您想要更新的一个或多个提交。将 pick 改为 reword(或简称为 r)，它会将您带到一个新的视图，您可以在其中编辑消息。

然而，从上面的列表中可以看出，交互式 rebase 提供的不仅仅是编辑提交消息:您可以通过从列表中删除提交来删除提交，还可以编辑、重新排列和压缩提交。

# 6.撤消推送的提交

是的，不幸的是，错误的提交偶尔会进入远程存储库。

不过，不要绝望，因为 Git 提供了回滚单次或多次提交的简单解决方案:

```
# Commit anhand von Commit-ID rueckgaengig machen
git revert 453fsdu2#Undo the penultimate commit
git revert HEAD ^#Undo multiple commits
git revert feature ~ 4..feature ~ 2
```

如果您不想创建任何额外的恢复提交，而只想对工作树进行必要的更改，您可以使用-no-commit 选项(简称为-n):

```
# Undo the last commit, but don't create a revert commit
git revert -n HEAD
```

# 7.查找合并后导致错误的提交

在大型合并之后，跟踪导致失败的确切提交可能非常耗时。

幸运的是，git 有一个很好的二分搜索法工具，可以使用“Git 二等分”命令。首先，你必须开始设置:

```
# Start bisecting session
git bisect start#Mark the current revision as "bad"
git bisect bad#Mark the last known good revision as "good"
git bisect good revision
```

之后，Git 会自动检查“好”和“坏”之间的修订。然后重新运行您的代码。用“坏”或“好”标记提交，直到找到导致错误的适当提交。

额外提示:其他一切都失败了——这就是你解决问题的方式
到目前为止，我们已经看到了许多帮助解决日常 Git 使用中常见错误的命令和提示。

大多数问题都有一个相当简单的解决方案。但是有些事件需要大“锤子”这里唯一有帮助的是重写相应分支的历史。在实践中，这种情况经常发生在需要删除的敏感数据上。这有时可能是意外传输到公共可见存储库的客户登录数据。必须迅速安全地采取行动。事情就是这样:

```
git filter-branch — force — index-filter \
 ‘git rm — cached — ignore-unmatch logindaten.txt’ \
 — prune-empty — tag-name-filter cat — — all
```

上述命令每天从每个分支中删除 logindaten.txt 文件。此外，上述操作会删除所有可能为空的提交。

请特别小心 filter-branch 命令，因为存储库的整个历史将被重写。这可能导致高交易成本，并扰乱正在进行的项目中的整个开发团队的工作。

# 关于 Git 问题的结论

这是 7 个最常见的 Git 问题和错误及其解决方案的详细概述。您必须了解以下命令:

*   git 检验
*   git 重置
*   。gitignore
*   git 提交—修改
*   git rebase-交互式
*   git 还原
*   git 平分
*   git 过滤器-分支

我希望您可以在自己的项目中实现这里提到的一些技巧，以便在将来更快地解决 Git 错误，减少麻烦。