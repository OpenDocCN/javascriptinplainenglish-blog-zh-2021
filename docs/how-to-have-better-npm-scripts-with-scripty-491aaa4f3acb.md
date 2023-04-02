# 如何用 Scripty 制作更好的 NPM 剧本

> 原文：<https://javascript.plainenglish.io/how-to-have-better-npm-scripts-with-scripty-491aaa4f3acb?source=collection_archive---------21----------------------->

## 减轻 npm 脚本复杂性的快速 npm 包。

![](img/7a7b7441d2529392afbbf44b67df7f53.png)

Photo by [Walkator](https://unsplash.com/@walkator?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名 JavaScript 开发人员(无论是后端还是前端)，我们经常依靠`npm scripts`来自动化一些常见的任务，比如启动服务器、构建项目，甚至在某些脚本之前或之后执行任务，比如`postbuild`、`prebuild`等等。

当这些命令像`node index.js`一样简单时，在我们的 **package.json** 中让它们成为一行根本不是问题。当我们需要一个扩展的命令、添加环境变量和连接命令时，真正的问题就开始了:

(示例摘自 [Material UI package.json](https://github.com/mui-org/material-ui/blob/830c18ba71af19bc0370f1eeb902f9f605144a5d/package.json) )

```
{
    "scripts": {
      "proptypes": "cross-env BABEL_ENV=development babel-node --extensions \".tsx,.ts,.js\" ./scripts/generateProptypes.ts",
      "deduplicate": "node scripts/deduplicate.js",
      "benchmark:browser": "yarn workspace benchmark browser",
      "build:codesandbox": "lerna run --parallel --scope \"@material-ui/*\" build",
      "release:version": "lerna version --exact --no-changelog --no-push --no-git-tag-version",
      "release:build": "lerna run --parallel --scope \"@material-ui/*\" build",
      "release:changelog": "node scripts/releaseChangelog",
      "release:publish": "lerna publish from-package --dist-tag next --contents build",
      "release:publish:dry-run": "lerna publish from-package --dist-tag next --contents build --registry=\"http://localhost:4873/\"",
      "release:tag": "node scripts/releaseTag",
      "docs:api": "rimraf ./docs/pages/api-docs && yarn docs:api:build",
      "docs:api:build": "cross-env BABEL_ENV=development __NEXT_EXPORT_TRAILING_SLASH=true babel-node --extensions \".tsx,.ts,.js\" ./docs/scripts/buildApi.ts  ./docs/pages/api-docs ./packages/material-ui-unstyled/src ./packages/material-ui/src ./packages/material-ui-lab/src --apiPagesManifestPath ./docs/src/pagesApi.js",
      "docs:build": "yarn workspace docs build",
      "docs:build-sw": "yarn workspace docs build-sw",
      "docs:build-color-preview": "babel-node scripts/buildColorTypes",
      "docs:deploy": "yarn workspace docs deploy",
      "docs:dev": "yarn workspace docs dev",
      "docs:export": "yarn workspace docs export",
      "docs:icons": "yarn workspace docs icons",
      "docs:size-why": "cross-env DOCS_STATS_ENABLED=true yarn docs:build",
      "docs:start": "yarn workspace docs start",
      //.....
    }
}
```

但是，如果我告诉你可以将这些命令提取到一个单独的文件中，并有一个像这样的`scripts`配置，会怎么样呢:

```
{
    "scripts": {
      "proptypes": "scripty",
      "deduplicate": "scripty",
      "benchmark:browser": "scripty",
      "build:codesandbox": "scripty",
      "release:version": "scripty",
      "release:build": "scripty",
      "release:changelog": "scripty",
      "release:publish": "scripty",
      "release:publish:dry-run": "scripty",
      "release:tag": "scripty",
      "docs:api": "scripty",
      "docs:api:build": "scripty",
      "docs:build": "scripty",
      "docs:build-sw": "scripty",
      "docs:build-color-preview": "scripty",
      "docs:deploy": "scripty",
      "docs:dev": "scripty",
      "docs:export": "scripty",
      "docs:icons": "scripty",
      "docs:size-why": "scripty",
      "docs:start": "scripty",
    }
   //.....
}
```

## 剧本

Scripty 是一个 npm 包，它使我们能够拥有运行`npm scripts`的可执行文件。

整个想法是将这些巨大的脚本行视为代码，并保持我们的 **package.json** 简洁明了。

假设我们有这个:

```
{
  "scripts": {
    "lint": "eslint . --cache --report-unused-disable-directives --ext .js,.ts,.tsx --max-warnings 0"
  }
}
```

使用 scripty，它将看起来像这样:

```
{
  "scripts": {
    "lint": "scripty"
  }
}
```

## 幕后的魔力

当然，我们刚刚删除的命令需要在某个地方。为了简单起见，scripty 做了一个`<npm-script-nam>:<executable-file-name>`的配对。

换句话说，如果我们有一个名为`lint`的 npm 脚本，我们需要一个名为`lint`、`lint.sh`或`lint.js`的可执行文件。

默认文件夹在根级别总是一个名为`scripts`的文件夹。因此，为了解决前面的迁移，我们将在`scripts`文件夹下创建一个名为`lint.sh`的文件，如下所示:

```
#!/usr/bin/env bashyarn eslint . --cache --report-unused-disable-directives --ext .js,.ts,.tsx --max-warnings 0
```

## 可执行 Bash 或。射流研究…

Scripty 只能处理可执行的 bash 或 JavaScript 可执行文件。

要拥有其中之一，该文件需要:

1.  将 shebang 放在文件的顶部(例如`#!/bin/bash`或`#!/bin/node`)；
2.  有执行权限(而`ls -la`需要有`x`标志)；

> 快速提示，如果您在 UNIX 环境中，您可以通过运行命令`chmod u+x <file-path>`快速授予该权限。

此外，文件扩展名不是必需的。你可以写一个`test.sh`、`test.js`或者只写`test`。定义语法高亮和执行的将是我之前提到的 shebang 指令之一。

```
#!/bin/nodeconst fs = require('fs');fs.copyFileSync('static/base.css', 'dist/base.css');
// ...#!/usr/bin/env bashNODE_ENV=productionyarn nest build
```

> *对于 JS 可执行文件，请记住它将由* `*node*` *执行，并且您不能使用无效的 js-node(例如* `*import*` *)语法。*

## 定量

我们经常遇到的另一个需求是运行大量相关的脚本。假设我们有很多`test`脚本，我们想运行所有的脚本，比如`test:*`:

```
{
  "scripts": {
    "test:unit": "jest",
    "test:e2e": "cypress run --ci",
    "test": "npm-run-all test:*",
  }
}
```

使用 scripty，我们可以创建一个名为`test`的子文件夹，并在那里声明这两种类型的测试:

```
.
├── package.json
├── scripts
│   └── test
│       ├── e2e
│       └── unit
└── yarn.lock
```

有了这些带有指令的文件，您可以将 package.json 更改为:

```
{
  "scripts": {
    "test:unit": "scripty",
    "test:e2e": "scripty",
    "test": "scripty",
  }
}
```

> *注意，对于这种情况，只有* `*test*` *脚本就足够了。我们将只保留* `*test:unit*` *和* `*test:e2e*` *，以防我们想要单独运行这些命令中的一个。*

当你运行`test`时，scripty 会知道你有一个名为`test`的文件夹，里面有很多脚本，它会运行所有的脚本。

请记住，这是一个并发调用，您不应该依赖于执行顺序。

## 控制配料顺序

如果您需要它们按照一定的顺序执行，使用与之前相同的 package.json，您需要做的就是在我们的`scripts/test`文件夹中，创建一个名为`index`的脚本，它将负责按照我们想要的顺序执行其他脚本:

```
.
├── package.json
├── scripts
│   └── test
│       ├── index
│       ├── integration
│       └── unit
└── yarn.lock#!/bin/bashscripts/test/unit
scripts/test/integration
```

> 请记住，当前的工作目录(CWD)将总是它被执行的地方，在这个例子中是我们的根文件夹。

## 平行手表

另一个常见的场景是，当我们需要运行某些脚本时，这些脚本会留在`watch mode`中；换句话说，锁定一个分区并一直监听文件的变化，这样它就可以执行某些操作。

```
{
  "scripts": {
    "watch:css": "sass src/scss/main.scss public/css/main.css -s compressed",
    "watch:js": "webpack --config webpack.config.js --watch --mode=development",
  }
}
```

启动这两个命令的方法是打开两个选项卡，并在一个选项卡中运行每个命令。但那很乏味。如果我们能有一个终端标签，同时运行所有的`watch`会怎么样？

要使用 scripty 做到这一点，我们所要做的就是在脚本中创建一个名为`watch`的文件夹，就像我们之前为`test`所做的一样。

```
.
├── package.json
├── scripts
│   └── watch
│       ├── css
│       └── js
└── yarn.lock
```

但是，除了将`scripty`传递给我们的 npm 脚本，我们还必须用`true`指定一个名为`SCRIPTY_PARALELL`的环境变量:

```
{
  "scripts": {
    "watch": "SCRIPTY_PARALLEL=true scripty"
  }
}
```

现在两者都将继续运行。

## 警告

这里最大的警告是针对 Windows 用户的。

如果你是他们中的一员，或者你维护着一个可以在 Windows 机器上运行的项目，你将需要一些特殊的处理，我建议你看看有这些说明的[文档](https://www.npmjs.com/package/scripty#windows-support)。

## 结论

Scripty 允许我们将 npm 脚本视为代码，拥有一个包含执行某些任务的所有指令的文件。

它还简化了回滚不正确的脚本指令的能力，并提供了一个很好的独立的 git 历史。

所以**要有创意！**

## 参考

*   [前端主机— JS 和 TS Monorepo](https://frontendmasters.com/courses/monorepos/)
*   [剧本](https://www.npmjs.com/package/scripty)
*   [MaterialUI Package.json](https://github.com/mui-org/material-ui/blob/830c18ba71af19bc0370f1eeb902f9f605144a5d/package.json)
*   [我的 Monorepo 使用 Scripty](https://github.com/raulfdm/raulmelo-studio)
*   [打包 NPM-运行-全部](https://www.npmjs.com/package/npm-run-all)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)