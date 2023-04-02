# 节点模板化:快速手柄

> 原文：<https://javascript.plainenglish.io/node-templating-handlebars-for-express-edb4e17b15c7?source=collection_archive---------24----------------------->

![](img/e5a89bee7fd78e6b3cd2f375f101d61f.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

参加完一个婚礼后，我对模板这个想法产生了兴趣。当您发送邀请时，除了“收件人:”部分，每个收件人的所有信息都是相同的。你的请柬正文是一样的，但对每个人都有一句问候。动态改变这个问候语的能力就是模板化的一个例子。

新程序员不断被教导要保持代码干爽，意思是“不要重复自己”。更好的代码是动态的和可重用的。有多种方法允许使用模板，但我将讨论一种与 Node 相关的方法，因为这是我最近的博客主题。

Handlebars 是一个流行的模板引擎和 JavaScript 库，可以很好地与 Express 服务器配对。首先，在 NPM 上下载哈佛商学院的软件包。

安装完成后，您需要一行代码来开始。写 app.set("查看引擎"，" hbs ")。这告诉 Express 模板引擎已经安装好，可以使用了。

但是，您将呈现动态页面，而不是通过公共文件夹提供静态文档，动态页面必须位于根文件夹中的“views”目录中。

在这个视图文件夹中，命名文件并以。hbs 扩展，它具有内置的 VSCode 支持。这些文件基本上是 HTML 文档，但它们允许特殊的表达式，并使用 Handlebars 和 Express 呈现。

要使页面在浏览器中可访问，请编写一个 app.get 来建立路由，并将请求和响应作为参数。例如，如果您在视图目录“about.hbs”中创建了一个新文件，您的代码将从 app.get("about "，(req，res) = >开始

与静态页面呈现的区别在于，不是编写 res.send 并提供类似“欢迎使用我的关于页面”的响应，而是使用 res.render，这允许您呈现其中一个模板。您现在可以选择在 Node 中提供值，而不是硬编码到 HTML 文件中。

现在可以使用 Node 将值注入到模板中。在 res.render 中，包含一个对象，该对象包含希望模板显示的值。假设你想给你的页面起一个标题，你可以写

```
res.render(“about”, {title: “Invitations”,event: “Wedding”})
```

在你的“about”文件中，你所需要的是双括号来注入值。您的标记现在可以编写如下:

```
<h1>{{title}}</h1>
<p>We can’t wait to have you at our {{event}}! </p>
```

这个过程让我想起了为 React 编写 JSX 时经常使用的插值。我现在有了一种用 JavaScript 创建动态内容的新方法。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)