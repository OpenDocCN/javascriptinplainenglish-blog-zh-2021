# 如何用 JavaScript 自动重命名文件

> 原文：<https://javascript.plainenglish.io/how-to-auto-rename-files-with-javascript-a72f4b6f2528?source=collection_archive---------5----------------------->

## 了解如何用 JavaScript 重命名文件

![](img/15af8125a021ebdf5f21fa5a59f45ad7.png)

Photo by [Christopher Robin Ebbinghaus](https://unsplash.com/@cebbinghaus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

当你想自动化一些你不得不反复做的事情时，JavaScript 是非常强大的。自动化工作也帮助我们在那些我们宁愿花很多时间去做的事情上节省时间。

我们将看看如何通过在终端上提供一个参数来实现文件重命名过程的自动化，JavaScript 将很快自动完成这项工作。

假设我们有几个文件，比如说几万个，我们想重命名它们，比如说，文件名以一个名字或 ID 开始，这取决于我们的偏好。手动操作会花费很多时间。

为什么现在要自动完成这项工作，让 JavaScript 在几秒钟内为我们完成呢？

## **设置流程**

我们将利用 NodeJS 的能力，让我们在节点运行时运行 JavaScript 文件。创建一个文件夹，在文件夹里面，给它一个文件名叫做 ***index.js*** 。在这个文件中，我们将使用 JavaScript 创建应用程序逻辑。

现在，您可以在根项目文件夹中重命名一些文件，以便我们更容易看到发生了什么，并帮助我们更有效地引用这些文件。

在 index.js 文件中，我们需要从 NodeJS 导入一个名为 fs 模块的模块。要了解更多关于这个模块的信息，请查看这个 [***链接。***](https://nodejs.org/api/fs.html)

这个模块将帮助我们从不同的路径加载和处理文件。我们还需要各种正则表达式来帮助我们识别给定文件名中的字母和数字。

我们还需要一个 filetype 正则表达式来识别文件的文件类型。为了确保用户从终端自动重命名文件，我们需要获取用户在终端上提供的参数。

我们将使用 Node 的 ***process.argv*** 来解析参数，这样我们就可以捕获来自用户的参数。

请记住，它将参数返回到一个数组中，因此为了捕捉为重命名提供的参数，我们需要将数组中的第三个参数定位为***process . argv[2]***

我们的目标是数组中的第三个元素，因为我们的终端命令将采用“node index.js name/id”的形式。

要阅读更多关于解析参数的内容，请查看这个 [***链接。***](https://nodejs.org/en/knowledge/command-line/how-to-parse-command-line-arguments/)

最后，我们的代码应该采用这种方法。

现在要运行自动重命名文件，您需要运行命令 node index.js name 或 node index.js ID，这取决于您希望如何重命名给定的文件。

请记住，此过程假设您的文件在文件名中有一个名称和 id 链接在一起。

## **结论**

JavaScript 可以用来自动化我们每天做的、会占用我们大量时间的事情。

感谢您抽出时间，祝您编码愉快。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)