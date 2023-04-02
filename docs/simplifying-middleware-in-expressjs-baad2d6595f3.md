# 为新手和专业人士简化 Express 中的中间件

> 原文：<https://javascript.plainenglish.io/simplifying-middleware-in-expressjs-baad2d6595f3?source=collection_archive---------8----------------------->

![](img/3fc2e769bd11475e2a2299b85803adff.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在编写 Express 应用程序时，最重要的是真正理解**中间件**的概念，因为它们是构建 Express 应用程序的构件。尽管很多开发人员在 Express 项目中实现了这个概念，但是很多人仍然没有完全理解这个概念。

在本文中，我将尽最大努力用最简单的类比来解释中间件，以便新手和有经验的开发人员更好地理解它。

# **秘书的比喻**

![](img/47e7ffc52e3a253d667fc083f86ca0ac.png)

正如在大多数拥有标准组织文化的现代企业中所看到的那样，在最高管理层的右边是一位可靠的**秘书**。

向公司高层管理人员提出的任何要求都必须通过**秘书**。各组织秘书的主要日常职责是**沟通**和**通信**。向最高管理层提出的请求通常要经过秘书，秘书分析信息并寻找最合适的方法来传递信息。

对提交给部长的信息进行分析和审查，以发现不符合某些政策的情况。此外，秘书执行其他任务，如文件，复制信息和许多其他程序，可能会增加有关组织。因此，发送给组织的任何信息/请求很少会不经过这一流程。

最后，当高层管理人员对员工或公众作出回应时，秘书在其中发挥作用。他/她(秘书)通常以接收者能很快理解的最佳方式传递信息。

在这个场景中，我们可以看到秘书基本上充当了中间人**的角色**，高层管理人员的所有请求和响应都是向其发出的。

总之，**Express**M**iddleware**可以表示为**秘书，它们采用回调函数的形式，所有 HTTP 客户端请求和服务器响应都由回调函数完成。**与类比相反，一个客户端请求中可以出现不止一个中间件。

故事讲完了。

基本示例:

```
const express = require ('express');
const app = express();middle1(req, res, next) => {
      console.log('You have made a request')
}app.get('/', middle1)
```

举例说明上面的代码，函数 middle1 将作为一个中间件，所有对服务器的 GET 请求都将通过它。因此，对于所有 GET 请求，*‘您发出了请求’*将被记录在控制台中。

另一个有用的比较是，Express 中间件充当每个客户端向服务器发出的请求的功能层。

# **定义。**

因此，最可靠的定义(来自明确的官方文件)是:

> ***中间件*** 函数是访问[请求对象](https://expressjs.com/en/4x/api.html#req)(`req`)[响应对象](https://expressjs.com/en/4x/api.html#res) ( `res`)以及应用程序请求-响应周期中的下一个中间件函数的函数。下一个中间件功能通常用一个名为`next`的变量来表示。

# **Express 中中间件的类别**

在处理 express 中间件时，需要理解 3 个主要类别。这些类别是:

1.  **应用级中间件:**

它们表示通过使用 app.use 和 app.method()绑定到 app 对象的中间件。

app.use 将包含所有请求，而 app.method 将特定于请求类型。(获取、发布、删除和放置)。

**例如:**

```
const express = require('express')
const app = express()//for all requests made
app.use(function (req, res, next) {
  console.log('I am an application level middleware')
  next()
})
```

**2。路由器级中间件:**

与应用级中间件相同，但主要区别在于它被绑定到 Express 路由器的一个实例。

**例如:**

```
const express = require('express')
const app = express()
const router = express.Router()// this example is respective only to get requests
router.get('/user/:id',(function (req, res, next) {
  console.log('Time:', Date.now())
  next()
})
```

3 **。错误处理中间件**

与其他中间件功能的工作方式相同，只是它有 4 个参数。

**例如:**

```
app.use(function (err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
})
```

好了，希望这有助于更好地简要解释 **Express** 中间件**的概念。关于 Express 中中间件的更深入的解释，我建议您阅读官方文档:**

[](https://expressjs.com/en/guide/using-middleware.html) [## 使用中间件

### Express 是一个路由和中间件 web 框架，它有自己的最小功能:Express 应用程序是…

expressjs.com](https://expressjs.com/en/guide/using-middleware.html) 

感谢阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)