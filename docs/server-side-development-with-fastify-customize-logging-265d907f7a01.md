# 使用 Fastify 进行服务器端开发—自定义日志记录

> 原文：<https://javascript.plainenglish.io/server-side-development-with-fastify-customize-logging-265d907f7a01?source=collection_archive---------8----------------------->

![](img/319befe918a5428f7be3eef021f836ac.png)

Photo by [Uillian Vargas](https://unsplash.com/@vargasuillian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Fastify 是一个用于开发后端 web 应用程序的小型节点框架。

在本文中，我们将了解如何使用 Fastify 创建后端应用程序。

# 自定义日志记录

我们还可以定制如何记录响应。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: {
    prettyPrint: true,
    serializers: {
      res (reply) {        
        return {
          statusCode: reply.statusCode
        }
      },
      req (request) {
        return {
          method: request.method,
          url: request.url,
          path: request.path,
          parameters: request.parameters,
          headers: request.headers
        };
      }
    }
  }
});fastify.get('/', (request, reply) => {
  request.log.info('Some info')
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

用`res`方法序列化响应日志内容。

我们用`req`方法对请求做同样的事情。

我们将`prettyPrint`设置为`true`来打印我们的输出。

我们可以在请求中添加一个钩子来记录请求负载，方法是:

```
const fastify = require('fastify')({
  logger: 'info'
});fastify.addHook('preHandler', (req, reply, done) => {
  if (req.body) {
    req.log.info({ body: req.body }, 'parsed body')
  }
  done()
})fastify.post('/', (request, reply) => {  
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

我们得到`req.body`，并将其放入`req.log.info`调用中。

此外，我们可以在路由处理程序之外使用日志记录器。

例如，我们可以写:

```
const log = require('pino')({ level: 'info' })
const fastify = require('fastify')({ logger: log })log.info('does not have request information')fastify.get('/', function (request, reply) {
  request.log.info('includes request information, but is the same logger instance as `log`')
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

我们在路由处理器外调用`log.info`。

我们称之为`request.log.info`。

我们可以用`redact`属性编辑日志信息。

例如，我们可以写:

```
const split = require('split2')
const stream = split(JSON.parse)const fastify = require('fastify')({
  logger: {
    stream,
    redact: ['req.headers.authorization'],
    level: 'info',
    serializers: {
      req (request) {
        return {
          method: request.method,
          url: request.url,
          headers: request.headers,
          hostname: request.hostname,
          remoteAddress: request.ip,
          remotePort: request.socket.remotePort
        }
      }
    }
  }
})fastify.get('/', function (request, reply) {
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

我们添加了`redact`属性来添加要在 ur 日志中跳过的属性路径。

现在我们不会在日志中看到`req.headers.authorization`的值。

# 结论

我们可以用 Fastify 定制我们的日志。

*阅读更多请点*[***plain English . io***](https://plainenglish.io/)