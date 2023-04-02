# 使用 fastify-basic-auth 向我们的 Fastify 应用程序添加基本身份验证

> 原文：<https://javascript.plainenglish.io/add-basic-authentication-to-our-fastify-app-with-fastify-basic-auth-98ce7c00b107?source=collection_archive---------6----------------------->

![](img/fdfb4903544a3b88482e1ed3e2e5996e.png)

Photo by [Anders Jildén](https://unsplash.com/@andersjilden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

通过 fastify-basic-auth 库，我们可以快速地将基本身份验证添加到我们的 fastify 应用程序中。

在本文中，我们将了解如何使用这个库向我们的 Fastify 应用程序添加身份验证。

# 装置

我们可以通过运行以下命令来安装该软件包:

```
npm i fastify-basic-auth
```

# 添加基本身份验证

我们可以通过编写一些代码将基本的 auth 添加到我们的 Fastify 应用程序中。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})const authenticate = {realm: 'Westeros'}
fastify.register(require('fastify-basic-auth'), { validate, authenticate })function validate (username, password, req, reply, done) {
  if (username === 'foo' && password === 'bar') {
    done()
  } else {
    done(new Error('invalid user'))
  }
}fastify.after(() => {
  fastify.addHook('onRequest', fastify.basicAuth) fastify.get('/', (req, reply) => {
    reply.send({ hello: 'world' })
  })
})fastify.listen(3000, '0.0.0.0',  function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们用`validate`和`authenticate`注册`fastify-basic-auth`插件。

`validate`是验证用户名和密码的功能。

`authenticate`是设定境界的对象。

为了添加基本的 auth，我们调用了`addHook`来添加一个钩子，在每个请求上用`validate`检查用户名和密码。

任何在`after`钩子中注册的路由都有基本授权保护。

`validate`功能可以是异步的。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})const authenticate = {realm: 'Westeros'}
fastify.register(require('fastify-basic-auth'), { validate, authenticate })async function validate (username, password, req, reply) {
  if (username !== 'foo' || password !== 'bar') {    
    return new Error('invalid user')
  }
}fastify.after(() => {
  fastify.addHook('onRequest', fastify.basicAuth) fastify.get('/', (req, reply) => {
    reply.send({ hello: 'world' })
  })
})fastify.listen(3000, '0.0.0.0',  function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

如果`validate`是异步的，那么我们就不需要调用`done`。

此外，我们可以将它与`onRequest`属性一起使用:

```
const fastify = require('fastify')({
  logger: true
})const authenticate = { realm: 'Westeros' }
fastify.register(require('fastify-basic-auth'), { validate, authenticate })
async function validate (username, password, req, reply) {
  if (username !== 'foo' || password !== 'bar') {
    return new Error('invalid user')
  }
}fastify.after(() => {
  fastify.route({
    method: 'GET',
    url: '/',
    onRequest: fastify.basicAuth,
    handler: async (req, reply) => {
      return { hello: 'world' }
    }
  })
})fastify.listen(3000, '0.0.0.0',  function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们将`fastify.basicAuth`设置为`onRequest`的值，以向我们的 GET `/`路由添加基本 auth。

此外，我们可以将它与`fastify-auth`一起使用:

```
const fastify = require('fastify')({
  logger: true
})const authenticate = {realm: 'Westeros'}
fastify.register(require('fastify-auth'))
fastify.register(require('fastify-basic-auth'), { validate, authenticate })
async function validate (username, password, req, reply) {
  if (username !== 'foo' || password !== 'bar') {
    return new Error('invalid user')
  }
}fastify.after(() => {
  fastify.addHook('preHandler', fastify.auth([fastify.basicAuth]))fastify.route({
    method: 'GET',
    url: '/',
    onRequest: fastify.auth([fastify.basicAuth]),
    handler: async (req, reply) => {
      return { hello: 'world' }
    }
  })
})fastify.listen(3000, '0.0.0.0',  function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们在 GET `/`路径的`adfter`钩子和`onRequest`属性中注册了基本的 auth 处理程序。

# 结论

fastify-basic-auth 库允许我们用几行代码将基本身份验证添加到 fastify 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**