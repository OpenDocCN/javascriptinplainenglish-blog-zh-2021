# 如何理解 Express 中的基本路线

> 原文：<https://javascript.plainenglish.io/understanding-basic-routes-in-express-js-9fa30d1a5188?source=collection_archive---------8----------------------->

## 更好的路由总是让你的用户更容易访问你的 web 应用。

![](img/76b38f1417211a958231ffa0d9073425.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@jstrippa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在过去的几年里，Node.js 在开发人员中变得越来越流行。尤其是当你擅长 JavaScript 的时候，因为有了 **Node.js** ，你就不用再学习任何其他特定的语言进行后端开发了。虽然有内置软件包，但它也支持第三方软件包。

**Express** 是一个旨在轻松创建节点网站的框架。

# 设置 Express

您可以通过运行下面的命令来安装 Express。完成后，检查您的 **package.json** 文件，确保它是否成功完成。

```
$ npm install express
```

好了，现在您的节点应用程序中有了一个 **Express** 框架。让我们将 **Express** 导入到我们的应用程序中，并为本教程创建一个简单的节点服务器。在 Node 中，您可以通过下面的命令导入 Express。

```
const express = require('express');
```

然后需要通过调用导入的 Express 函数来设置 Express app。为此，请使用下面的命令。

```
const app = express();
```

接下来，你需要为你的网站设计网页，你的网站可以是静态网站，也可以是动态网站。为了理解 Express 中的基本路由，我在本教程中使用了一个静态节点网站，向用户显示信息。

让我们在应用程序中创建一个名为 docs 的文件夹来存储我们的 web 页面。

这里，我将为这个应用程序选择像`index.html`、`about.html`、`contact.html`这样的基本页面。

您可以在 docs 文件夹中创建这些 HTML 页面，并为您的 web 页面添加一些内容和相关样式。

让我们为我们的应用程序定义端口并调用 **listen** 方法。

```
// defining the portconst port = 3000; // invoke listen methodapp.listen(port, () => {
   console.log(`app listening for requests on port ${port}`);
});
```

# 添加基本路线

第一条路线应该是到我们的主页，它是在 **docs 文件夹**中的`index.html`。让我们先创建它。

```
app.get('/', (req, res) => {
   res.sendFile('./docs/index.html', { root: __dirname });
}); // inside this function you don't need to set either header or status code, but make sure to specify the root directory.
```

好的，然后我们可以为剩下的网页添加其他路线。我们可以这样做。

```
// about.htmlapp.get('/about', (req, res) => {
  res.sendFile('./docs/about.html', { root: __dirname });
});// contact.htmlapp.get('/contact', (req, res) => {
  res.sendFile('./docs/contact.html', { root: __dirname );
});
```

好了，现在我们差不多完成了，打开你的浏览器，然后去 **localhost:3000** 看看你的 index.html 页面是否加载了。这是你的`‘/’`路线，同样，也检查`localhost:3000/about`和`localhost:3000/contact`网址。

如果您的路由工作正常，您将能够在浏览器中看到响应。

# 添加重定向& 404 页面

如果用户在 URL 的末尾输入`/about-us`而不是`/about`，希望看到你网站上的“关于”页面，会发生什么？他/她会得到特定的页面吗？当然不是。那我们怎么把这样的案例引导到相关页面呢？

接下来**将**重定向到图片中，并且当你的用户点击了一个没有目的地的错误 URL 时，你需要添加一个 **404 错误页面**来表明用户访问了一个错误的目的地，而这个目的地在你的网站中是不可用的。

是时候给我们的网站添加**重定向**和一个 **404 页面**了。

```
// user trying to reach /about-us pageapp.get('/about-us', (req, res) => {
  res.redirect('/about');
}); // when a user hit the localhost:3000/about-us, this will automatically redirect the user to the *localhost:3000/about* page.// 404 page - here, you need to create another HTML file called 404.html inside the docs folder and add some content like the 404 error page to indicate the user, the destination tried to reach is unavailable. app.use((req, res) => {
  res.status(404).sendFile('./docs/404.html', { root: __dirname });
});
```

***注意:*** *确保将 404 页面* `*(app.use() function)*` *添加到代码的底部，因为它会响应服务器收到的每个请求，包括****GET****和****POST****。如果你把它贴在通常路线上面的某个地方，你将不会在它下面得到任何回应。*

让我们通过访问`localhost:3000/about-us`和一个在你的网站上不存在的目的地比如`localhost:3000/store`来试试上面的重定向和 404 页面

在第一种情况下，如果您被重定向到**/关于**页面而没有引起任何错误，那么您已经正确地进行了重定向。此外，当你试图到达你的网站上不存在的某个地方时，你在浏览器中得到 404 错误页面作为响应，那么你已经做了所有正确的事情。

如果你需要完整的代码，可以在下面找到。

# 结论

**恭喜你！**您已经向使用 Express 框架构建的节点网站添加了基本路由。

感谢您的阅读！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区*](https://discord.gg/GtDtUAvyhW) *获得独家写作机会和建议。*