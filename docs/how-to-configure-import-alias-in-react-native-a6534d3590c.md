# 如何在 React Native 中配置导入别名

> 原文：<https://javascript.plainenglish.io/how-to-configure-import-alias-in-react-native-a6534d3590c?source=collection_archive---------7----------------------->

![](img/39ed7b7f58cc65b2af4bc9ee484c01f5.png)

How to configure import alias in React Native cover image

导入别名对于维护和可读性更好。了解如何在 React Native 中设置它们！

看看这两个例子:

```
1\. import { InputArea } from '~components/InputArea'
2\. import { InputArea } from '../../../../../components/InputArea'
```

我们将学习如何设置我们的环境，让第一个变体工作。

## “src”文件夹的别名

对于本教程，我假设我们有一个标准的 React 原生文件结构。我们希望为“src”文件夹中的目录创建别名。

```
├── App.js
├── __tests__
├── android
├── app.json
├── babel.config.js
├── index.js
├── ios
├── metro.config.js
├── node_modules
├── package.json
├── src
│ ├── components
│ └── helpers
└── yarn.lock
```

## 为什么波浪号前缀` ~ `很重要？

这个自定义前缀有助于区分您的本地导入包和第三方包。一看就知道哪些导入来自项目。

以下是“助手”文件夹的两个示例:

```
1\. import something from ‘helpers’ // — without prefix
2\. import something from ‘~helpers’ // — with prefix
```

国家预防机制注册表中有一个名为“帮助者”的包。如果您决定在没有任何前缀的情况下命名您的“helpers”文件夹，那么您将面临命名冲突的风险。

我决定坚持使用` ~ `，因为我还没有见过使用它的第三方软件包。还有其他流行的前缀——我的建议是坚持使用波浪号。*

## 安装 Babel 插件

首先，我们要为巴别塔编译器添加一个合适的插件。

```
▶ yarn add — dev babel-plugin-module-resolver
```

## 调整 Babel 配置

在“babel.config.js”中添加“插件”部分。如果它已经存在，只需添加“模块解析器”配置，如下所示。如果你没有这份文件。然后检查“. babelrc”或创建一个。所有可能的配置文件都列在[文档](https://babeljs.io/docs/en/config-files)中。

```
module.exports = {
 // ... some other config
  plugins: [
   // ... some other plugins
    [
      'module-resolver',
      {
        root: ['./'],
        alias: {
          /**
           * Regular expression is used to match all files inside `./src` directory and map each `.src/folder/[..]` to `~folder/[..]` path
           */
          '^~(.+)': './src/\\1',
        },
        extensions: [
          '.ios.js',
          '.android.js',
          '.js',
          '.jsx',
          '.json',
          '.tsx',
          '.ts',
          '.native.js',
        ],
      },
    ],
  ],
};
```

选项如下所述:

1.root——根目录的字符串或数组，
2。别名——别名图，
3。扩展名—解析程序中使用的文件扩展名数组。

## 作为别名的正则表达式

为了防止单独添加每个“src”子文件夹，我们希望使用正则表达式来完成路径。你可以在[babel-plugin-module-resolver Github 页面](https://github.com/tleunen/babel-plugin-module-resolver/blob/master/DOCS.md#regular-expressions)看到关于使用正则表达式的文档。

## 重启 metro 流程

让它工作的最后一步是重启 *metro* 服务器。只需在项目的终端中使用“CTRL + C ”,然后再次使用“yarn start”。

如果有些东西不工作，也许你必须清除缓存-使用“纱线开始-重置-缓存”命令。

## 如何让 VSCode 别名自动完成工作？

有了上面的配置，代码将按预期编译和工作。现在，我们希望让自动完成功能使用我们新创建的别名(或者由 Visual Studio 代码创建者命名的 *IntelliSense* )。

我们必须输入“jsconfig.json”文件(如果它不起作用，就创建它)。

```
{
 “compilerOptions”: {
 “baseUrl”: “.”,
 “paths”: {
 “~*”: [“src/*”]
 }
 },
 “exclude”: [“node_modules”]
}
```

在“jsconfig.json”中，我们必须指定两个选项:“baseUrl”和“paths”对象。这里，我们再次使用一种正则表达式在一行中匹配所有子目录。

## 类型脚本支持

有趣的是，在 TypeScript 项目中，我不得不使配置稍有不同以使其工作:

```
{
 “compilerOptions”: {
 “baseUrl”: “.”,
 “paths”: {“~*”: [“./src/*”]}, 
 },
 “exclude”: [“node_modules”]
}
```

请注意“src”路径前面的点。我不知道为什么需要这样的改变。也许你知道些什么？让我知道！

您还可以在[官方文档中检查 config，以获得 TypeScript 别名](https://reactnative.dev/docs/typescript#using-custom-path-aliases-with-typescript)。

## 在 VSCode 中重新启动 TypeScript 进程

使用新别名的自动完成应该会立即生效。如果它不起作用，也许您必须重新启动 TypeScript 服务器(即使对于像这样的纯 JavaScript 项目，服务器也负责自动完成)。

为此，请打开命令面板并键入“重新启动 TS 服务器”。

## 感谢阅读

👉[在我的推特上查看 React Native 的最新提示](http://twitter.com/Koprowski_it)

👉[在我的时事通讯✉️上关注新的教程](https://koprowski.it/subscribe)

*最初发布于*[*https://koprowski . it*](https://koprowski.it/import-alias-in-react-native-and-vscode/)*。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)