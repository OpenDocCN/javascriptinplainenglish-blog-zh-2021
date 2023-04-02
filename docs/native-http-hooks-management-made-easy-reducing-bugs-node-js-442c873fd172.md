# 使用 Node.js 使本机 HTTP 挂钩管理变得容易

> 原文：<https://javascript.plainenglish.io/native-http-hooks-management-made-easy-reducing-bugs-node-js-442c873fd172?source=collection_archive---------11----------------------->

![](img/06513d1431febb58be46c1df35a71425.png)

使用**本地 *HTTP*** 实例*[*node . js*](http://nodejs.org/)的**优势之一是它将允许我们尽可能多地使用它。但是不要担心，然后我们会介绍我们的盟友，使这更容易。不管我们是在**前端**上使用[*REST API*](https://www.redhat.com/en/topics/api/what-is-a-rest-api)*还是我们的**后端**需要调用外部服务，下面设想的用例都是有效的。****

**我们要用的包就是大家熟知的[***Axios***](https://github.com/axios/axios)。这是一个**助手**，它将处理我们的本地 *HTTP* 实例。**

## **很高兴知道这一点**

**随意看看官方 [*Node.js* 文档](https://nodejs.org/es/docs/)关于 [HTTP 协议](http://nodejs.org/api/http.html)通过其**原生库**的使用。这将帮助我们**理解**通过它的可用方法[***Axios***](https://github.com/axios/axios)正在采取什么动作。**

# **安装**

**让我们将这个包添加到[*package . JSON*](https://docs.npmjs.com/cli/v7/configuring-npm/package-json)*中的" [*dependencies*](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#dependencies) "部分，但是如果您使用的是 [TypeScript](https://www.typescriptlang.org/docs/handbook/intro.html) ，这个包已经包含了类型***

```
**npm install --quiet --save axios**
```

**本教程中使用的软件包的当前 [npm 注册表版本](https://www.npmjs.com/package/axios#installing)是:**

```
**"axios": "^0.21.1"**
```

**使用 ***Axios*** 的主要优势之一是**关于使用 [HTTP 协议](http://nodejs.org/api/http.html)的安全更新**是由*[*node . js*](http://nodejs.org/)的维护人员进行的😃***

# **选择钩子**

**该软件包引入了 [***拦截器的概念***](https://www.npmjs.com/package/axios#interceptors) 对任何 *HTTP* 请求。这将允许我们在使用任何可用的 *HTTP* 方法之前或之后执行我们的**定制功能**。这为**修改请求的部分内容**或简单地执行任何其他动作而不进行修改提供了机会。**

# **触发 HTTP 方法**

**在我们的例子中，我们有一个在 [*Node.js*](http://nodejs.org/) 中制作的后端，每当它需要调用一个外部提供者的 *HTTP* *API* 时，它需要通过一个[授权头](https://developer.mozilla.org/es/docs/Web/HTTP/Headers/Authorization)证明它的服务是经过认证的。**

**这个应用程序使用对不同的*API*的多次调用，所以我们不需要在所有请求中添加这个新的头。出于这个原因，我们将使用 Axios 的 [**新实例，这将允许我们**添加拦截器**，该拦截器将只在对该外部提供者**的 *HTTP* 调用中执行，而不影响应用程序中已经存在的**的其余**调用。](https://www.npmjs.com/package/axios#creating-an-instance)**

**因此，对于我们在应用程序中调用的每个外部 *API* 使用不同的**[**Axios**](https://www.npmjs.com/package/axios)**实例**是一种**良好做法。******

## ****创建实例****

****首先，要求包装:****

```
****const axios = require('axios').default;****
```

****接下来，我们创建一个实例，使**总是**指向相同的***base URL***，这样我们就避免了输入错误。****

```
****// This is the external service API url.
const baseURL = process.env.MASTERCARD_API_BASE_URL || '[https://mastercard.com/product/bill-pay/](https://developer.mastercard.com/product/bill-pay/)';
const axiosInstance = axios.create({ baseURL });****
```

****在上面的例子中，我们试图使用"[*process . env*](https://nodejs.org/dist/latest-v8.x/docs/api/process.html)*"*全局变量来定义外部提供者的"*const**【base URL】*。这是一个避免弄乱我们代码的好方法，可以选择查看如何使用模块😍。****

## ****修改请求标头****

****在发送请求内容之前，是时候执行我们的自定义操作了。****

```
****const apiSecret = process.env.API_SECRET || 'super-secret-value';axiosInstance.interceptors.request.use(
    request => ({
        ...request,
        headers: {
            Authorization: apiSecret,
        },
    }),
    error => Promise.reject(error),
);****
```

****另一个用例是在日志中记录所有通话(请始终存储匿名数据)。****

```
****axiosInstance.post(
    '/api/v2/company/incoming',
    {
        "amount": "4"
        "currency": "BTC"
    },
);****
```

# ****使用实例****

****我们将在新的[***Axios***](https://www.npmjs.com/package/axios)实例中使用的任何 *HTTP* 方法都将包含请求 [**的原始头，该请求连接或覆盖了 headers 对象中的***授权*](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Spread_syntax) "键。****

****此**将**应用于 *HTTP* 对象的**各种元素**，例如 body:****

```
****{
    ...request,
    body: {
        companyName: 'We love Axios, LLC',
    },
}****
```

# ****良好做法****

****由于*API*并不总是返回**非失败状态**，我们必须考虑错误情况。为了更好地理解**如何拦截和处理[***Axios***](https://www.npmjs.com/package/axios)中的响应错误**，请看一下[这个](https://www.npmjs.com/package/axios#handling-errors)。****

****但是这种情况**只适用于**如果我们有一个**响应拦截器**定义在我们的实例中，如果我们没有，我们不必担心。****

```
****const logger = console.log;axiosInstance.interceptors.response.use(
    ({ data }) => data, // Destructuring response body element
    ({ status }) => {
        const responseStatus = status || 500;
        logger.error(responseStatus);
        return responseStatus;
    },
);****
```

****如果你有兴趣看到更多真实的用例，不要犹豫，把它放在评论中，你只需要问！****