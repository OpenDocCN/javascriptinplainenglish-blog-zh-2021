# 在 Next.js 中创建一个类似 Express 的框架

> 原文：<https://javascript.plainenglish.io/express-like-framework-in-next-js-27a884a0264d?source=collection_archive---------7----------------------->

![](img/345ad969a0db60f79e2cfb9e843e7add.png)

在本文中，我将演示如何在 Next.js 中构建类似 Express 的 API，而不需要部署 Express 服务器，只需做一些调整。

如果您正在寻找 Express 框架的好处，但对您的应用程序保持无服务器状态感到满意，这可能是您的一个选择。

# 使用 Next.js 的注意事项

我从 Next.js 开始了我的旅程，因为它使 React 的服务器端呈现变得简单明了。它允许我在页面加载之前轻松地选择要呈现的内容，并且有一个 pages 文件夹用于直观的路由。我还发现了[无服务器的其他好处](https://blog.newrelic.com/engineering/what-is-serverless-architecture/),比如易于部署，更注重产品开发而不是管理服务器。

> *以后想看这个故事吗？* [*保存在日记本上。*](https://usejournal.com/?utm_source=medium.com&utm_medium=noteworthy_blog&utm_campaign=tech&utm_content=guest_post_read_later_text)

这意味着你这边的工作更少，但控制也更少。阅读 Vercel 平台的限制[以了解它是否适合您的应用程序是很有用的，注意在没有企业计划的情况下，有 1000 个并发请求的限制](https://vercel.com/docs/platform/limits#)[。](https://vercel.com/docs/platform/limits#)

# Next.js 的 API vs Expresss

我主要关心的是如何设计我的 API。对于[无服务器函数](https://vercel.com/docs/serverless-functions/introduction)，理想的模式是让每个路由在 pages/api 目录中的单个文件中提供单个函数(例如 **GET '/api/user/:id'** )。

我正在从一个快速环境中迁移，并享受将功能留给控制器的逻辑流程。我的应用程序有一个定制的身份验证流，所以像 **/api/login/** 这样的端点太大了，很难限制在一个函数中。更不用说我想重用其中的一些功能，所以将这个逻辑存储在隔离的端点对我来说没有意义。

问题变成了:

# 我可以简单地将 Express 与 Next.js 一起使用吗？

是的，但不是没有一些权衡。

一种选择是设置一个定制服务器，但是这首先就否定了使用 Next.js 的一些理由，因为您不能在 Vercel 上部署，并且您不再是无服务器的。然而，对于许多应用程序来说，这是正确的选择，尤其是那些受益于管理自己的服务器的大型应用程序。

另一个选择是[在无服务器功能](https://vercel.com/guides/using-express-with-vercel)内使用 Express。Vercel 建议这只是一种迁移你的应用程序的方法，本质上是将你自己从一个专用的服务器中分离出来。个人觉得在无服务器环境下运行 Express 有点傻。这也意味着您在对每个请求执行完整的服务器实现，这违反了无服务器功能服务于一个目的的模式。但我并不是说这对你没用。

我决定留在 Next.js 的缓冲区内，并尝试在不使用 Express 的情况下从 Express 的框架中获得我想要的好处。

# 我遇到的问题

我在我的应用程序中设置了一个控制器目录，在那里我导出了无数的函数，并从我的无服务器函数中像调用中间件一样调用它们。

然而，在 Next.js 中这样做很麻烦，因为它缺少一个 Next()函数，Express 使用这个函数来**转义**中间件链和**绕过**其余的功能。

从本质上说，不能访问 next()意味着我不能轻易摆脱中间件。

# 不要做什么:

在本例中，我们有一个端点，它在发送用户数据之前等待令牌的验证。如果中间件功能告诉我们没有通过验证，我们需要处理这个响应，避免执行下一个中间件功能。

```
**/api/authenticateUser**import authController from 'controllers/authController';export default async (req, res) => {try { **// Controller sends back a boolean "verified" and "userId"**
  const result = await authController.verifyToken(req, res);
  if (result.verified === false) {
    return res.json({ error: 'Not authenticated'})
  }; const payload = { userId: result.userId }; **// Fetch user data by userId. Returns username**  const data = await authController.header(req, res, payload);
  const { username } = data; return res.json({ username });} catch(e) {
  return res.status(500).send(e.message);
}};
```

如您所见，这看起来一点也不像我们在 Express 中习惯的干净的中间件链。我必须将类似{ verified: true }的信息传递回“waiting”函数，以便处理异常。

在 express 中，我们只需在控制器内部返回类似 next(err)或 RES . JSON({ error:' custom error ' })**，**的内容，如果我们没有命中 next()语句，就不会继续。这里，如果我们从控制器调用 res.json()，它将从函数中返回，但不会一起结束响应。

还要注意，没有 res.locals 对象在它们之间传递数据是多么笨拙。我们必须将数据打包到有效载荷中，并将每个控制器调用的结果解包。

# 解决方案是:

(解释如下)

```
import wrapper from ‘utils/wrapper’;
import authController from ‘controllers/authController’;const handler = async (req, res, middlewareChain) => { await middlewareChain
  (
    authController.verifyToken,
    authController.getUserId,  
  )
  .then(result => { if (!result) return; })
  .catch(e => { res.status(500).send(e.message); }) return res.json({
    username: res.locals.username
  });};export default wrapper(handler);
```

如果不向您展示我在顶部导入的包装函数，这并不能解释太多。请注意，我们不是导出函数，而是传递函数的包装器。

## 包装材料:

包装函数允许我们使用修改过的 res 和 req 函数来执行函数，以及将任何其他函数添加到我们的参数中(比如 middlewareChain)。

包装文件如下所示:

```
**utils/wrapper**const wrapper = handler => {return (req, res, middlewareChain) => {

    **/* res.locals object */** res.locals = {}; **/* middlewareChain function */** middlewareChain = async (...funcs) => {
      let finished = true;
      for (const func of funcs) {
        await func(req, res)
        if (res.finished) {
          finished = false;
          break;
        };
      };
    return next;
    }; return handler(req, res, middlewareChain);
  };
};module.exports = wrapper;
```

首先，您将看到我们可以像使用 Express 一样声明和使用 **res.locals** 。这使得我们可以轻松地在函数之间传递数据。

至于 **middlewareChain** 函数，它将所有控制器函数作为参数。对于每个函数，我们等待响应并检查我们是否调用了 res.json()或 res.send()。我们通过利用 res 对象固有的 **res.finished** 属性来检查这一点。当您调用 res.json()或 res.send()时，它的值会从 true 变为 false。(这通常是为了确保我们不会设置两次响应)。

如果我想早点退出我的控制器函数，可以调用 **return res.json({data})** 。我的 middlewareChain 将捕捉到我想返回一个响应并跳出循环。除了调用 **break** 之外，我们还将一个 **finished** 变量设置为 false，使得 middlewareChain 的返回值为布尔值。我们在**中处理这个响应。然后()**，说如果它求值为 false，返回。

当然，打破控制器功能的另一种方式是抛出一个错误，但是这并不适合每种情况。

## 使用包装器还可以做其他事情:

在我的应用程序中，我还将错误处理和 cookie 处理函数( **res.cookie** )放在了响应对象上，这是我强烈推荐的。我在这里写了一篇关于[以类似快递的方式处理 cookies 的文章](https://justinjaeger.medium.com/next-js-using-cookies-in-getserversideprops-89c03a216b0b)。

要点是，您可以将任何类型函数或对象附加到 req 和 res 上，这使您的生活更轻松，或者去掉重复的代码。

# 最后

这种策略可以帮助您保持类似 Express 的工作流，而不需要创建定制的服务器**和**,也不需要牺牲使用可以停止“中间件”链的控制器的能力。

📝把这个故事保存在[杂志](https://usejournal.com/?utm_source=medium.com&utm_medium=noteworthy_blog&utm_campaign=tech&utm_content=guest_post_read_later_text)上。