# 停止在 JavaScript 中使用 Fetch API

> 原文：<https://javascript.plainenglish.io/stop-using-the-fetch-api-in-javascript-f3ac14aca026?source=collection_archive---------7----------------------->

## 这就是 Axios 更好的原因

![](img/721c5ee71e16d08ed440453e3530024f.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

作为一名开发人员，经常会有很多选项、包和路径需要遵循和选择。例如，当我们发出 HTTP 请求时，我们应该选择哪种方式？在这篇文章中，我将介绍 **Axios** 库和 **Fetch** API，并展示它们的区别。

# 它们是什么？

当我们想要通过 HTTP 协议与服务器通信时，我们发出请求并获取数据——这个过程被称为 AJAX(异步 JavaScript 和 XML)。任何前端开发人员在执行此操作时都会记得的两个最常见的关键字是——Axios 或 Fetch。

## Axios

Axios 是一个 JavaScript 库，用于从 Node.js 或浏览器发出 HTTP 请求。根据其文档，它可以:

*   从浏览器发出 XMLHttpRequests
*   从 Node.js 发出 HTTP 请求
*   支持承诺 API
*   拦截请求和响应
*   转换请求和响应数据
*   取消请求
*   JSON 数据的自动转换
*   客户端支持防止 [XSRF](https://en.wikipedia.org/wiki/Cross-site_request_forgery)

由于 Axios 库不是 JavaScript API 的原生库，我们必须将其导入到项目中。可以直接一步一步的检查安装[这里](https://github.com/axios/axios)！

## 获取 API

Fetch API 提供了从浏览器获取资源的接口。根据它的[文档](https://developer.mozilla.org/pt-BR/docs/Web/API/Fetch_API)，Fetch 为请求和响应提供了对象的通用定义。它还使用了**承诺**并提供了一个全局`fetch()`方法。该方法只需要您想要获取的资源的路径作为强制参数。无论成功与否，它都将返回一个承诺来解决该请求的响应。

# 和睦相处

以下是两者兼容的顶级浏览器列表:

*   axios——Chrome、Firefox、Safari、Opera、Edge、IE。
*   fetch——Chrome、Firefox、Safari、Opera、Edge。

可以肯定地说，Axios 在旧版本的浏览器中支持得很好，它也支持 IE，而 Fetch API 不支持。

# 安全

Axios 不太容易受到攻击，因为它具有针对 XSRF(跨站点请求伪造)的客户端保护。基本上，它发生在网站之间发出 HTTP 请求的情况下，在这种情况下，有人试图冒充系统用户。关于 CSRF 更好的解释可以在[这里](https://owasp.org/www-community/attacks/csrf)看到！

# 句法

比较 Axios 和 Fetch 时，需要注意的是，它们的语法明显不同。检查 Axios 的`GET`方法并取出:

```
const url = 'https://jsonplaceholder.typicode.com/posts';// Axios
axios.get(url)
  .then(response => console.log(response));// Fetch
fetch(url)
  .then(response => response.json())
  .then(data => console.log(data));
```

如果您从未见过它们，我相信您会想知道为什么在 Fetch 的情况下使用`.json()`方法。实际上，Axios 内部也是如此，当请求被解析时，它会自动序列化为 JSON。

# 拦截请求和响应

HTTP 拦截器对于检查从客户端到服务器的 HTTP 请求非常有用。它们很适合在请求/响应开始/接收之前进行更改。在 Fetch 中，没有办法拦截 HTTP 请求，但是可以通过覆盖全局`fetch()`方法并创建自己的拦截器来绕过它。

与此同时，Axios 已经拥有了自己的拦截器，甚至在做出`.then`或`.catch`的承诺之前就已经执行了。为了说明这一点:

```
axios.interceptors.request.use(
  config => {
    // something can be done with your request data here
    console.log('A request has been sent!');
    return config;
  }, (error) => {
    return Promise.reject(error);
  }
);axios.interceptors.response.use(
  config => {
    // something can be done with your response data here
    console.log('A response has been received!');
    return config;
  }, (error) => {
    return Promise.reject(error);
  }
);axios.get('https://jsonplaceholder.typicode.com/posts')
  .then(response => console.log(response));
```

# 超时和进度

我觉得 Axios 很酷的一点是 Fetch 不提供`timeout`作为它的设置之一，也就是请求被中止前的时间限制。超时是以毫秒为单位在`config`对象中传递的一个可能的设置选项。重要的是要记住，超时是响应超时，而不是连接超时。例如:

```
axios.get(
  'https://jsonplaceholder.typicode.com/posts',
  {
    timeout: 10
  }
)
  .then(response => console.log(response));
```

但是有一种方法可以使用 Fetch API 创建超时，例如:

```
const controller = new AbortController();
const timeoutValue = 10000;
const timeout = setTimeout(() => controller.abort(), timeoutValue);
fetch('https://jsonplaceholder.typicode.com/posts', { signal: controller.signal })
  .then(response => response.json())
  .then(data => console.log(data));
```

就进展而言，我们有另一个理由更喜欢 Axios，因为它提供了一种更简单的方式来了解您请求的进展。`OnUploadProgress`是配置对象中传递的可选设置之一。

# 错误处理

使用 Axios，处理错误要容易得多，因为错误响应会自动被拒绝，这与 Fetch 不同，Fetch 中甚至可以解决 404 或 500 个错误。在这种情况下，后端返回“500 内部服务器错误”代码，Fetch 将像处理代码“200 正常”一样处理它。为了在 Fetch 中处理这个问题，我们可以使用“ok”标志:

```
fetch('https://official-joke-api.appspot.com/jokes/ten/hehe')
  .then(response => {
    if (!response.ok) {
      throw Error(response.statusText)
    }
    return response.json()
  })
  .then(data => {
    console.log(data)
  })
  .catch(error => console.error(error))
```

就 Axios 而言，下面是一个简单的错误处理示例:

```
axios
  .get('https://official-joke-api.appspot.com/jokes/ten/hehe')
  .then(response => {
    console.log("response", response)
  })
  .catch(error => console.log(error))
```

# 结论

很明显，与 Fetch 相比，Axios 的易用性更高。另一个需要考虑的问题是，Axios 是一个需要包含在项目中的外部包，而 Fetch 已经内置在浏览器中，也就是说，它的总重量为 0 KB。我更喜欢在我的项目中使用 Axios，但这不是使用它的规则。所以做出明智的选择！快乐编码！

# 参考

[](https://github.com/axios/axios) [## axis/axis

### 浏览器和节点的基于承诺的 HTTP 客户端。js 新 axios 文档网站:单击此处从…

github.com](https://github.com/axios/axios) [](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) [## 获取应用编程接口-网络应用编程接口| MDN

### 获取 API 提供了获取资源的接口(包括通过网络)。对…似乎很熟悉

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)