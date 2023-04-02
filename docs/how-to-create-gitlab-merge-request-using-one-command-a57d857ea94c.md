# 如何仅使用一个命令创建 Gitlab 合并请求

> 原文：<https://javascript.plainenglish.io/how-to-create-gitlab-merge-request-using-one-command-a57d857ea94c?source=collection_archive---------4----------------------->

![](img/c18d0043258051d88f1e69c667b78cf9.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

故事开始于一个开发人员开始对开发工作流感到厌烦和厌倦，并尽最大努力至少改进工作流的一个部分，并感到更有生产力。

如果你厌倦了使用 Gitlab 网站创建合并请求，你想以一种更快更简单的方式来做，那么这篇文章可能就是你正在寻找的。事不宜迟，我们开始吧。

# 逐步指南

在我们深入研究分步指南之前，让我们先定义一下我们希望实现的结果。

# 结果

这是我们希望的最终结果。

*   **使用一行命令创建合并请求。**

# 将任务分成更小的部分

*   将当前本地分支推至远程。
*   为此本地分支创建合并请求。
*   将合并请求目标设置为主分支。
*   合并后必须删除源分支。(删除源分支)。

事实上，Gitlab 提供了 push 选项，使用一个命令就可以做到这一点。你可以参考完整的文档[这里](https://docs.gitlab.com/ee/user/project/push_options.html)。

*   推送选项— `merge_request.create`允许我们创建合并请求。
*   推送选项— `merge_request.target=master`允许我们将合并请求的目标分支设置为主分支。
*   推送选项— `merge_request.remove_source_branch`允许我们在合并请求被合并时设置移除源分支。

在我们理解了每个选项的作用之后，下面是完整的命令:

```
# Here will be the format of the command linegit push -o merge_request.create -o merge_request.target=master -o merge_request.remove_source_branch $upstream_remote_name $local_branch_name# Sample run commandgit push -o merge_request.create -o merge_request.target=master -o merge_request.remove_source_branch origin feature/payment-integration
```

# 优化命令

我们已经取得了我们想要的结果。但是，写上面这个长命令可能比在 Gitlab 网站上创建合并请求还要糟糕(我个人的感觉)。

幸运的是，我们可以使用 Git alias 使它变得更好、更短。下面是我如何在我的`.gitconfig`文件中定义我的 Git 别名。

```
[alias]
  bn = "!git rev-parse --abbrev-ref HEAD"

  mrtd = "!git push -o merge_request.create -o merge_request.target=development -o merge_request.remove_source_branch origin $(git bn)" mrts = "!git push -o merge_request.create -o merge_request.target=staging -o merge_request.remove_source_branch origin $(git bn)" mrtp = "!git push -o merge_request.create -o merge_request.target=master -o merge_request.remove_source_branch origin $(git bn)"
```

我有 4 个 Git 别名:

*   **bn** :打印当前分行名称
*   **mtrd** (合并开发请求):这为我们必须输入的长命令创建了一个别名，该命令创建了一个从当前分支到开发分支的合并请求。

简而言之，这个长命令已经简化为:

`git push -o merge_request.create -o merge_request.target=master -o merge_request.remove_source_branch origin feature/payment-integration`

对此:

*   `git mrtd`:创建合并请求到开发分支。
*   `git mrts`:创建对暂存分支的合并请求。
*   `git mrtp`:创建生产分支的合并请求。

# 结论

我个人非常喜欢这样的结果，因为它节省了我创建合并请求的大量时间。你每天节省的一点点时间累积起来，在你的整个职业生涯中会节省大量的时间。

我希望你喜欢这篇文章，我会在下一篇文章中看到你！

# 参考

本节总结了我在研究该主题时发现的资源:

*   Gitlab 推送选项[文档](https://docs.gitlab.com/ee/user/project/push_options.html)。
*   罗布·米勒的[Git config](https://gist.github.com/robmiller/6018582)——一些每天都在使用的有用的 Git 别名。

> 最初发表在我的[博客](https://tekloon.dev/how-to-create-gitlab-merge-request-using-one-command)上。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)