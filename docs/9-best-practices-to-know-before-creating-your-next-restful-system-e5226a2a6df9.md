# 在创建下一个 Restful 系统之前要知道的 9 个最佳实践

> 原文：<https://javascript.plainenglish.io/9-best-practices-to-know-before-creating-your-next-restful-system-e5226a2a6df9?source=collection_archive---------6----------------------->

![](img/0bc2ba9f9cb441ffec2c20a252c649bf.png)

Photo by [Sincerely Media](https://unsplash.com/@sincerelymedia?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

REST 架构是为 Web 服务创建交互式 API 的最常见的架构。REST 是由 Roy Fielding 在 2000 年首次提出的。20 年后，REST API 几乎被所有企业使用。

REST 架构没有为 API 开发提供任何指南或标准。所有 Restful API 只需要遵循 Roy Fielding 创建的 6 个约束。你们大多数人都知道这 6 个约束:客户机-服务器架构、可缓存性、无状态性、分层系统、统一接口和按需编码。

由于设计 Rest API 没有具体的指导原则，我们必须非常仔细地设计 Rest API，这样在未来，我们就不会有任何与安全性、性能或易用性相关的问题。

自从 REST 问世 20 年以来，许多人都写过关于设计 REST APIs 的最佳实践。本文将着眼于创建 rest API 的 9 个最重要的实践。

# 1)在 Rest 端点中总是用名词代替动词

在休息，动词已经出现在 URI。我们应该始终避免在 REST API 的 URI 中引入动词。当您调用 rest 端点时，总是必须用请求定义 HTTP 方法。常见的 HTTP 方法如下:

```
POST: Create a new data in server
GET: Retrieve data from server
PUT: Update resource data in server
PATCH:Update partial resource data in server
DELETE: Delete data from server
```

基本上，这些 HTTP 方法已经在 URI 中引入了动词，所以引入另一个动词没有意义。以端点在博客服务中创建帖子为例。我们可以创建后 URIs 像下面两个端点。

```
[http://localhost:8081/v1/createnewblog](http://localhost:8081/v1/createnewblog)
[http://localhost:8081/v1/](http://localhost:8081/v1/createnewblog)blogs
```

现在我们调用这个 POST 方法，所以我们已经知道我们正在创建一个博客，在 URL 中添加“createnewblog”没有任何帮助。另外在 URL 中添加一个动词只会让用户感到困惑。假设如果我们选择在 endpoint 中添加“createnewblog”，那么 endpoint 将通过什么来检索 blog，会是“[http://localhost:8081/v1/get blog](http://localhost:8081/v1/createnewblog)”吗？如果我们不使用动词，这将非常容易，如果我们需要检索产品，我们可以使用 URL http://localhost:8081/v1/blogs/{ blog Id }上的 GET 方法

# 2)端点上的逻辑嵌套是优选的，但不是强制的

我在很多地方读到过，当您为 rest 设计端点时，总是建议您应该将包含相关信息的资源分组。这基本上意味着，如果某个对象包含另一个对象，它应该反映在 URL 中。

例如，每个博客都可以有评论。因此，检索特定博客端点的评论就像。

```
http://localhost:8081/v1/blogs/1/comments/
```

您可能还必须检索用户所做的评论，因此，您必须创建另一个 URI。这是 URI 逻辑嵌套的问题之一，你必须创建一个冗余的 URI 来获得一个注释列表。嵌套的 URI 也会变得很长，比如你想让所有员工都在 XYZ 公司和 ABC 部门工作。URI 对于这个请求会是这样的:

```
http://localhost:8081/v1/companies/XYZ/departments/ABC/employees
```

通常，当您的数据是严格分层的，嵌套不太深，并且关系不经常改变时，嵌套 URI 是首选。在其他情况下，在 URI 并不强制使用嵌套。你可以在 URI [这里](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Best-Practices-for-Sub-and-Nested-Resources/)检查使用嵌套资源的利弊，并做出相应的选择。

# 3)优雅地处理错误并返回标准错误代码

优雅地处理错误非常重要。如果您收到错误的请求，那么整个服务就会停止，这真的没有意义。服务器应该总是抛出正确的错误，这样用户就可以知道什么是问题。所有 Rest APIs 都应该返回正确的 HTTP 响应代码，比如状态代码 4**是为客户端错误保留的，5**是为服务器错误保留的。一些常见的 rest 代码如下:

```
400(Bad Request): It indicates something is wrong with request.
401(Unauthorized): It indicates user is not able to authenticate.
403(Forbidden): It indicates user don't have permission to access resource.
404(Not Found): It indicates unable to found resource.
500(Internal Server Error):
502(Bad Gateway):
503(Service Unavailable):
```

错误处理不应该仅限于正确的 HTTP 代码。在错误响应中，错误的正确描述也应该与状态代码一起给出。例如，在下面的响应中，通过查看错误响应，我们可以确定我们没有在请求中传递客户 id。

```
{
     "error": {
         "timeStamp": "18-07-2017 06:49:25"
         "message": "Mandatory Parameter Customer Id is missing from      Request.",      
         "status": "400",
         "code": 0001
     } 
}
```

您还可以在错误响应中添加一些其他信息，如脸书在其错误响应中也发送跟踪 id。每个人都应该注意的一点是，对于一个组织内的所有 REST API，所有的错误响应都应该是相同的。

# 4)允许过滤、排序和分页

有时候，您的 REST API 会有大量数据需要发送来响应。例如，一个用户可能想获得某个特定主题的所有博客。这样的博客可能有数百万个。如果您将在一次响应中返回整个列表，这可能会产生很多问题—例如，您可能会遇到内存不足的异常。支持分页总是必须的。用户也可能只需要访问所有博客的某个子集。喜欢用户只想访问一个月内创建的职位。在这种情况下，过滤会有所帮助

过滤和分页都有助于我们提高 API 的性能。用户可能还需要根据特定的字段对响应进行排序，因此也应该支持排序。

# 5)永远不要用纯文本回复

虽然不是 REST 强加的，但是大部分时候 JSON 是和 Rest 齐头并进的。响应 JSON 格式的请求而不是普通文本总是明智的。然而，仅仅在 JSON 中发送响应并不是您必须做的唯一事情。您还需要提供一个 Content-Type 头来响应值 application/JSON。如果您愿意，也可以使用其他格式的响应，比如 XML，但是 XML 响应并没有被广泛使用，因为它需要额外的处理。

# 6)永远不要损害终端的安全性

客户端和服务器之间的所有通信都应该受到保护。始终尝试为您的服务器启用 TLS，因为它将保护传输中的数据。有了现代的库，启用 SSL 是非常容易的。

我们还需要启用适当的基于角色的访问控制。毕竟，没有人会喜欢他/她的信息被其他用户访问。您应该始终给予用户执行所需操作的最低权限。例如，如果某种类型的用户只能搜索资源，那么应该只授予调用搜索 API 所需的权限。还应该记住，在 URL 中发送任何敏感数据都是一个大忌。所以你永远不应该设计一个在 URI 接受密码的 REST API。

# 7)尽量采用 OpenAPI 规范

根据 OpenAPI 规范的官方定义文档:

> OpenAPI 规范(OAS)为 RESTful APIs 定义了一个标准的、与语言无关的接口，允许人类和计算机在不访问源代码、文档或通过网络流量检查的情况下发现和理解服务的功能。正确定义后，消费者可以用最少的实现逻辑理解远程服务并与之交互。

在 OpenAPI 而不是实现 API 中，首先，在开发开始之前，合同文档就已经设计好并达成一致。这份合同大部分是用 YAML 文件写的，我们有各种工具，比如 swagger editor，可以让你轻松编辑和阅读 YAML 的内容。甚至您的 API 的所有消费者都可以使用该契约生成一个客户端工具包，而不需要额外的信息。

OpenAPI 附带了很多工具，这些工具不仅可以帮助你设计 API，还可以在 API 的整个生命周期中提供帮助。你可以在这里了解更多关于 OpenAPI 规范[的信息。](https://swagger.io/specification/)

# 8)哈特奥斯是你的朋友

HATEOAS 表示超文本是应用程序状态的引擎。这里的超文本指的是任何包含视频、音频、图像和文本等其他媒体链接的内容。在 REST 的上下文中，HATEOAS 意味着作为响应，我们将链接到其他资源。仅以 Github API 为例，下面是 1 个示例响应。作为回应，您可以看到不同资源有许多 URIs。

```
{
   "pull_request": {
     "patch_url": null,
     "html_url": null,
     "diff_url": null
   },
   "created_at": "2012-11-14T15:25:33Z",
   "comments": 0,
   "milestone": null,
   "title": "New logo",
   "body": "We should have one",
   "user": {
     "login": "pengwynn",
     "gravatar_id": "7e19cd5486b5d6dc1ef90e671ba52ae0",
     "avatar_url": "[https://secure.gravatar.com/avatar/7e19cd5486b5d6dc1ef90e671ba52ae0?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png](https://secure.gravatar.com/avatar/7e19cd5486b5d6dc1ef90e671ba52ae0?d=https://a248.e.akamai.net/assets.github.com%2Fimages%2Fgravatars%2Fgravatar-user-420.png)",
     "id": 865,
     "url": "[https://api.github.com/users/pengwynn](https://api.github.com/users/pengwynn)"
   },
   "closed_at": null,
   "updated_at": "2012-11-14T15:25:33Z",
   "number": 17,
   "closed_by": null,
   "html_url": "[https://github.com/pengwynn/api-sandbox/issues/17](https://github.com/pengwynn/api-sandbox/issues/17)",
   "labels": [
     {
       "color": "ededed",
       "name": "design",
       "url": "[https://api.github.com/repos/pengwynn/api-sandbox/labels/design](https://api.github.com/repos/pengwynn/api-sandbox/labels/design)"
     }
   ],
   "id": 8356941,
   "assignee": null,
   "state": "open",
   "url": "[https://api.github.com/repos/pengwynn/api-sandbox/issues/17](https://api.github.com/repos/pengwynn/api-sandbox/issues/17)"
 }
```

这些链接帮助我们的 API 的消费者进一步探索 API 的资源。就像如果你需要用户的头像，你真的不需要去文档。它的 URI 已经出现在响应中，您只需要使用那个 URI 并获取图像。

# 9)版本控制

每当您必须对请求或响应结构进行更改时，总有可能会破坏某些客户的利益。在这种情况下，版本控制可能是救命稻草。请求和响应中的所有更改都应该创建为 API 的单独版本。您的 API 的所有消费者可以逐渐转移到您的 API 的较新版本。版本化是一种比强迫所有消费者同时使用新版本 API 更好的方法。

有许多方法可以实现版本，最流行的方法是在端点本身维护版本。例如，在下面的端点 V1 是你的 API 的版本。

```
[http://localhost:8081/v1/](http://localhost:8081/v1/createnewblog)blogs/1/comments/
```

当我们在 REST API 的端点中维护版本时，这会使 HATEOAS 实现变得复杂，因为作为响应，您必须为所有资源添加一个版本。版本也可以在查询字符串中传递，甚至可以通过创建一个新的 Rest API 自定义头来传递。同样，这两种方法也会受到影响，因为它们会使 HATEOAS 的实现变得复杂。

更友好的一种方法是在 Accept 头中传递版本信息，如下所示:

```
GET [https://localhost:8081/blogs/3](https://localhost:8081/blogs/3) HTTP/1.1 
Accept: application/vnd.medium.v1+json
```

在上面的例子中，我们告诉服务器客户端需要我们 API 的 v1，并且响应应该是 JSON 格式的。服务器将尽力满足这些要求并提供响应。

在为您的组织选择正确的版本化方法时，您还应该考虑缓存。借助 URI 和查询字符串进行版本控制比其他两种方法更加缓存友好。对于自定义标头和客户标头，您可能需要编写额外的代码来实现缓存。

# **结论**

Rest API 乍看起来非常简单，但是设计完美的 Rest API 可能非常具有挑战性。设计一个 Rest API 有很多东西。强烈建议您在第一次设计 API 时花费时间和精力，以便在将来重新设计 API 时花费更少的时间。

如果你有任何疑问，请随时评论这篇文章。

# 参考

[](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/) [## REST API 设计的最佳实践——堆栈溢出博客

### 了解如何设计 REST APIs，使其易于任何人理解，面向未来，安全且快速，因为它们服务于数据…

stackoverflow.blog](https://stackoverflow.blog/2020/03/02/best-practices-for-rest-api-design/) [](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design) [## API 设计指南——云应用的最佳实践

### 大多数现代 web 应用程序公开了客户端可以用来与应用程序交互的 API。一个设计良好的 web API…

docs.microsoft.com](https://docs.microsoft.com/en-us/azure/architecture/best-practices/api-design) [](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Best-Practices-for-Sub-and-Nested-Resources/) [## 子资源和嵌套资源的 REST API 设计最佳实践

### 当我们开始设计一个 API 时，会出现很多问题，尤其是如果我们想创建一个 REST API 并遵循 REST…

www.moesif.com](https://www.moesif.com/blog/technical/api-design/REST-API-Design-Best-Practices-for-Sub-and-Nested-Resources/) [](https://medium.com/hashmapinc/rest-good-practices-for-api-design-881439796dc9) [## REST:API 设计的良好实践

### 设计您的 REST API，以便它能被使用

medium.com](https://medium.com/hashmapinc/rest-good-practices-for-api-design-881439796dc9) 

*更多内容尽在*[plain English . io](http://plainenglish.io/)