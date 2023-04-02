# 使用 GitHub 操作部署到 Heroku

> 原文：<https://javascript.plainenglish.io/deploy-to-heroku-with-github-actions-a890044a620f?source=collection_archive---------6----------------------->

![](img/c3d616aa1190106a599ee163700b3088.png)

[Heroku](https://b.remarkabl.org/heroku)

这篇文章讲述了如何使用 [GitHub Actions](https://b.remarkabl.org/github-actions) 工作流部署到 [Heroku](https://b.remarkabl.org/heroku) 。

# 先决条件

## 赫罗库

创建一个 Heroku 应用程序，并保存与您的帐户关联的应用程序名称和电子邮件。然后进入[账户设置](https://dashboard.heroku.com/account)复制你的`API Key`。

## 开源代码库

进入你的 GitHub 库的`Settings` > `Secrets`，设置[秘密](https://docs.github.com/en/actions/reference/encrypted-secrets):

*   `HEROKU_API_KEY`
*   `HEROKU_APP_NAME`
*   `HEROKU_EMAIL`

## GitHub 操作

使用[部署到 Heroku](https://github.com/marketplace/actions/deploy-to-heroku) 操作部署的工作流:

动作推至`[main](https://devcenter.heroku.com/articles/git-branches)` [分支](https://devcenter.heroku.com/articles/git-branches)。

查看附加的[选项](https://github.com/marketplace/actions/deploy-to-heroku#options)。

## 自定义工作流程

使用自定义作业部署的工作流:

下面解释了这两种工作流之间的区别。

## 检验

[Checkout](https://github.com/marketplace/actions/checkout) 动作必须[获取整个 Git 历史记录](https://github.com/marketplace/actions/checkout#fetch-all-history-for-all-tags-and-branches)，否则构建将失败，并出现错误:

## Heroku 登录

`[~/.netrc](https://devcenter.heroku.com/articles/authentication#api-token-storage)`包含 Heroku 登录凭证:

## 使用 Git 部署

然后设置 [Git 遥控器](https://devcenter.heroku.com/articles/git#for-an-existing-heroku-app)并按下[按钮](https://devcenter.heroku.com/articles/git#deploying-code):

我们在这里推进到`master`分支，但是我们也可以推进到`main`。

# 例子

[库](https://github.com/remarkablemark/github-actions-heroku-deploy)包含代码示例。

成功的部署看起来是这样的:

*本文原载于《remarkablemark.org》2021 年 3 月 12 日。*