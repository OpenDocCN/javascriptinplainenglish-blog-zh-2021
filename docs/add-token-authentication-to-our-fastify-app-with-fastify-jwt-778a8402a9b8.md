# 使用 fastify-jwt 为我们的 Fastify 应用程序添加令牌认证

> 原文：<https://javascript.plainenglish.io/add-token-authentication-to-our-fastify-app-with-fastify-jwt-778a8402a9b8?source=collection_archive---------4----------------------->

![](img/951b562698608ab2a916be52587ae361.png)

Photo by [Harley-Davidson](https://unsplash.com/@harleydavidson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有了 fastify-jwt 库，我们可以快速地将基本认证添加到我们的 fastify 应用程序中。

在本文中，我们将了解如何使用这个库向我们的 Fastify 应用程序添加身份验证。

# 装置

我们可以通过运行以下命令来安装该软件包:

```
npm i fastify-jwt
```

# 发行代币

我们可以用这个方法发行代币。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})
fastify.register(require('fastify-jwt'), {
  secret: 'secret'
})fastify.post('/signup', (req, reply) => {
  const token = fastify.jwt.sign({ foo: 'bar' })
  reply.send({ token })
})fastify.listen(3000, '0.0.0.0', function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们只是调用方法，用我们想要的对象作为有效载荷来返回一个令牌。

# 验证令牌

我们可以用`jwtVerify`方法验证令牌。

例如，我们可以写:

```
const fastify = require('fastify')({
  logger: true
})
fastify.register(require('fastify-jwt'), {
  secret: 'secret'
})fastify.decorate("authenticate", async (request, reply) => {
    try {
      await request.jwtVerify()
    } catch (err) {
      reply.send(err)
    }
  })
  .after(() => {
    fastify.route({
      method: 'GET',
      url: '/secret',
      preHandler: [fastify.authenticate],
      handler: (req, reply) => {
        reply.send('secret')
      }
    })
  })fastify.post('/signup', (req, reply) => {
  const token = fastify.jwt.sign({
    foo: 'bar'
  })
  reply.send({
    token
  })
})fastify.listen(3000, '0.0.0.0', function(err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们调用`request.jwtVerify`方法，在我们调用`fastify.register`方法之后就可以使用了。

如果有错误，将运行`catch`程序块。

为了添加一些需要 auth 令牌的路由，我们添加了带有由`fastify.route`定义的路由的`after`回调。

`preHandler`在调用路由之前运行，以便我们可以运行授权令牌检查，并且只有在令牌有效时才调用路由处理程序。

# 饼干

我们可以将身份验证令牌放在 cookies 中。

例如，我们可以写:

```
const fastify = require('fastify')()
const jwt = require('fastify-jwt')fastify.register(jwt, {
  secret: 'key',
  cookie: { 
    cookieName: 'token'
  }
})fastify
  .register(require('fastify-cookie'))fastify.get('/cookies', async (request, reply) => {
  const token = await reply.jwtSign({
    name: 'foo',
    role: ['admin', 'spy']
  })reply
    .setCookie('token', token, {
      domain: '*',
      path: '/',
      secure: true,
      httpOnly: true,
      sameSite: true
    })
    .code(200)
    .send('Cookie sent')
})fastify.get('/verifycookie', async (request, reply) => {
  try {
    await request.jwtVerify()
    reply.send({ code: 'OK', message: 'it works!' })
  }
  catch(error){
    reply.send(error);
  }
})fastify.listen(3000, '0.0.0.0', function (err, address) {
  if (err) {
    fastify.log.error(err)
    process.exit(1)
  }
  fastify.log.info(`server listening on ${address}`)
})
```

我们添加了`/cookies`路径来发布 cookie。

注册了`fastify-cookie`插件后`setCookie`就可用了。

我们将`token`传递给`setCookie`方法，以传递响应头中的 cookie。

`secure`确保它发送到 HTTPS。

`httpOnly`确保它仅用于 HTTP 请求。

`sameSite`检查 cookie 是否是从使用它的同一站点发布的。

在`verifycookie`路径中，我们调用`request.jwtVerify`来验证 cookie，然后再做其他事情。

# 结论

我们可以使用 fastify-jwt 来发布 JSON web 令牌并验证它。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**