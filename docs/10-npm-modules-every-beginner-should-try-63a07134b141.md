# 每个初学者都应该尝试的 10 个 Npm 模块

> 原文：<https://javascript.plainenglish.io/10-npm-modules-every-beginner-should-try-63a07134b141?source=collection_archive---------12----------------------->

## 推荐初学者使用的 npm 模块

![](img/90fe6ea8e154943d6b46e3ad7f0770f9.png)

Photo by [Jonathan Sanchez](https://unsplash.com/@jonathansancheziam?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 已经越来越流行了。节点包管理器(NPM)在这里扮演着重要的角色。用它可以将一系列预制模块集成到您自己的应用程序中。

在本文中，我将向您提供最值得推荐的 npm 模块，我自己已经根据需求在各种项目中使用过这些模块。Node.js 的 npm 模块数不胜数，调色板小到辅助功能，大到复杂框架。

# 1.Cuid

针对水平缩放和二分搜索法查找性能优化的防冲突 ids。cuid 模块更像是一个较小的 Node.js 模块。该模块生成无冲突 id，例如，我用它来为不同用户上传的文件添加前缀。

```
$ npm install --save cuid
```

# 2.咖啡脚本

CoffeeScript 是一种编译 JavaScript 的语言。由于语法特别简单，省略了花括号，CoffeeScript 成了我近年来 Node.js 项目中最喜欢的语言。

```
npm install --save-dev coffeescript
```

# 3.PM2 —高级 Node.js 流程管理器

对我来说，PM2 模块已经成为生产环境中不可或缺的一部分。它允许在不停机的情况下简单地重新加载 Node.js 进程，以及对各个进程进行优雅的监控。PM2 有许多有趣的特性，在高效使用 Node.js 时不应该错过。贝宝等公司也使用 PM2。

```
$ npm install pm2 -g
```

# 4.帕格又名。jade——Express 的模板引擎

如果你正在寻找一种轻量级的模板语言。帕格对他很有意见，他不久前还自称杰德。因为多亏了缩进和其他好的特性，Pug 将 HTML 语法减少到了最低限度。
结合 Express，目前对我来说没什么可比性！

```
$ npm install pug
```

# 5.mocha——有趣、简单、灵活的 JavaScript 测试框架

npm Mocha 特别适合 Node.js 下的测试驱动开发，因为它有一个易读、易学的语法。

```
$ npm install --global mocha
```

# 6.节点邮件程序

顾名思义，npm 模块非常适合在 Node.js 应用程序中发送电子邮件。这个模块有许多配置选项，因此它可以很容易地集成到我目前的所有项目中。

```
npm install nodemailer
```

# 7.MongoDB Node.js 驱动程序

对于查询 MongoDB 数据库，这个模块特别合适，因为它提供了查询和操作 MongoDB 的本地接口。

# 8.再见

如果您想在项目中使用 JQuery 选择器在服务器端操作 HTML / XML，npm 模块 Cheerio 是最佳选择。因为它允许服务器端遍历和操纵 HTML / XML。

```
npm install cheerio
```

# 9.sequel ize-node . js ORM 映射器

如果你需要一个关系数据库的 ORM 映射器，你现在还不能使用这个模块。Sequelize 是一个相对简单的关系数据库 ORM 映射器。然而，仔细观察会发现它有非常广泛的特征。这里特别有趣的是后续数据库迁移(改变表格)到网站的可能性

```
$ npm install --save sequelize
```

# 10.Express — Node.js web 应用程序框架

对于我和我的项目来说，Express 目前是创建 web 应用程序的 MVC 框架。因为版本 4……特别是轻量级的，可以快速用于新项目。

```
$ npm install express
```

# 结论

上面的 npm 模块绝对值得一看，对我个人来说，根据需求，不可能想象没有它们的任何项目。