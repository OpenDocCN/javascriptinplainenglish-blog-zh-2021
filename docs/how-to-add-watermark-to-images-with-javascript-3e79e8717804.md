# 如何用 JavaScript 给图像添加水印

> 原文：<https://javascript.plainenglish.io/how-to-add-watermark-to-images-with-javascript-3e79e8717804?source=collection_archive---------15----------------------->

## 了解如何用 JavaScript 给图像添加水印

![](img/2305d30c5ce38e5024e313e3d11aa8b2.png)

Photo by [Marek Piwnicki](https://www.pexels.com/@marek-piwnicki-3907296?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/green-leaf-in-close-up-photography-9202372/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

JavaScript 非常强大，使我们能够有效地处理图像和文件。再加上 Node.js，这是一个 JavaScript 运行时环境，我们可以用这种编程语言做一些令人惊叹的事情。

多亏了 JavaScript，我们可以处理图像并操纵它们。在这篇文章中，我们将学习如何操作图像和给图像添加水印。

当我们处理许多图像并想要添加一些自定义水印时，这也很有帮助。我们可以用 JavaScript 全程自动化这个过程。让我们看看我们如何能做到这一点。

## **设置项目**

对于这个项目的必要性，我们不打算从头开始编码。为了不浪费时间，我们将使用一个叫做 jimp 的 JavaScript 包。

“JIMP”是 JavaScript 图像处理程序的首字母缩写。Jimp 是 Node.js 的图像操作库，用 JavaScript 编写。

Jimp 允许我们处理各种图像文件类型，如 **jpgs、png、gif、BMP 和 tiff** 。

**安装 jimp**

Jimp 安装非常简单，我们只需根据您的首选软件包管理器运行下面的命令。

**NPM**

```
npm i jimp
```

**纱线**

```
yarn add jimp
```

现在我们有了 jimp 的相关包和模块，可以在我们的项目中本地使用。

## **在我们的项目中实施 jimp**

Jimp 考虑了承诺的使用，如下面的代码片段所示。

## **对图像应用水印**

假设我们有一个包含相关图像文件类型的文件夹，并且我们想对它们应用水印徽标。手动将徽标应用到图像上将是一项令人生畏的任务，并且会花费大量时间。

我们可以利用 jimp 并编写一些代码来自动完成这个过程。

## **流程自动化**

现在，让我们投入其中，编写一些代码逻辑来为我们自动化这个过程。

首先，我们需要从 NodeJS 导入文件系统模块，以便将相关的图像加载到我们的程序中。

代码片段注释很好地解释了代码将要做什么。

现在在你的终端上，你可以运行 ***节点<文件名>***

## **结论**

Node.js 和 JavaScript 在自动化无聊的东西和那些我们宁愿花很多时间的东西方面非常强大。

感谢您抽出时间，祝您编码愉快。

## **更读**

[](/how-to-auto-rename-files-with-javascript-a72f4b6f2528) [## 如何用 JavaScript 自动重命名文件

### 了解如何用 JavaScript 重命名文件

javascript.plainenglish.io](/how-to-auto-rename-files-with-javascript-a72f4b6f2528) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)