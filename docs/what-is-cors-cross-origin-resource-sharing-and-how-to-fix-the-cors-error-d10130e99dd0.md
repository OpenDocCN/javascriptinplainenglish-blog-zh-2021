# 什么是 CORS(跨源资源共享),如何修复 CORS 错误？

> 原文：<https://javascript.plainenglish.io/what-is-cors-cross-origin-resource-sharing-and-how-to-fix-the-cors-error-d10130e99dd0?source=collection_archive---------4----------------------->

## 最后，摆脱 CORS 错误。

![](img/18144a492d3100cfc8859dab5beb0a80.png)

Photo by [Elisa Ventur](https://unsplash.com/@elisa_ventur?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 什么是同源政策和 CORS？

跨源资源共享是一种机制，允许一个 URL 上的网站从另一个 URL 请求数据。例如，您试图从一个 API 获取数据，而应用程序失败了，并在控制台中显示一个 cors 错误。这是因为浏览器实现了*同源策略*。该策略允许客户端从自己的 URL 自由请求数据，但阻止来自不同 URL 的任何内容，除非满足某些条件。

当浏览器向服务器发出请求时，它会在请求中添加一个源头`Origin: [https://localhost:3000](https://localhost:3000)`。如果这个请求发送到一个具有相同来源的服务器，浏览器就会允许它。但是，如果请求去往不同的 URL，称为*跨源请求*，那么服务器必须向响应消息添加一个`*Access-Control-Allow-Origin*` 报头。然后，浏览器会将此标题与原点进行匹配。如果不匹配，浏览器将拒绝响应，抛出一个 cors 错误。这是*同源*策略，实施该策略是为了防止*跨站点请求伪造攻击*，恶意网站利用浏览器的 cookie 存储系统。

![](img/dc4d6a0633d4fb750acc2fbd062aa904.png)

This is what the CORS error looks like.

当使用 API 和/或托管时，这个错误经常困扰开发人员。下面是解决这个问题的一些方法。

## 场景 1 —构建全栈应用

在开发环境中，一切似乎都很好，因为您在同一台机器上运行服务器和客户机程序。然而，当您部署您的服务器(使用 Heroku 或一些其他服务)然后试图请求数据时，Snap！cors 错误开始出现。

好消息…修复真的很简单。您只需要将 Access-Control-Allow-Origin 头添加到服务器响应中。

> `response.header('Access-Control-Allow-Origin', '*')`

这里，“*”指定通配符值，以允许所有域访问服务器资源。服务器也可以非常具体，只在头中包含可以访问资源的域的源 URL。

**—替代解决方案:使用 cors 包。**

> 安装— `npm install cors`
> 
> 进口— `const cors = require('cors')`
> 
> 为您的服务器添加中间件— `app.use(cors())`

您可以配置 cors 选项，甚至只将它添加到特定的端点，而不是所有的响应。点击查看软件包文档[。](https://www.npmjs.com/package/cors)

## 场景 2 —在前端从第三方 API 获取数据

假设您的前端试图向 [GitHub 作业 API](https://jobs.github.com/api) 发出 GET 请求。但是这个 API 没有在响应中包含一个`Access-Control-Allow-Origin`头，这导致了一个 cors 错误。

**—解决方案 1:将您的请求发送到获取代理(快速修复)**

代理服务器充当客户端和 API 之间的中间件。GET 请求首先到达添加了`Access-Control-Allow-Origin`头的代理，然后将请求转发给客户机。

有许多免费的代理服务器可供选择，如 cors anywhere、thingproxy、等。要使用获取代理，请将代理 URL 附加到 API 请求中。请参见下面的示例:

> 上一个— `axios.get(https://jobs.github.com/positions.json)`
> 
> 已修改— `axios.get(https://cors-anywhere.herokuapp.com/https://jobs.github.com/positions.json)`

这里是你可以使用的 10 个免费代理服务器的列表。这个解决方案很棒，因为它易于实现。然而，这些代理中的大多数仅用于开发目的，或者仅提供临时使用的演示，或者不能在生产环境中工作。此外，通常需要一段时间才能收到影响应用程序性能的响应。

**—解决方案 2:构建自己的代理服务器**

不要担心，这比听起来容易得多，最好的解决方案是构建自己的代理，这将为您的设计和实现提供更多的灵活性和控制力。构建一个简单的服务器，从 API 获取数据，并将相同的数据发送到您的前端，同时将`Access-Control-Allow-Origin`头添加到响应中。下面是一个使用 restify 从 GitHub Jobs API 获取数据的节点代理示例。

带有非标准头(Put、Patch、Delete)的 HTTP 请求需要预先飞行。浏览器首先使用选项 HTTP verb 发出请求，服务器使用头`Access-Control-Allow-Methods: PUT`使用该源允许的方法进行响应，之后可以发送实际的请求。服务器可以用一个`Access-Control-Max-Age: 30000`头来响应，允许浏览器在一定时间内缓存预检，使过程更加高效。

**一些临时修复—**

*   将`"proxy": "API_URL"`添加到 package.json 文件中，并修改获取查询以将请求发送到“/”
*   安装允许-控制-允许-起源浏览器插件。

**免责声明:**这些解决方案只在开发中有效，在生产环境中会失败。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)