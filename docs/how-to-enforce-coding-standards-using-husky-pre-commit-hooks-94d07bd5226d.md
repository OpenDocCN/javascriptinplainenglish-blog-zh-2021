# 如何使用 Husky 预提交挂钩实施编码标准

> 原文：<https://javascript.plainenglish.io/how-to-enforce-coding-standards-using-husky-pre-commit-hooks-94d07bd5226d?source=collection_archive---------14----------------------->

![](img/ab72cb6fc83f49e8e7a86a82f622c478.png)

随着应用程序的扩展，保持一致性和执行编码标准变得非常重要。自动化过程以确保质量标准并使应用程序可维护变得很重要。ESLint 和 Prettier 可以用来定义这些标准，但是我们也需要一个工具来执行它们。Husky 通过提供可根据我们的需求进行配置的预提交 git 挂钩来提供该功能。

这些标准也可以通过在 CI 级别对 pull 请求使用门控检查来实施，但是 Husky 是在本地机器级别实施的替代方法。

# 什么是哈士奇？

Husky 是一个 npm 包，使管理 Git 挂钩变得容易。当用 Git 初始化时，它启用了一个称为钩子的特性(如果您想知道，与 react 钩子没有关联)。

它提供了预推送、预重定基、预提交和其他类似的挂钩。这些钩子允许一种机制在 git 命令运行之前执行一个动作。

要查看项目中所有挂钩的列表，我们可以运行:

```
ls .git/hooks
```

所有 git 挂钩及其用法的列表可以在这里找到。

出于我们的目的，我们需要在有人创建提交之前运行 linter 和 formatter。所以我们将使用预提交 git 挂钩。

哈斯基确保:

*   钩子在机器之间共享(使用 package.json 中的配置安装)
*   挂钩是在本地开发人员的机器上创建的
*   钩子在 git 命令执行时运行(在它执行之前)
*   如果不满足标准，则实施检查以使 git 命令执行失败

# 安装和配置 Husky

我们使用以下命令安装 husky:

```
npm i -D husky
```

配置 husky 需要向项目包的根目录添加一个 husky 键。json:

```
"husky": {
  "hooks": {
    "pre-commit": "",  // pre-commit command
    "pre-push": "",    // pre-push command
    "...": "..."
  }
}
```

这些命令可以是我们希望在相应的 git 操作之前运行的任何命令。

如果我们有 npm 脚本运行更漂亮，ESLint 设置为:

```
"scripts": {
    "prettier": "prettier --config .prettierrc 'src/**/*.{js,jsx,css}' --write",
    "lint": "eslint . --ext .js",
    ...
  },
```

我们可以将 husky 配置为在提交发生之前运行这些功能:

```
"husky": {
    "hooks": {
      "pre-commit": "npm run prettier && npm run lint"
    }
  }
```

这确保了在没有格式化代码的情况下无法进行提交，并强制执行使用 ESLint 设置的编码标准。

**注意:**不是在整个项目上运行林挺，而是检查包 [lint-staged](https://github.com/okonet/lint-staged) ，它只在 staged 文件上运行 linter。这减少了对项目进行 lint 处理所需的时间。

使用 husky 和 git 预提交挂钩，我们可以在没有任何手动干预的情况下跨项目实施编码标准。如果你有任何问题或其他林挺小贴士，请在下面的评论中告诉我们。

*原载于 2021 年 6 月 5 日 https://www.wisdomgeek.com**[*。*](https://www.wisdomgeek.com/development/web-development/javascript/enforcing-coding-standards-husky-pre-commit-hooks/)*

**更多内容看*[***plain English . io***](http://plainenglish.io/)*