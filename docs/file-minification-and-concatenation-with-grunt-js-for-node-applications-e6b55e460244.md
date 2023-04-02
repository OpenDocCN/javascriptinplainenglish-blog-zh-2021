# Node.js 应用程序的文件缩小和连接

> 原文：<https://javascript.plainenglish.io/file-minification-and-concatenation-with-grunt-js-for-node-applications-e6b55e460244?source=collection_archive---------7----------------------->

![](img/16cac240a9ac0c2c1ae4dcc48a208553.png)

在构建 web 应用程序时，性能是一个非常重要的话题。在软件开发领域，理想的情况是，您的 web 应用程序在生产环境中性能良好并经过优化。在应用程序包含大量 JavaScript 和 CSS 文件的情况下，由于文件大小不同，这可能会影响应用程序的加载时间。因此，您的应用程序在低性能方面会滞后。

建议您将尽可能少的文件发送到生产环境，以帮助实现高性能和快速加载。

现在，如果你不知道什么是咕噜声，你就没什么好担心的了。在我们开始使用它之前，我会告诉你它是什么。除此之外，在这篇文章中，我将教你如何:

*   安装 Grunt
*   用 Grunt 缩小 JavaScript 文件
*   用 Grunt 连接文件

# 先决条件

要充分利用本文，您需要具备以下条件:

*   Node.js 的基础知识
*   文本编辑器(例如，VSCode)
*   终端应用程序(例如，命令提示符)

[Grunt](https://gruntjs.com/) 是 Node.js 的任务运行器。当然，你可能想知道任务运行器是做什么的。坚持住！我一会儿就告诉你。

任务执行者为我们执行重复性的任务。这些任务可以是:

*   并非所有需要供应商前缀的浏览器都支持为 CSS 样式添加 CSS 规则前缀。
*   由于浏览器无法理解 SASS 文件，所以将 SASS 文件编译为 CSS 文件。
*   通过压缩 JS 和 CSS 文件来减小它们的大小，使它们在服务器请求时能够更快地加载。
*   最后，将不同的 JavaScript 文件连接成一个 JavaScript 文件，将 CSS 文件连接成一个 CSS 文件等等。

Grunt 提供了很多很多的插件来执行这些任务。每个任务都有不同的插件，取决于哪个适合你。你所要做的就是安装一个特定的插件来完成这个任务。这些插件可能还需要你有额外的库才能工作。grunt 的目标是简单地使您的开发工作流程顺畅。

出于本文的目的，我们将使用 Grunt 缩小 JS 文件，并使用 Grunt 连接文件，因为其他任务不是本文的目的。

创建一个名为`grunt-project`的工作项目目录(文件夹的名称完全由您决定)，并用您的文本编辑器打开它。

# 装置

我假设您的计算机上已经安装了 Node.js。现在，在我们安装 grunt 之前，我们将不得不创建一个`package.json`文件来跟踪我们的 grunt 版本和我们将用来运行我们的任务的所有其他插件。运行以下命令创建一个。

```
npm init -y
```

**全局安装 Grunt】**

```
npm install grunt-cli -g
```

**本地安装 Grunt】**

```
npm install grunt --save-dev
```

在您的项目目录中，创建一个`GruntFile.js`文件。这个文件将包含我们任务的所有配置，并且这个文件将告诉插件在哪里可以找到某些文件。在我们的例子中，JavaScript 和 CSS 文件。然后，加载插件，注册任务。

# 缩小 JavaScript 文件

假设您有一个包含大量代码的 JavaScript 文件，当上传到服务器时，当客户端请求它时，可能需要更长的时间来加载。缩小它可以减小文件大小，并使它在服务器请求时加载得更快。这是格朗特能处理的事。它丑化了它。

grunt 用来缩小文件的插件叫做`contrib-uglify`。这是我们将用来缩小 javascript 文件的插件。运行下面的代码来安装它。

```
npm install grunt-contrib-uglify --save-dev 
```

完成后，将这段代码粘贴到您的`GruntFile.js`文件中。

```
module.exports = function(grunt) //configurationgrunt.initConfig({ uglify: { build: { files: [{ src: 'script/script.js', dest: 'build/script.js' }] } } }); //Load plugins grunt.loadNpmTasks('grunt-contrib-uglify'); //Register Tasks}
```

上面的代码只是告诉丑陋的插件在哪里找到它应该缩小的文件，为它提供一个目的地，告诉插件在哪里存储缩小的文件。在我们的例子中，它将创建一个构建文件夹，并将缩小的 javascript 文件存储在那里。之后，我们加载插件。要运行此任务，请运行以下命令:

```
grunt uglify 
```

成功完成后，您应该会在构建文件夹中看到缩小的 javascript 文件。

# 串联文件

对于有多个 javascript 和 CSS 文件的情况，将它们连接起来是一个很好的做法。grunt 用来连接文件的插件叫做`contrib-concat`。有一吨他们，但这一个特别的工程只是罚款，它是官方维护。运行下面的代码来安装这个插件:

```
npm install grunt-contrib-concat --save-dev
```

现在，您的`GruntFile.js`文件将包含以下代码:

```
module.exports = function(grunt) {//configuration grunt.initConfig({ concat: { js: { src: ['script/*.js'], dest: 'build/scripts.js' }, css: { src: ['styles/*.css'], dest: 'build/styles.css' } }});//Load pluginsgrunt.loadNpmTasks('grunt-contrib-concat');//Register Tasks}
```

上面的代码连接了两个不同的文件，一个是 js 文件，另一个是 CSS 文件。配置只是告诉插件分别进入脚本和样式文件夹，并连接任何。js 或者。css 文件，并将它们存储在不同的目的地。要运行此任务，请运行以下命令:

```
grunt concat
```

成功完成后，您应该在 build 文件夹中看到一个脚本文件和一个样式文件。

# 结论

我希望我已经能够让初学者了解什么是咕噜声。语法非常简单。您也可以使用 grunt 来运行单元测试。grunt 库有非常受欢迎的文档，你可以用 Grunt 做更多的事情。在 grunt 网站上搜索 SASS 关键字，尝试创建一个将 SASS 文件编译为 CSS 文件的任务，然后您将看到可用插件的列表。现在，在安装之前，查看你想使用的每个插件的详细信息是非常重要的。一旦你点击一个特定的插件，它会把你带到 npm 网站，在那里你会找到安装它的代码。有些插件要求你的电脑上有其他的库，所以在你选择之前要阅读手册。

感谢您的阅读和快乐编码！

*更多内容看* [*说白了。报名参加我们的*](http://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*