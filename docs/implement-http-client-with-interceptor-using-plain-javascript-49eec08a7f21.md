# 使用普通 JavaScript 实现带有拦截器的 HTTP 客户端

> 原文：<https://javascript.plainenglish.io/implement-http-client-with-interceptor-using-plain-javascript-49eec08a7f21?source=collection_archive---------6----------------------->

![](img/3d68c30b8f23403c0ec0591eedb9c99c.png)

Photo by [Glenn Carstens-Peters](https://unsplash.com/@glenncarstenspeters?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com/?utm_source=medium&utm_medium=referral)

从头开始构建东西总是令人着迷的。总是有可能使用像 [Axios](https://axios-http.com/) 这样的库。然而，从头开始构建不仅有助于理解编程语言。这也有助于您提高性能。在本文中，我们将使用 [JavaScript Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 来构建一个 HTTP 客户端。类似的过程可以在 Node.js 中使用 [HTTP](https://nodejs.org/api/http.html) 模块。

![](img/ec79aaf27ee39b45970cfbd03c50f54c.png)

Photo by [Barn Images](https://unsplash.com/@barnimages?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 先决条件

1.  基本了解最新 JavaScript (ES6 及以上)——[传播运算符](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)、[方法速记](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)
2.  异步编程的基本理解— [异步等待](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)。
3.  对[获取](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)的基本理解

## 目录

1.  创建一个模拟服务器
2.  添加服务类别
3.  构建一个简单的 HTTP 客户端模块
4.  实现拦截器模式

## 1.创建一个模拟服务器

在构建实际的 HTTP 客户端模块之前，我们需要处理数据。您可以使用任何 JSON 数据源。然而，对于本文，我们将创建一个带有一些基本端点的模拟服务器。我们还将为 HTML 和 JavaScript 添加一些静态文件。

**添加 JSON 服务器**
添加 JSON 服务器相当简单。您可以使用 **npx** 命令动态启动 JSON 服务器。

创建一个文件 **db.json** ，文件夹 **public** 。

```
md intercepter-demo
cd intercepter-demo
md public
touch db.json public/index.html public/app.js
```

添加下面的代码。

```
**// db.json**{
  "users": [
    {
      "name": "deepak",
      "age": 32,
      "address": "not found"
    }
  ]
}**// public/index.html**<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Implementing HTTP Client with Interceptor using Plain JavaScript</title>
  </head>
  <body>
    <h1>Open Console using inspector</h1>
    **<script src="app.js"></script>**
  </body>
</html>**// public/app.js**console.log("Welcome to How To Write Services Using JavaScript")
```

现在，您可以使用命令`npx json-server db.json.` 启动服务器。该命令可能会要求您安装一个模块。按(Y)继续。可以打开 [http://localhost:3000/](http://localhost:3000/) 查看变化。可以访问[http://localhost:3000/users](http://localhost:3000/users)获取用户列表。

## 2.添加服务类别

既然我们的 **app.js** 现在已经在工作了。我们可以开始添加代码了。为了添加服务模块，我将使用一个对象。

```
// app.jsconst services = {
  getUsers() {
    // TODO
  },
  createUser(user) {
    // TODO
  }
}
services.getUsers().then(console.log)
services.createUser({
  "id": Date.now(),
  "name": "deepak2",
  "age": 32,
  "address": "not found2"
}).then(console.log)
```

如果你已经注意到了，我正在使用[方法简写](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)在一个对象中创建函数。您可以将这些代码移动到一个单独的文件中，并将`export default services`作为一个外部模块。

因为我们已经有了[/用户](http://localhost:3000/users)端点。让我们添加通过服务模块获取用户的基本代码。

```
**const apiHost = `**[**http://localhost:3000`**](http://localhost:3000`)
const services = {
  getUsers() {
    **return fetch(`${apiHost}/users`)**
  },
  createUser(user) {
    **return fetch(`${apiHost}/users`, {
      method: 'POST',
      headers: { 'Content-Type': "application/json" },
      body: JSON.stringify(user)
    })**
  },
  updateUser({ id, ...user }) {
    **return fetch(`${apiHost}/users`, {
      method: 'PUT',
      headers: { 'Content-Type': "application/json" },
      body: JSON.stringify(user)
    })**
  }
}
const id = Date.now();services.getUsers().then(console.log)
services.createUser({
  "id": id,
  "name": "deepak2",
  "age": 32,
  "address": "not found2"
}).then(console.log)services.updateUser({
  "id": id,
  "name": "deepak2",
  "age": 33,
  "address": "not found2"
}).then(console.log)
```

刷新 [http://localhost:3000/](http://localhost:3000/) 页面后，您将在浏览器的控制台中看到日志。

如果你看到上面的代码，大量的样板代码必须反复编写。为了避免这种情况，我们可以构建一个包装器 HTTP 客户端。

![](img/2a3aad3ec57518d3ef32e0eb5457bd78.png)

Photo by [Cytonn Photography](https://unsplash.com/@cytonn_photography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 3.构建一个简单的 HTTP 客户端模块

HTTP 客户端必须支持 GET、POST、PUT 和 DELETE 协议。Fetch 只有一个方法 fetch 来支持所有的协议。然而，作为关注点分离(SOC ),我们应该分成多个方法。

```
const http = {
  async get(url, options = {}) {
    // TODO
  },
  async post(url, body = {}, options = {}) {
    // TODO
  },
  async put(url, body = {}, options = {}) {
    // TODO
  },
  async delete(url, body = {}, options = {}) {
    // TODO
  },
  async request(url, body = {}, options = {}) {
    **options.headers = {
      'Content-Type': "application/json",
      ...options.headers,
    };
    const res = await fetch(url, {
      body: body ? JSON.stringify(body) : undefined,
      ...options,
    });
    return res.json()**
  }
}
```

这里的**请求**是处理所有边缘情况的辅助方法。如果你想定制一个请求，你可以使用**请求**方法。

```
const http = {
  async get(url, options = {}) {
    **return this.request(url, null, options)**
  },
  async post(url, body = {}, options = {}) {
    **return this.request(url, body, { ...options, method: "POST" })**
  },
  async put(url, body = {}, options = {}) {
    // TODO
  },
  async delete(url, body = {}, options = {}) {
    // TODO
  },
  async request(url, body = {}, options = {}) {
    options.headers = {
      'Content-Type': "application/json",
      ...options.headers,
    };
    const res = await fetch(url, {
      body: body ? JSON.stringify(body) : undefined,
      ...options,
    });
    return res.json()
  }
}
```

在 HTTP 客户端更新之后，让我们看看如何修改服务类。许多样板代码已经转移到客户端。因此，服务等级将是精简的。

```
const services = {
  getUsers() {
    **return http.get(`${apiHost}/users`)**
  },
  createUser(user) {
    **return http.post(`${apiHost}/users`, user)**
  },
  updateUser({ id, ...user }) {
    return http.put(`${apiHost}/users/${id}`, user)
  }
}// Rest of the code.
```

![](img/8431c92c60611ae9f77b92d7a9b51b1b.png)

Photo by [Hobi industri](https://unsplash.com/@hobiindustri?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 4.实现拦截器模式

如果你使用过 Axios 或 express.js 这样的模块，你可能知道拦截器或中间件的概念。拦截器是函数或模块，它们根据请求或响应的实现方式来拦截请求或响应。使用拦截器的最大用途是根据条件为每个请求或响应添加公共代码。在本文中，我们将关注一个简单的用例，您希望基于 URL 模式在每个路由上添加一个**授权令牌**。

```
const http = {
  **cb: [],
  intercept(cb) {
    this.cb.push(cb);
  },**
  async get(url, options = {}) {
    return this.request(url, null, options)
  },
  // Rest of the code
  async request(url, body = {}, options = {}) {
    options.headers = {
      'Content-Type': "application/json",
      ...options.headers,
    };
    **// Iterate all interceptors to modify the options
    if (this.cb.length) {
      for (let fn of this.cb) {
        options = fn(options, url);
      }
    }**
    const res = await fetch(url, {
      body: body ? JSON.stringify(body) : undefined,
      ...options,
    });
    return res.json()
  }
}
**const authInterceptor = (options, url) => {
  if (/users/.test(url) && options.method === "POST")
    options.headers.Authorization = 'Bearer sometoken';
  return options
}
http.intercept(authInterceptor)**// Rest of the code
```

一旦你运行了上面的代码并且查看了网络调用。您会发现**授权‘不记名令牌’**将被添加到**/用户发布**呼叫中。您可以根据需要添加更多拦截器。

## 结论

本文简单演示了普通 JavaScript 的 fetch 模块的用法。这并不意味着，我鼓励你在生产环境中使用这些代码。我仍然建议您为您的生产代码选择一个好的库。但是，出于您自己的学习目的，您可以扩展这个版本的代码。

注意:你可以在下面的 Gist URL 中获得 app.js 代码

## **奖励:如何使用拦截器在 Axios 中添加授权头**

要向任何请求添加头，可以使用持久性数据存储，如 localStorage、sessionStorage。根据条件，您可以向请求添加令牌。

```
// Global Level
axios.interceptors.request.use(function () {
  **const token = sessionStorage.getItem("token");
  config.headers.Authorization = token;
  return config;**
});// Individual Instance
const instance = axios.create();
instance.interceptors.request.use(function () {
  **const token = sessionStorage.getItem("token");
  config.headers.Authorization = token;**
  return config;
});
```

**参考文献:**

*   https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Functions/Method _ definitions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions)
*   [https://developer . Mozilla . org/en-US/docs/Web/JavaScript/Reference/Operators/Spread _ syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
*   [https://axios-http.com](https://axios-http.com/)

*更多内容看* [***说白了。*** *报名参加我们的*](http://plainenglish.io/) [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***