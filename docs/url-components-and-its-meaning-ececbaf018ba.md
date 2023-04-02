# 什么是 URL？

> 原文：<https://javascript.plainenglish.io/url-components-and-its-meaning-ececbaf018ba?source=collection_archive---------11----------------------->

## URL 由什么组成，它的组成部分是什么，它们的含义是什么？

![As](img/a31dd58eb32eae63c3d82e41e6cb2205.png) 作为 一个 web 开发者，了解 URL 的不同部分及其功能是很重要的。但是，即使对于“普通”的互联网用户来说，知道哪个部分负责哪个任务也是有帮助的。

这只是我们发表的许多文章中的一篇。检查我的个人资料，你会看到，我们是一个开发人员的小团队。我们每周发布多次。关注并订阅我们，以免错过任何关于 JavaScript 和软件开发的精彩内容。

![](img/29ded5cd78d58abc900fe648ba8baf9a.png)

Photo by [Steve Johnson](https://unsplash.com/@steve_j?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

浏览网页时，你不可避免地会碰到浏览器的地址栏和其中的地址。一个例子是:

[http://foo.com:80/some-link](http://foo.com/some-link)/

您在上面看到的地址称为 URL(统一资源定位器)。有了这个网址，你可以访问互联网上的某些资源。它的广义结构是这样的:

<url-scheme>:// <host-name>: <port-number>/ <url-path>？ <query-string>#<fragment></fragment></query-string></url-path></port-number></host-name></url-scheme>

首先有了 **URL 方案**(在我们的例子中是“http”)。它描述了如何访问手边的资源。这里它告诉浏览器使用超文本传输协议。://之后的所有内容都将特定于协议，例如 ftp(文件传输协议)、mailto(代表电子邮件地址)等。在这种情况下，我们将专注于 http。

之后是**主机名**(在我们的例子中是“foo.com”)。主机是保存资源的服务器。浏览器将使用 DNS(域名服务)将主机名“翻译”成浏览器可以理解的地址:网络地址。知道了网络地址，浏览器就能够发送对资源的请求。

在极少数情况下，您可以在主机名后面看到端口号**。默认端口号是 80。通常 URL 中会省略默认端口号。只有当服务器监听默认端口号以外的端口号时，才需要它。您通常只需要在测试、调试或开发环境中指定一个不同于默认的端口号。**

接下来是 **URL 路径**(在我们的例子中是:“/some-link/”)。它是主机中指向主机上特定资源的地址。

URL 路径指向的这些资源可以是静态的，例如资源可以是文件(例如“/document.pdf”)、图片(例如“/photo.jpg”)、音乐文件(例如“/music.mp3”)等。然而，资源也可以是动态的。指向/another-resource 的 URL 路径没有引用主机服务器 foo.com 上的真实文件。您可以看到这一点，因为它没有前面静态示例中的文件结尾。在这种情况下，主机服务器上运行着一个应用程序，它接受请求，并使用数据库中的内容动态构建资源。(该应用程序是用 web 技术编写的，它能够通过创建供浏览器显示的 HTML 来响应传入的请求。web 技术可以是 ASP.NET、PHP、Perl、Ruby on Rails 等等。)

在“？”后面的部分被称为**查询(或“查询字符串”)。**它包含请求网站使用或解释的信息。如何指定该查询完全取决于应用程序。但是通常传递的字符串是一个名称-值对，例如:

【http://foo.com】T2？name 1 = value 1&name 2 = value 2

或者

【http://searchengine.com】T4？q = what+I+am+搜索

在这种情况下，搜索引擎搜索名称 q，并使用它的值进行搜索查询。

“#”后面的所有内容都被称为**片段**。与 URL 方案、主机名、URL 路径、端口或查询字符串不同，片段不会发送到服务器。相反，它仅由客户端用来标识资源中的某个部分。典型地，网络浏览器将呈现网站，使得用户将在屏幕的顶部看到网页的顶部元素。使用片段，您可以指定某个部分将显示在屏幕的顶部。

这用于将注意力吸引到元素的特定部分。当人们发布指向维基百科文章的链接时，你可以经常看到这种情况，他们只指向文章的特定部分。客户端(浏览器)将确保片段所标识的部分显示在屏幕的顶部。

![](img/5c7fdb823e2c7f4190f716ff6bed224c.png)

## 结论

你还知道更多的 URL 部分吗？你有什么问题吗？在下面评论，让我知道。

你已经关注或订阅我们了吗？我们每周都会多次发布关于 JavaScript 和软件开发的文章。请确保不要错过我们的任何精彩内容。