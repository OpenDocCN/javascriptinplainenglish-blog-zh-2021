# 在 Next.js 中使用环境变量

> 原文：<https://javascript.plainenglish.io/using-environment-variables-in-nextjs-22b99b6ee39e?source=collection_archive---------5----------------------->

## 保管好你的钥匙。

![](img/4caee147dde2465fbdec90ea7763abc9.png)

Photo by [Franck](https://unsplash.com/@franckinjapan?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/safe?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

如今，环境变量无处不在。像 [dotenv](https://www.npmjs.com/package/dotenv) 这样的库有助于实现相同的功能，而更大的框架如 Next.js 实现了它们自己的 dotenv 版本。

一个`.env`文件是一个在你自己的系统上使用的文件，它包含进行 API 调用的键、数据库连接字符串等等。但是，出于显而易见的原因，您应该保持这些文件的安全，这一点很重要。

大多数时候，框架以大致相同的方式实现环境变量。因此，阅读本文对于理解您可以在其他项目中使用的相同原则仍然是有用的。

# 装置

[下一个](https://nextjs.org/docs/getting-started)。js 是一个使用 React 进行模板化来构建 web 应用程序的简单框架。它有更多的功能，如路由，我今天不会进入。

在你的控制台中，运行`npm init`和`npm i next react react-dom`通过节点包管理器安装 Next.js、React 和 ReactDOM。

在您的`package.json`中添加以下脚本:

```
"scripts": {  
  "dev": "next dev",
  "build": "next build",
  "start": "next start"
}
```

接下来，我们需要添加一个带有`index.js`的`/pages/`目录。

index.js

在您的终端中运行`npm run dev`，转到`localhost:3000`并检查页面是否显示。

# 。环境文件

对于我们的环境变量，我们将使用`env`文件扩展名。我们还将在文件前面加上一个点，使它们“隐藏”。

理论上，一个项目只能包含一个`.env`或`.env.development`文件，但是如果项目足够大，并且有多个开发人员在开发，那么通过添加一个`.local.env`文件来分隔可能无法在其他系统上工作的不同变量通常是一个好主意。这个文件应该添加到`.gitignore`中，并且应该只在您的本地系统上工作。

接下来增加了仅使用`.env`为*所有*环境添加文件、使用`.env.development`的开发环境或使用`.env.production`的生产环境文件的可能性。`.env.local`也是一个应该只在本地使用的默认文件。

让我们在项目根目录下创建一个名为`.env`的文件。

我们在`HOST`字段中使用了一个变量来展示这种可能性。

# 使用环境变量

Next.js 推荐的检索环境变量的方法是使用`[.getStaticProps](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation)`。

在你的文件中创建这个函数后，你可以使用`props`参数，这个参数可以给 React 页面，这个页面现在将包含`host`、`port`和`hostname`变量。

您的完整的`index.js`文件现在看起来像这样。

我们将`HomePage`导出为 React 功能的默认变量，并将`getStaticProps`导出为 Next.js。这些属性将被翻译，该页面现在将在屏幕上显示我们的`props.host`环境变量。

![](img/ba021bbaecd796fb62e457fad14d999c.png)

Image showing the environment variable

当然，你不应该给用户看，但是我们可以验证它是否工作。

# 结论

如果你想了解更多关于使用环境变量的知识，你可以在这里阅读官方文档。

我认为在 Next.js 中使用环境变量非常简单。文档很容易理解，并且您想要的所有功能都可以获得，无需安装任何额外的库。

非常感谢您的阅读，祝您有美好的一天。