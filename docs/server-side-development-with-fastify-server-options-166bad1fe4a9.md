# 使用 Fastify 进行服务器端开发—服务器选项

> 原文：<https://javascript.plainenglish.io/server-side-development-with-fastify-server-options-166bad1fe4a9?source=collection_archive---------11----------------------->

![](img/bd716bf38c06eac49864bacfa5013c04.png)

Photo by [Science in HD](https://unsplash.com/@scienceinhd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fastify 是一个用于开发后端 web 应用程序的小型节点框架。

在本文中，我们将了解如何使用 Fastify 创建后端应用程序。

# 服务器选项

我们可以在需要`fastify`的时候设置一些选项。

`http2`让我们使用 HTTP/2 来绑定套接字。

`https`让 ys 监听 TLS 连接。

`connectionTimeout`让我们以毫秒为单位定义服务器超时。

`keepAliveTimeout`让我们以毫秒为单位定义服务器保持活动超时。

`ignoreTrailingSlash`使 Fastify 在匹配路线时忽略尾随斜线。

例如，如果我们有:

```
const fastify = require('fastify')({
  ignoreTrailingSlash: true
})fastify.get('/foo/', function(req, reply) {
  reply.send('foo')
})// registers both "/bar" and "/bar/"
fastify.get('/bar', function(req, reply) {
  reply.send('bar')
})
const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

`/foo`和`/foo/`与`/foo/`路线相匹配。

并且`/bar`和`/bar/`与`/bar/`路线相匹配。

`maxParamLength`设置路线参数的最大长度。任何超过长度的都不会被调用。

`bodyLimit`设置最大请求体尺寸。

`logger`让我们启用记录器。

我们可以通过编写以下代码将`pino`添加为自定义记录器:

```
const pino = require('pino')();const customLogger = {
  info(o, ...n) { },
  warn(o, ...n) { },
  error(o, ...n) { },
  fatal(o, ...n) { },
  trace(o, ...n) { },
  debug(o, ...n) { },
  child() {
    const child = Object.create(this);
    child.pino = pino.child(...arguments);
    return child;
  },
};const fastify = require('fastify')({
  logger: customLogger
})fastify.get('/foo/', function(req, reply) {
  reply.send('foo')
})// registers both "/bar" and "/bar/"
fastify.get('/bar', function(req, reply) {
  reply.send('bar')
})
const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

`disableRequestLogging`让我们禁用请求日志记录。

`serverFactory`让我们将一个定制的 HTTP 服务器传递给 Fastify。

例如，我们可以写:

```
const Fastify = require('fastify')
const http = require('http')const serverFactory = (handler, opts) => {
  const server = http.createServer((req, res) => {
    handler(req, res)
  })
  return server
}const fastify = Fastify({ serverFactory })fastify.get('/', (req, reply) => {
  reply.send({ hello: 'world' })
})const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

使用`http`模块创建服务器。

`caseSensitive`让我们设置是否以区分大小写的方式匹配路线。

例如，如果我们有:

```
const fastify = require('fastify')({
  caseSensitive: false
})fastify.get('/user/:username', (request, reply) => {  
  reply.send(request.params.username)
})const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

然后如果我们去`/USER/NODEJS`，我们看到`NODEJS`，因为`caseSensitive`是`false`。

`genReqId`选项让我们用自己的函数生成请求 ID。

例如，我们可以写:

```
let i = 0
const fastify = require('fastify')({
  genReqId (req) { return i++ }
})fastify.get('/', (request, reply) => {  
  reply.send('hello world')
})const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')
  } catch (err) {
    fastify.log.error(err)
    process.exit(1)
  }
}
start()
```

创建我们自己的函数来生成请求 ID。

# 结论

我们可以用 Fastify 服务器配置一些选项。

喜欢这篇文章吗？如果有，在[**plain English . io**](https://plainenglish.io/)找到更多类似内容