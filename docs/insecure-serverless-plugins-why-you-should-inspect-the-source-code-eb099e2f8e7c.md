# 不安全的无服务器插件:为什么要检查源代码

> 原文：<https://javascript.plainenglish.io/insecure-serverless-plugins-why-you-should-inspect-the-source-code-eb099e2f8e7c?source=collection_archive---------21----------------------->

![](img/5368077d7b4f118f6d695f59b8d98a12.png)

Photo by [Dmitry Ratushny](https://unsplash.com/@ratushny?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无服务器框架支持许多插件，而且它们很棒！他们在部署我们的无服务器应用程序时节省了大量时间。为什么要重新发明轮子？这种便利有一个缺点:不是所有的插件都写得安全。我们必须明智地选择我们的插件，这意味着我们应该检查源代码。

# 什么是无服务器框架插件？

[无服务器框架](https://serverless.com/)允许我们在部署过程中使用插件(或创建一个插件)来连接[生命周期事件](https://gist.github.com/HyperBrain/50d38027a8f57778d5b0f135d80ea406)。在部署开始之前，我们可以连接到“before:deploy:deploy”事件来设置文件和变量。我们可以连接到“deploy:finalize”钩子来保存一些关于部署的信息。插件有很多可能性。

有一些插件:

*   [创建无服务器网站](https://github.com/MadSkills-io/fullstack-serverless)
*   [启用 AWS 云信息堆栈终止保护](https://github.com/miguel-a-calles-mba/serverless-stack-termination-protection)
*   [根据功能配置 AWS IAM 策略](https://github.com/functionalone/serverless-iam-roles-per-function)

还有更多。

为了使用插件，我们安装了 npm 包:

```
npm install --save-dev serverless-iam-roles-per-function
```

将插件添加到我们的无服务器配置文件(`serverless.yml`)中:

```
plugins:
  - serverless-iam-roles-per-function
```

并且，遵循插件需要的任何说明和设置。

我们现在已经改进并简化了我们的无服务器部署。

# 并非所有插件都有相同的安全级别

插件是由无服务器社区构建的。任何人都可以创建一个插件。无服务器框架公司列出了[插件](https://github.com/serverless/plugins)，但只有一小部分被“批准”。这意味着我们应该意识到我们在使用什么。

一个插件，允许我们在`serverless.yml`文件中添加 if-else 语句:[无服务器插件 IfElse 插件](https://github.com/anantab/serverless-plugin-ifelse)。这个插件很有用，因为我们可以根据部署场景调整我们的无服务器配置。

例如，我们可以部署特定于我们的`dev`阶段的功能，并将它们从其他阶段中排除。

```
service: insecure-plugins
​
provider:
  name: aws
  runtime: nodejs12.x
  stage: ${opt:stage, 'dev'}
  region: us-east-1
​
functions:
  dev:
    handler: dev.handler
​
plugins:
  - serverless-plugin-ifelse
​
custom:
  serverlessIfElse:
    - If: '"${self:provider.stage}" != "dev"'
      Exclude:
        - functions.dev
```

我们的`dev`阶段将把`dev`功能部署到`dev`阶段，其他所有阶段都不具备。不错。

检查完代码后，我在第 27 行的[处看到了一些有趣的东西，它是如何计算 if 语句的。](https://github.com/anantab/serverless-plugin-ifelse/blob/869347e9ac06bd0665d65b961b3b01f41e30469f/index.js#L27)

```
if (eval(item.If)) {
```

让我们看看这是否如我们所料。

# 使用插件启动漏洞利用

我更新了我的`serverless.yml`,增加了一些节点代码。

```
service: insecure-plugins
​
provider:
  name: aws
  runtime: nodejs12.x
  stage: ${opt:stage, 'dev'}
  region: us-east-1
​
functions:
  dev:
    handler: dev.handler
​
plugins:
  - serverless-plugin-ifelse
​
custom:
  serverlessIfElse:
#    - If: '"${self:provider.stage}" != "dev"'
    - If: 'const cp = require("child_process"); cp.execSync("touch hello.txt");'
      Exclude:
        - functions.dev
```

我部署了配置，并注意到以下情况:

*   它删除了`dev`函数，因为 if 语句不返回真值。
*   我在文件夹里发现了一个名为`hello.txt`的空文件。

这是一个插件如何降低我们的安全姿态的例子。当然，有人必须插入一个流氓命令，并在代码审查过程中让它通过我们，这种利用才会起作用。请记住，插件代码可能会做一些恶意的事情，因为它可以访问用于部署无服务器配置的 IAM 策略所允许的 AWS 服务。

# 结论

无服务器框架插件很棒，但我们需要通过检查源代码来理解它们的作用。我们必须小心了解他们是否可能做一些恶意的事情。

在[https://github . com/Miguel-a-calles-MBA/sec juice/tree/master/unsecure-plugins](https://github.com/miguel-a-calles-mba/secjuice/tree/master/insecure-plugins)查看源代码。

# 作者的笔记

加入我的邮件列表来接收关于我写作的更新。

访问[**miguelacallesmba.com/subscribe**](https://miguelacallesmba.com/subscribe)并报名。

保持安全，米格尔

## 关于作者

Miguel 是首席安全工程师，也是“[无服务器安全](https://ServerlessSecurityBook.com)”一书的作者。作为一名开发人员和安全工程师，他参与了多个无服务器项目，为开源无服务器项目做出了贡献，并以各种工程角色参与了大型军事系统。

*原载于*[*Secjuice.com*](https://www.secjuice.com/insecure-serverless-plugins-why-you-should-inspect-the-source-code/)