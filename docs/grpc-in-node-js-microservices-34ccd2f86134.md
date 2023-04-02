# Node.js 微服务如何使用 gRPC 相互交互

> 原文：<https://javascript.plainenglish.io/grpc-in-node-js-microservices-34ccd2f86134?source=collection_archive---------0----------------------->

![](img/d17abc1e5af287be96cc22ce78c266fc.png)

在本文中，我们将了解微服务如何使用 gRPC 框架相互交互。gRPC 是一种现代的 RPC，它使微服务能够相互交互。

## 什么是微服务？

微服务是一种架构，它将服务器应用程序分成松散耦合的服务。例如:

1.  专用于用户认证和授权的微服务。
2.  用于处理客户详细信息(获取、更新、插入等)的微服务。)
3.  处理产品的微服务。
4.  处理订单的微服务。
5.  这样的例子不胜枚举。

关于微服务更详细的解释可以在[https://en.wikipedia.org/wiki/Microservices](https://en.wikipedia.org/wiki/Microservices)找到

这些微服务经常需要相互交互。例如，orders 微服务经常需要产品细节和一些客户细节。

产品和订单微服务通常需要与用户的微服务进行交互，以了解用户是否被授权执行某些操作，如添加产品或确认订单。

有几种方法可以定义微服务之间的交互方式。最常用的有:

1.  肥皂
2.  HTTP REST 架构
3.  GraphQL

在本文中，我们将重点介绍一种新的协议，称为 gRPC。与旧协议不同，此协议基于 HTTP 2.0 协议。

## 这种新协议的一些优点是:

1.  二进制数据而不是文本数据。因为二进制数据比文本数据压缩程度更高，所以确保了更低的延迟和更高的速度。
2.  HTTP 2.0 是完全复用的。HTTP 1.1 传输一个资源(比如图像、JavaScript 文件等等)，所以如果一个资源由于某种原因被阻塞，那么这个被阻塞的资源之后的所有资源也被阻塞。这在 HTTP 2.0 中不是问题，因为它可以在单个 TCP 连接中发送多个数据流，这样任何资源都不能阻塞其他资源。
3.  服务器推送:服务器推送多个资源以响应一个请求。
4.  标题压缩确保了更快的加载时间。

## 设置 Node.js 环境

为了演示如何在 Node.js 应用程序中实现 gRPC，我们将构建两个应用程序。

1.  用户 _ 服务器
2.  用户 _ 客户端

第一步是定义计划传输的数据和要使用的功能。定义这些功能的文件是一个原型定义文件(`.proto`)，我们将使用的语言是协议缓冲语言。

所以让我们开始写一个. proto 文件。第一行是原型版本声明:

我们还必须定义一个包:

我们将协议缓冲语言版本定义为版本 3。现在我们可以为我们应该接收的数据定义一个数据结构。

我们定义的第一个对象是 OrderItemObject。每个 order item 对象将包括 3 个属性:`orderId`作为一个数字，`orderDescription`作为一个字符串，quantity 作为一个数字。

假设我们必须接收特定客户的订单项目列表。为此，我们将创建第二个对象来汇总返回给客户端的数据。它将包括两个属性:`customerID`作为一个数字和一个之前定义的订单项数组。

现在让我们定义函数的参数:

最后，现在我们可以定义方法本身了:

完整的文件将如下所示:

## 构建服务器端组件

首先，我们必须导入外部库来加载`.proto`文件并创建 gRPC 服务器:

```
npm i @grpc/grpc-jsnpm i @grpc/proto-loader
```

在这个新文件中，让我们定义原型文件路径:

现在，我们将导入在使用 NPM 之前下载的外部组件:

现在，我们将导入在使用 NPM 之前下载的外部组件:

我们现在将定义包装定义:

`PROTO_PATH`代表原型文件的路径。第二个对象定义了包定义的不同参数。此处的不同参数可在[https://www.npmjs.com/package/@grpc/proto-loader](https://www.npmjs.com/package/@grpc/proto-loader)上详细解释

现在让我们将刚刚创建的包定义加载到`gRPC`对象中。

OnlineShop 是我们创建的原型文件的包名。

现在，仅仅为了演示 gRPC，我们将创建一个硬编码的对象来表示来自服务器的数据。

现在，我们终于可以实现以下内容了:

在`.proto`文件中，我们定义了一个名为`GetOrdersForCustomerID`的服务，其中一个参数表示`customerID`。在函数中，我们通过调用`call.request.id`来获取这个参数值。输出由回调函数发出。

剩下的工作就是将所有东西都绑定到一个工作模块中:

这是完整的服务器文件:

现在，我们的服务器已经完成，我们可以通过以下命令来执行它:

```
node users_server.js
```

## 构建客户端组件

在本演示中，我们将构建一个简单的命令行实用程序，其执行方式如下所示:

```
node users_client.js —baseaddress localhost —customerID 1
```

其中`baseaddress` 和`customerID` 是客户端组件的参数。我们期望获得 ID 为 1 的客户的所有订单。

因此，像在服务器组件中一样，我们必须导入我们在服务器组件中使用的相同的 proto 文件，导入`@grpc/grpc-js`和 `@grpc/proto-loader`，并创建包定义:

现在让我们创建我们的主函数，它叫做 main:

```
function main() {}
```

在这个函数中，我们必须解析参数(`baseaddress` 和 customerID)。为此，我们必须导入另一个名为`minimist`的外部库

```
npm i minimist
```

我们现在将参数，解析它们，并将它们存储到两个变量中:

如果参数中没有定义`baseaddress`，那么我们将把它设置为“localhost”。

下一步是创建一个连接到服务器的客户机对象:

最后一步是执行我们在服务器中定义的方法:

最终文件将如下所示:

## 总结:

我们看到了一个组件如何执行另一个组件的方法，就好像它是在本地执行的一样。

完整的源代码可以在:[https://github.com/krasnoff/gRPC_nodeJS_microservices](https://github.com/krasnoff/gRPC_nodeJS_microservices)找到

## 进一步阅读

[](https://bit.cloud/blog/component-driven-microservices-with-nodejs-and-bit-l64shurc) [## 具有 NodeJS 和 Bit 的组件驱动的微服务

### 大多数人认为组件是前端的一部分。然而，CBSE(基于组件的软件工程)是…

比特云](https://bit.cloud/blog/component-driven-microservices-with-nodejs-and-bit-l64shurc) [](https://plainenglish.io/blog/how-to-compose-and-integrate-apis-together-as-if-you-were-using-npm-for-apis) [## 如何将 API 组合和集成在一起，就像您正在使用 API 的 NPM 一样

### 将两个 API 整合到一个应用程序中，该应用程序显示了历史上最大的音乐会，按国家首都排列。与……

简明英语. io](https://plainenglish.io/blog/how-to-compose-and-integrate-apis-together-as-if-you-were-using-npm-for-apis) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***