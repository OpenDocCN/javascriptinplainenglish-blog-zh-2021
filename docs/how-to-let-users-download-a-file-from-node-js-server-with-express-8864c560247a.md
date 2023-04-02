# 如何让用户用 Express 从 Node.js 服务器下载一个文件？

> 原文：<https://javascript.plainenglish.io/how-to-let-users-download-a-file-from-node-js-server-with-express-8864c560247a?source=collection_archive---------12----------------------->

![](img/3a25cc484d86b94472e9e4c029cd2689.png)

Photo by [Karim MANJRA](https://unsplash.com/@karim_manjra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望让用户在我们的 Express 应用程序中下载文件。

在这篇文章中，我们将看看如何让用户从 Express 应用程序下载文件。

# res .下载

让用户从 Node.js 服务器下载文件的一种方法是使用 Express 提供的`res.download`方法。

例如，我们可以写:

```
const express = require('express')
const app = express()
const port = 3000app.get('/', (req, res) => {
  res.send('Hello World!')
})app.get('/download', (req, res) => {
  const file = `${__dirname}/download/foo.txt`;
  res.download(file);
});app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

我们只是用字符串变量`file`指定文件的路径。

然后我们将它传递给`res.download`方法来下载文件。

`__dirname`是快递 app 的当前工作目录。

# 将文件作为静态文件

我们还可以使用`express.static`中间件将服务器中的一个文件夹作为静态文件夹。

为此，我们写道:

```
const express = require('express')
const app = express()
const port = 3000
app.use('/download', express.static('download'))app.get('/', (req, res) => {
  res.send('Hello World!')
})app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

我们调用`app.use`来使用 Express 静态中间件。

第一个参数是用户用来访问静态文件夹内容的路径。

第二个理由是快速静态中间件。

我们通过用文件夹路径字符串调用`express.static`来创建中间件。

因此，我们将服务器中的`download`文件夹作为静态文件夹。

# 资源附件

我们还可以用`route.attachment`方法在我们的路由中返回一个文件作为响应。

它采用与`res.download`方法相同的参数。

它将`Content-Disposition`响应头设置为`attachment`。

它还根据正在下载的文件类型设置`Content-Type`响应头。

例如，我们可以写:

```
const express = require('express')
const app = express()
const port = 3000
app.get('/', (req, res) => {
  res.send('Hello World!')
})app.get('/download', (req, res) => {
  const file = `${__dirname}/download/foo.txt`;
  res.attachment(file).send();
});app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
})
```

我们用`send`调用`res.attachment`向用户发送文件下载响应。

# 结论

我们可以使用多种方式让用户通过 Express 端点将文件下载到他们(用户的)设备上。

*更多内容看* [***说白了. io***](http://plainenglish.io/)