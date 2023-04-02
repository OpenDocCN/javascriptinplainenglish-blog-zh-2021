# 如何使用 Yarn 工作空间设置 Lerna

> 原文：<https://javascript.plainenglish.io/how-to-set-up-lerna-with-yarn-workspaces-63ac0a505234?source=collection_archive---------4----------------------->

![](img/59ed763f0f5fc80091ceb43f9c4fa2ba.png)

Lerna and Yarn

这篇文章讲述了如何使用[纱线工作空间](https://classic.yarnpkg.com/en/docs/workspaces/)来设置 [Lerna](https://lerna.js.org/) monorepo。

# 莱尔纳

用`[lerna init](https://github.com/lerna/lerna/tree/main/libs/commands/init#readme)`创建一个新的 Lerna monorepo:

```
$ npx lerna init
```

初始化的 Lerna 文件应该如下所示:

```
$ tree
.
├── lerna.json
├── package.json
└── packages1 directory, 2 files
```

*可选*:启用`lerna.json`中的[独立版本模式](https://github.com/lerna/lerna#independent-mode):

# 故事

在`[package.json](https://classic.yarnpkg.com/en/docs/workspaces/#toc-how-to-use-it)`启用纱线工作空间:

然后在`[lerna.json](https://github.com/lerna/lerna#lernajson)`上加上`npmClient`和`useWorkspaces`:

现在当您运行`yarn install`时，Lerna[bootstrap](https://github.com/lerna/lerna/tree/main/libs/commands/bootstrap#readme)和[将](https://github.com/lerna/lerna/blob/main/doc/hoist.md#readme)节点模块提升到项目根目录:

```
$ yarn
```

这意味着跨包共享的`devDependencies`可以保存到项目根`package.json`:

```
$ yarn add --dev eslint -W
```

# 资源

查看范例库 [lerna-template](https://github.com/remarkablemark/lerna-template) 。

[*本文原载于《remarkablemark.org》2021 年 9 月 18 日。*](https://b.remarkabl.org/3Cpop8J)