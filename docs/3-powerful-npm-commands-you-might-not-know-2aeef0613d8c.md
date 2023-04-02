# 你可能不知道的 3 个强大的 NPM 命令

> 原文：<https://javascript.plainenglish.io/3-powerful-npm-commands-you-might-not-know-2aeef0613d8c?source=collection_archive---------8----------------------->

![](img/742ec1f1c627cb7caee1881b0eee76d4.png)

如今，你很难找到一个以前从未涉足 NPM 的开发商。它的易用性和 npmjs.com 上大量维护良好的软件包使 NPM 几乎不可或缺。尽管 NPM 被广泛使用，但并不是所有的命令和选项都广为人知。一些 NPM 宝石隐藏在表面之下。因此，为了发挥你的全部 NPM 潜力，这里有三个你现在可能已经知道的漂亮的 NPM 命令。

# 1. [npm 文档](https://docs.npmjs.com/cli/v7/commands/npm-docs)

此命令允许您在 web 浏览器中打开包的文档。只需键入命令，后跟包名，您的默认浏览器就会立即打开文档。

```
npm docs <package-name>
```

不喜欢浏览器弹出来只想看网址？别担心。将浏览器配置设置为 false 将在终端中返回一个 URL。

```
npm docs <package-name> --browser false
```

# 2. [npm 修剪](https://docs.npmjs.com/cli/v7/commands/npm-prune)

你曾经使用过`npm uninstall`来移除包吗？还是把他们从`package.json`上撤下来，跑去`npm install`收拾你的`node_modules`？Npm 修剪会让你的生活轻松很多。该命令清除`package.json`中没有引用的`node_module`的所有包。所以只要清理你的`package.json`，运行`npm prune`，你的模块就都整理好了。

# 3. [npm 重复数据删除](https://docs.npmjs.com/cli/v6/commands/npm-dedupe)

该命令在您的包树中找到重复的包，并将它们上移以防止重复。假设您有两个具有相同依赖关系的包。

```
- package A
  - dependency C
- package B
  - dependency C
```

依赖项 C 安装了两次，膨胀了你的`node_modules`。NPM 重复数据消除将把`dependency C`移到树的上方，在那里它可以被程序包 A 和 b 利用

```
- package A
- package B
- dependency C
```

*更多内容请看*[***plain English . io***](http://plainenglish.io/)