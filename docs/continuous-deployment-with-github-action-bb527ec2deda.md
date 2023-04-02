# GitHub Action 的持续部署

> 原文：<https://javascript.plainenglish.io/continuous-deployment-with-github-action-bb527ec2deda?source=collection_archive---------12----------------------->

## 使用 GitHub 动作实现持续部署的简单方法。

![](img/70387bd1a36f1f976567110b1688c861.png)

Photo by [De an Sun](https://unsplash.com/@andyadcon?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/continuous?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

本文演示了一种使用 GitHub 动作进行连续部署的简单方法。它适用于所有类型的后端和前端，如 Node.js、Ruby、Python、PHP、Vue.js、React、Angular 等。这种方法很简单，没有成本&更重要的是，它可以用于生产。

*是中级文章；适用于那些手动将应用程序部署到服务器，但难以实现自动化的人。此外，GitHub 操作的基本知识是预期的。*

**这是两个主要步骤**

1.  使用 SSH 和 GitHub 进行部署
2.  自动化步骤 1

# 1.使用 SSH 和 GitHub 进行部署

这是正常的部署策略，即如何通过 SSH 和 git 手动部署应用程序。

1.  通过 SSH 连接到服务器
2.  创建 SSH 密钥
3.  将公钥添加到 GitHub 的部署密钥中
4.  将 Repo 克隆到服务器
5.  设置项目
6.  运行项目

至此，项目应该可以顺利运行了。下一步是通过 GitHub Action 自动化相同的过程。

# 2.自动化步骤 1

## **A .配置必要的值**

转到 GitHub Repo 设置机密

创建 3 个`New repository secrets`

*   SSH_PRIVATE_KEY_DEV:来自服务器的 SSH 私有密钥
*   主机开发:服务器的主机名
*   用户名:服务器用户名

如果你使用`ssh root@xx.xx.xx`来访问服务器。`root`是**用户名**而`xx.xx.xx`是**主机 _ 开发**。

## **B .创建 YML 文件**

在项目目录里面创建一个. **yml** 文件`deploy.yml`在

项目目录→。github →工作流程→ `deploy.yml`

`deploy.yml`文件包含部署脚本。

**示例:将 Vue.js/React/Angular 项目自动部署到服务器**

**示例:将基于 pm2 的 Node.js 应用程序自动部署到服务器&重启 pm2**

**示例:将相同的应用程序部署到 AWS S3，通过 AWS CloudFront 提供，** [**查看此代码片段**](https://bibhutipoudyal.com.np/snip/deploy-vuejs-to-aws/) **。**

将更改推送到`dev`上的 GitHub 或其他指定的分支。前往 GitHub 您的存储库 Actions 选项卡。

在那里，您将看到您最近执行的工作流运行的工作流。如果成功/失败，它将显示各自的日志。还是那句话，尝试一些改动，推给 GitHub。它会自动更新。

正如您已经注意到的，`yml`脚本使用`appleboy/ssh-action@master`来简化任务。虽然有点慢。如果您想要更快的替代方案，同样的任务可以手动完成。这里有一篇很好的文章:

[](https://blog.benoitblanchon.fr/github-action-run-ssh-commands/) [## GitHub 操作:如何运行 SSH 命令(没有第三方操作)

### 最近，我一直在使用 GitHub Actions 进行我的持续集成和持续交付。通常，我使用简单的…

blog.benoitblanchon.fr](https://blog.benoitblanchon.fr/github-action-run-ssh-commands/) 

另一件需要考虑的事情是 GitHub 动作定价。一个免费的计划是有限制的。你可以在这里找到更多[的细节。](https://github.com/pricing)

这种方法和你在**步骤 1(手动)**中做的完全一样。它使用凭证通过 SSH 访问服务器:用户名、主机& SSH 私有密钥(之前在 GitHub →设置→秘密中提供)。然后执行指定的命令来构建项目&如果需要的话重启服务器/进程管理器。

*更多内容看* [***说白了就是 io***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和**[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。**