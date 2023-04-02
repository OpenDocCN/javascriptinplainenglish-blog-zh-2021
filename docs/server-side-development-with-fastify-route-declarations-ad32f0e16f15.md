# 使用 Fastify 进行服务器端开发—路由声明

> 原文：<https://javascript.plainenglish.io/server-side-development-with-fastify-route-declarations-ad32f0e16f15?source=collection_archive---------13----------------------->

![](img/96fa767b385367254daa8d2693ea79bb.png)

Photo by [Guillaume Jaillet](https://unsplash.com/@i_am_g?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fastify 是一个用于开发后端 web 应用程序的小型节点框架。

在本文中，我们将了解如何使用 Fastify 创建后端应用程序。

# 路线声明速记

Fastify 附带了声明路线的简写方法。

这些方法包括:

*   `fastify.get(path, [options], handler)`
*   `fastify.head(path, [options], handler)`
*   `fastify.post(path, [options], handler)`
*   `fastify.put(path, [options], handler)`
*   `fastify.delete(path, [options], handler)`
*   `fastify.options(path, [options], handler)`
*   `fastify.patch(path, [options], handler)`

例如，我们可以写:

```
const fastify = require('fastify')()const opts = {
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
}
fastify.get('/', opts, (request, reply) => {
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

我们创建`opts`来设置响应模式。

然后我们把它作为第二个参数传递给`get`方法。

我们也可以写:

```
const fastify = require('fastify')()const opts = {
  schema: {
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
}
fastify.get('/', opts)const start = async () => {
  try {
    await fastify.listen(3000, '0.0.0.0')  
  } catch (err) {
    fastify.log.error(err)    
    process.exit(1)
  }
}
start()
```

将`handler`方法放在`opts`对象中，而不是传递给第三个参数。

# Url 构建

Fastify 支持静态和动态 URL。

例如，我们可以通过编写以下内容来注册参数路径:

```
const fastify = require('fastify')()fastify.get('/example/:userId', (request, reply) => {
  reply.send('example')
})
fastify.get('/example/:userId/:secretToken', (request, reply) => {
  reply.send('example')
})
fastify.get('/example/*', (request, reply) => {
  reply.send('example')
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

添加路线。

`:userId`和`:secretToken`是 URL 参数。

而`*`是通配符。

此外，我们可以使用正则表达式来匹配 URL 路由模式。

例如，我们可以写:

```
const fastify = require('fastify')()fastify.get('/example/:file(^\\d+).png', (request, reply) => {
  reply.send('example')
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

我们将 URL 模式与`(^\\d+)`模式进行匹配。

因此，当我们转到`/example/1.png`时，我们会看到返回的响应。

我们可以用斜杠定义多个路由参数。

例如，我们可以写:

```
const fastify = require('fastify')()fastify.get('/example/near/:lat-:lng/radius/:r', (request, reply) => {
  reply.send('example')
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

添加`:lat-lng`和`:r`路线参数。

我们可以用正则表达式做同样的事情:

```
const fastify = require('fastify')()fastify.get('/example/at/:hour(^\\d{2})h:minute(^\\d{2})m', (request, reply) => {
  reply.send('example')
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

# 结论

我们可以用 Fastify 声明具有各种匹配模式的路线。

*查看更多内容请点击*[***plain English . io***](https://plainenglish.io/)