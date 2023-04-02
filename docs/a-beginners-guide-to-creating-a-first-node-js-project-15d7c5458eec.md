# 创建第一个 Node.js 项目的初学者指南

> 原文：<https://javascript.plainenglish.io/a-beginners-guide-to-creating-a-first-node-js-project-15d7c5458eec?source=collection_archive---------18----------------------->

## 创建第一个 Node.js 项目的分步指南

![](img/21ae010c6cb30bfc919f2d6a91a9137b.png)

Photo by [Tim Swaan](https://unsplash.com/@timswaanphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Node.js 是 web 开发人员中的流行工具。它允许开发人员在构建应用程序时使用 JavaScript。如果您希望成为全栈 web 开发人员或后端开发人员，Node.js 是一个可以用来构建应用程序的工具。

大多数大公司，如易贝、GoDaddy、PayPal、优步、雅虎、网飞，都在他们的软件中使用 Node.js。

# **什么是后端开发？**

HTML，CSS，Bootstrap 都是前端开发的一些工具。它们帮助开发人员创建前端应用程序。所以，前端开发与用户在网页上看到的内容有关。例如，网站顶部的图像、页面布局、指向其他网页的链接以及页面上可以看到的所有彩色元素。

相反，后端开发是关于人们在页面上看不到的东西。后端开发者专注于数据库、网站架构、API、服务器、支付流程。

# **如何安装 Node.js？**

首先，你需要去 [Node.js 网站](https://nodejs.org/en/)，下载 LTS 版本。然后，您可以运行安装程序并设置**Node . js。**然后，您可以进入您的命令行界面并编写`node --version`来检查在您的计算机上是否已经成功安装了节点，然后重新启动您的计算机。

# **如何使用 Node.js？**

使用 Node.js，您不需要在浏览器中运行 JavaScript。您可以在命令行中运行 JavaScript 代码。例如，您可以使用 Node.js 如下所示打印`"Hello world"`。首先，在桌面上打开你的终端。然后，应用以下步骤。

```
mkdir nodejsExample
cd nodejsExample
touch index.js
echo 'console.log("Hello World")' > index.js
node.js index.js // will return Hello World on the terminal.
```

上面的例子是 Node.js 最直接的用法。在本地节点模块中有很多用例。

# **使用原生节点模块**

可以使用 Node.js 直接与电脑交互，不需要使用浏览器。您可以使用[本地节点模块](https://nodejs.org/api/all.html)来实现这一点。例如，您可以将一个文本文件复制到另一个文本文件。

要将一个文本文件复制到另一个文本文件，您可以访问上面的链接。然后，您可以找到文件系统部分。在该部分中，有一个名为 copyFileSync()的方法。

您可以按如下方式使用该方法。

```
const fs = require(“fs”);fs.copyFileSync(“file1.txt”, “file2.txt”)
```

上面的脚本将`file1.txt`中写的文字复制到`file2.txt`。注意，你不需要创造`file2.txt`。该方法将自动生成它。

现在，您可以使用命令行运行`file.js`。

# **使用外部节点模块**

您可以在上面的文档中找到要在下一个项目中使用的本地节点模块。它们是内部模块。您还可以安装外部节点模块，以便在下一个项目中使用它们。

你可以使用`npm`、**、**来实现。你可以在这里搜索[包](https://www.npmjs.com/)。

要初始化 npm，您可以在项目目录中打开一个命令行并编写`npm init`。

现在，您可以使用命令行安装包来打印蛇的名字。

`npm install snake-names`

然后，可以使用下面的代码打印假的蛇名。

Gist added by author.

# **结论**

Node.js 是 web 和后端开发人员中流行的工具。您可以使用 Node.js 在命令行上运行 JavaScript 代码。

Node.js 有自己的本地模块可以在项目中使用。也可以使用`npm`(节点包管理器)安装外部节点模块。您可以在您的项目中发现它们的包。

此外，还有非常流行的 npm 包，如 lodash，react，react-dom，chalk，request，express，commander，debug，async。

您可以探索这些包来提高您的 web 开发知识。

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***