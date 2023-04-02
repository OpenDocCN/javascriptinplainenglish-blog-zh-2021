# 如何 lint Git 提交消息

> 原文：<https://javascript.plainenglish.io/how-to-lint-git-commit-messages-5864dc695d75?source=collection_archive---------9----------------------->

![](img/8c7ed4cd0ce1970e1478247ee1ea22bb.png)

[commitlint](https://b.remarkabl.org/commitlint)

这篇文章讲述了如何用[commit list](https://b.remarkabl.org/commitlint)和[husky](https://b.remarkabl.org/husky)lint Git commit 消息(参见[演示库](https://b.remarkabl.org/3qIwXlU))。

# 先决条件

*   [Node.js](https://b.remarkabl.org/nodejs-site)

# 哈士奇 5 号

观看 [YouTube 视频](https://youtu.be/2J9VnYiZ_Ts?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ):

用配置文件安装`[commitlint](https://www.npmjs.com/package/commitlint)`:

```
npm install @commitlint/{cli,config-conventional}
```

> 这个命令同时安装`[@commitlint/cli](https://www.npmjs.com/package/@commitlint/cli)`和`[@commitlint/config-conventional](https://www.npmjs.com/package/@commitlint/config-conventional)`。

[配置-常规](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)是基于[角度常规](https://github.com/angular/angular/blob/22b96b9/CONTRIBUTING.md#-commit-message-guidelines)的[标准](https://www.conventionalcommits.org/)。

创建`.commitlintrc.json`，它扩展了[配置-常规](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)的规则:

或者导出`commitlint.config.js`中的规则:

安装`[husky](https://www.npmjs.com/package/husky)`:

```
npm install husky
```

启用 [Git 挂钩](https://git-scm.com/docs/githooks):

```
npx husky install
```

或者给`package.json`添加`postinstall`脚本，在`npm install`之后启用 Git 挂钩:

> 假设包是私有的。如果这个包是 **public** ，那么确保使用`[pinst](https://github.com/typicode/pinst)`禁用`postinstall`脚本。更多信息见[哈士奇文件](https://typicode.github.io/husky/#/?id=install)。

添加`commit-msg`钩:

```
npx husky add .husky/commit-msg 'npx commitlint --edit $1'
```

> 确保使用单引号而不是双引号，以便正确添加`$1`。

提交并验证消息是否遵循[常规提交](https://www.conventionalcommits.org/):

# 哈士奇 4 号

用配置文件安装`commitlint`:

```
npm install @commitlint/{cli,config-conventional}
```

创建`.commitlintrc.json`，它扩展了[配置-常规](https://github.com/conventional-changelog/commitlint/tree/master/%40commitlint/config-conventional)的规则:

或者导出`commitlint.config.js`中的规则:

安装`husky@4`，设置[挂钩](https://git-scm.com/docs/githooks):

```
npm install husky@4
```

创建`.huskyrc`(或`.huskyrc.json`)并添加运行`commitlint`的 Git `commit-msg`钩子:

或者给`package.json`加上挂钩:

测试提交挂钩是否有效:

[*本文原载于 2019 年 5 月 29 日《remarkablemark.org》。*](https://b.remarkabl.org/3u0Vdlc)