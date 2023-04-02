# 使用 Fastify 开始服务器端开发

> 原文：<https://javascript.plainenglish.io/getting-started-with-server-side-development-with-fastify-e45b4917cb12?source=collection_archive---------11----------------------->

![](img/1b064e3308d820036f38debe508d510d.png)

Photo by [Anders Jildén](https://unsplash.com/@andersjilden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fastify 是一个用于开发后端网络应用程序的小型 Node 框架。

在本文中，我们将了解如何使用 Fastify 创建后端应用程序。

# 装置

我们通过运行以下程序安装`fastify`包:

```
npm i fastify --save
```

与 NPM 或:

```
yarn add fastify
```

纱线。

# 第一个应用

我们用几行代码创建了一个简单的服务器应用程序。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})fastify.get('/', (request, reply) => {
  reply.send({ hello: 'world' })
})fastify.listen(3000, '0.0.0.0', (err, address) => {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

使用`/`路由创建一个简单的服务器。

`logger`设为`true`启用内置记录器。

`reply.send`发出回应。

`fastify.listen`启动应用程序，监听服务器。

第一个参数是端口，第二个参数是监听请求的 IP 地址。`'0.0.0.0'`监听所有地址。

当我们进入`/`时，我们看到:

```
{"hello":"world"}
```

回来了。

我们也可以在路由器处理程序中使用`astbc`和`await`。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})fastify.get('/', async (request, reply) => {
  return { hello: 'world' }
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

我们只是返回我们想要的对象作为回应。

我们在没有回调的情况下调用`fastify.listen`。

# 验证请求数据

我们可以通过向我们的路由传递一个选项来验证请求数据。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})const opts = {
  schema: {
    body: {
      type: 'object',
      properties: {
        foo: { type: 'string' },
        bar: { type: 'number' }
      }
    }
  }
}fastify.post('/', opts, async (request, reply) => {
  return { hello: 'world' }
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

创建我们的模式，然后将属性传入其中。

我们规定了`foo`和`bar`属性的类型。

这让我们可以指定接受的属性。

# 序列化数据

我们也可以为响应指定模式。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})const opts = {
  schema: {
    response: {
      200: {
        type: 'object',
        properties: {
          hello: { type: 'string' }
        }
      }
    }
  }
}fastify.post('/', opts, async (request, reply) => {
  return { hello: 'world' }
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

指定`/`路由返回的响应。

# 运行我们的服务器

我们可以通过 Fastify 命令行界面运行 Fastify 应用程序。

我们通过运行以下程序来安装它:

```
npm i fastify-cli
```

在`package.json`中增加:

```
{
  "scripts": {
    "start": "fastify start server.js"
  }
}
```

然后我们运行它:

```
npm start
```

# 结论

我们可以使用 Fastify 轻松创建一个简单的后端节点 web 应用程序。

喜欢这篇文章吗？如果是这样，在 [**找到更相似的内容**](https://plainenglish.io/)