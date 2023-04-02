# Axios 与 Fetch:哪个更好？

> 原文：<https://javascript.plainenglish.io/axios-vs-fetch-aeaec89023b3?source=collection_archive---------12----------------------->

## 哪个是你的首选？

![](img/f7916802dc2889afb445094c93ffe186.png)

Photo by [Miguel Á. Padriñán](https://www.pexels.com/@padrinan?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/web-text-1591060/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

```
Contents
· [Axios](#a760)
· [Fetch](#06f2)
· [Backward Compatability](#0571)
· [Response Timeout](#300d)
· [Interceptors](#5982)
· [JSON Data](#e099)
· [Conclusion](#59e5)
```

# Axios

对于那些不确定 Axios 是什么的人来说，它是一个基于承诺的用于浏览器和 Node.js 的 HTTP 客户端。在客户端(浏览器)，它将使用 XMLHttpRequests，而在服务器端，它将使用本机 Node.js 模块。您只需要调用`axios()`并把选项作为对象传入来创建一个 API 请求。

一种更简短、技术性更低的解释方式是，Axios 是一种工具，可以在对后端服务进行 API 调用时帮助简化数据检索。

下面是一个使用 Axios 的示例:

```
const axios = require('axios');
// We need to import the package into to our workspaceaxios({
  url: 'https://webapp/api/auth/sign-in',
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
  },
  data: {
    email: 'admin@admin.com',
    password: '12345678',
  },
})
.then(respsonse => {
  console.log(response.message);
});
```

# 取得

Fetch API 是一个简单的接口，它也允许开发人员向后端服务或 API 发出 HTTP 请求。它提供了在浏览器窗口对象上定义的方法`fetch()`。该方法只有一个必须传递的参数，即用户想要检索的资源的 URL，您可以也很可能将 options 对象作为第二个参数传递。

下面是一个使用 Fetch API 的示例:

```
fetch('https://webapp/api/auth/sign-in', {
  method: 'POST',
  headers: {
    'Accept': 'application/json',
    'Content-Type': 'application/json',
  },
  body: JSON.stringify({
    email: 'admin@admin.com',
    password: '12345678',
  }),
})
.then(respsonse => {
  console.log(response.message);
});
```

*   Axios 需要一个 options 对象，并且 URL 是在对象内部定义的。
*   URL 作为参数传递到`fetch()`中，而不是在 options 对象中设置。
*   Axios 使用 data 属性，Fetch 使用 body 属性。
*   在使用 Fetch 发送数据之前，我们需要对数据进行字符串化
*   这两种实现也有相似的语法。

# 向后兼容性

Axios 之所以获得如此庞大的追随者，是因为其广泛的浏览器支持。另一方面，Fetch 并没有得到广泛支持，你可以在这里查看哪些浏览器`fetch()`不支持。

# 响应超时

使用 Axios，开发人员可以通过在 options 对象上设置超时(以毫秒为单位)属性，轻松地为他们的请求设置响应超时。

虽然可以使用 Fetch 实现类似的功能，但它肯定不像 Axios 采用的方法那么简单。这里有一个简短的[教程](https://dmitripavlutin.com/timeout-fetch-request/)，你可以从中学习如何使用`fetch()`创建响应超时。

# 截击机

Axios 受 devs 欢迎的另一个原因是 Axios 有一个内置的功能来拦截 HTTP 请求。例如，您可以在每次发送 HTTP 请求之前记录一条消息或执行一些逻辑。

Fetch 不提供任何默认的方法来拦截请求。但这并不意味着没有办法克服这个小问题。您可以轻松地覆盖 Fetch 方法并定义一个定制的拦截器。

# JSON 数据

还记得我们在前面的例子中对 options 对象设置的`data`吗？Axios 会在发送 HTTP 请求之前自动将该数据字符串化。

然而，这是 Fetch 在默认情况下不能提供的另一个特性，但同样，它肯定是可以用一些额外的时间来完成的。

# 结论

到了这一步，你可能已经意识到或者还没有意识到 Axios 有一些默认提供给我们的便利特性，而 Fetch 没有。记住这一点，两人做同样的事情，而且都做得很好。

Axios 拥有的大多数功能也可以使用 Fetch 来重现。那么应该用哪一个呢？

Axios 提供了一个很好的一体化包供您轻松使用，但您需要所有这些功能吗？就一两个？您当前的项目使用 Fetch 可能会做得很好，如果您真的需要一些额外的功能，您所要做的就是花一点时间来创建一个工作区。有大量的资源供你学习如何做到这一点。

所以也许你可以问自己，“我需要这些特性中的任何一个吗？或者我的项目可以少一个需要担心的依赖吗？”。

*   axios—[https://axios-http.com/docs/intro](https://axios-http.com/docs/intro)
*   https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API

[](https://jrpotatodev.medium.com/how-to-create-a-simple-web-server-using-node-js-2021-5c3e89833128) [## 如何使用 Node.js (2021)创建一个简单的 web 服务器

### 使用 Node.js 的简单 web 服务器(2021)

jrpotatodev.medium.com](https://jrpotatodev.medium.com/how-to-create-a-simple-web-server-using-node-js-2021-5c3e89833128) [](https://jrpotatodev.medium.com/how-to-create-dynamic-forms-with-react-hook-form-2021-a3bccae35163) [## 如何用 react-hook-form 创建动态表单

### 在本教程中，我们将学习如何创建一个带有动态输入的表单，或者像有些人所说的那样，创建一个扩展表单

jrpotatodev.medium.com](https://jrpotatodev.medium.com/how-to-create-dynamic-forms-with-react-hook-form-2021-a3bccae35163) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)