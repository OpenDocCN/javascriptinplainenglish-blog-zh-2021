# 使用 Fastify 的服务器端开发—初始配置和路由

> 原文：<https://javascript.plainenglish.io/server-side-development-with-fastify-initial-config-and-routes-f77262fbda94?source=collection_archive---------15----------------------->

![](img/e37396f81ac2df1eac1c34cbed676a26.png)

Photo by [Shiro hatori](https://unsplash.com/@shiroscope?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fastify 是一个用于开发后端网络应用程序的小型 Node 框架。

在本文中，我们将了解如何使用 Fastify 创建后端应用程序。

# 初始配置

我们可以通过初始化 Fastify 来设置应用程序的初始配置。

为此，我们写道:

```
const { readFileSync } = require('fs')
const Fastify = require('fastify')const fastify = Fastify({
  https: {
    allowHTTP1: true,
    key: readFileSync('./fastify.key'),
    cert: readFileSync('./fastify.cert')
  },
  logger: { level: 'trace'},
  ignoreTrailingSlash: true,
  maxParamLength: 200,
  caseSensitive: true,
  trustProxy: '127.0.0.1,192.168.1.1/24',
})console.log(fastify.initialConfig)fastify.get('/', async (request, reply) => {  
  return 'hello world'
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

设置初始配置。

`https`有 HTTPS 选择。

`allowHTTP1`让我们监听 HTTP1 请求。

`key`和`cert`是 SSL 密钥和证书文件。

`logger`设定采伐等级。

`ignoreTrailingSlash`让 Fastify 在匹配路由时忽略尾随斜线。

`caseSensitive`设置是否启用区分大小写的路由匹配。

`trustProxy`让我们设置信任哪个代理。

我们得到了具有`fastify.initialConfig`属性的配置。

此外，我们还可以通过以下方式动态设置选项:

```
const { readFileSync } = require('fs')
const Fastify = require('fastify')const fastify = Fastify({
  https: {
    allowHTTP1: true,
    key: readFileSync('./fastify.key'),
    cert: readFileSync('./fastify.cert')
  },
  logger: { level: 'trace'},
  ignoreTrailingSlash: true,
  maxParamLength: 200,
  caseSensitive: true,
  trustProxy: '127.0.0.1,192.168.1.1/24',
})console.log(fastify.initialConfig)fastify.register(async (instance, opts) => {
  instance.get('/', async (request, reply) => {
    return instance.initialConfig
  }) instance.get('/error', async (request, reply) => {
    instance.initialConfig.https.allowHTTP1 = false
    return instance.initialConfig
  })
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

我们编写`instance.initialConfig.https.allowHTTP1 = false`来设置`/error`路由处理程序中的`allowHTTP1`选项。

可以公开的属性包括:

*   `connectionTimeout`
*   `keepAliveTimeout`
*   `bodyLimit`
*   `caseSensitive`
*   `http2`
*   `https` (明确通过则返回`false` / `true`或`{ allowHTTP1: true/false }`
*   `ignoreTrailingSlash`
*   `maxParamLength`
*   `onProtoPoisoning`
*   `pluginTimeout`
*   `requestIdHeader`

# 路线

我们可以用`fastify.route`方法来申报路线。

例如，我们可以写:

```
const fastify = require('fastify')()fastify.route({
  method: 'GET',
  url: '/',
  schema: {
    querystring: {
      name: { type: 'string' },
      excitement: { type: 'integer' }
    },
    response: {
      200: {
        type: 'object',
        properties: {
          hello: { type: 'string' }
        }
      }
    }
  },
  handler: function (request, reply) {
    reply.send({ hello: 'world' })
  }
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

添加`/`路线。

我们用`querystring`属性指定它接受的查询字符串。

我们用`response`属性指定它返回的响应。

`handler`具有路由处理功能。

`reply.send`向用户发送响应。

# 结论

我们可以通过`fastify.route`设置 Fastify 应用的初始配置，并为 Fastify 应用添加路由。

*阅读更多在*[***plain English . io***](https://plainenglish.io/)