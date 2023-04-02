# 关于跨来源资源共享你需要知道的一切(CORS)

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-cross-origin-resource-sharing-cors-ca4385f81076?source=collection_archive---------11----------------------->

## 通过例子了解 CORS。

![](img/5fc52d463bc1b2e054d5a6a2547a61e2.png)

Photo by [Emile Perron](https://unsplash.com/@emilep?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

跨源资源共享(CORS)允许我们在网络上共享资源。根据 Wiki，跨源资源共享是一种机制，它允许从提供第一资源的域之外的另一个域请求网页上的受限资源。这可能令人沮丧，有时会阻碍对某些资源的访问。

更简单的解释是，它允许共享信息和资源，比如从 localhot:3000 到 localhost:5000。所以，在其他时候，我们想要做的是，我们设置跨源资源共享(CORS)来允许来自特定 URL 的请求，就是这样。

为了设置和配置跨源资源共享(cors)，我们将使用一个名为 CORS 的包，它允许我们设置请求的源。

## **安装跨产地资源共享(CORS)**

使用 npm

```
npm install cors
```

该命令将把 cors 安装到我们项目的依赖项中，并使它们在我们的应用程序中可用。

出于本教程的考虑，我们将使用 express.js 框架来获得 cors 的核心功能。假设服务器被配置为只允许来自某个 URL 的请求，比如说 [http://127.0.0.5500](http://127.0.0.5500) ，而我们想要从一个 URL 访问相同的信息，比如说 [https://localhost:8080](https://localhost:8080) 。

我们可以配置 cors，并从它们服务的 [http://127.0.0.5500](http://127.0.0.5500) 设置来源，并允许任何请求。

```
const express = require('express');
const app = express()
const cors = require('cors')
const port = 5000
app.use(cors({
    origin: '[https://loclhost:8080'](https://loclhost:8080')
}))app.get('/user', (req, res) => {
    res.json({ user: 'John Philip', role: 'Software Developer', age: '21' });
})app.listen(port, () => {
    console.log(`App is running on port ${port}`);
});
```

上面的例子显示了我们如何设置 cors 只允许来自我们提供给它的源的请求。当我们想要设置 cors 来允许来自任何其他 URL 的请求而不阻止请求时，情况又会如何呢？

## **允许来自所有 URL 的请求**

我们可以根据请求来自的 URL 设置 cors 不阻止任何请求。

```
const express = require(‘express’);
const app = express()
const cors = require(‘cors’)
const port = 5000
app.use(cors({
 origin: ‘*’
}))app.get(‘/user’, (req, res) => {
 res.json({ user: ‘John Philip’, role: ‘Software Developer’, age: ‘21’ });
})app.listen(port, () => {
 console.log(`App is running on port ${port}`);
});
```

当你设置一个星形的原点时，你将允许 cors 接受来自任何 URL 的请求，并且不会阻止来自其他 URL 的访问。

cors 的另一个非常重要的用例是，我们可以配置它来接受某些 HTTP 方法或动词，比如 GET、PUT、DELETE 和 POST。默认情况下，cors 被设置为允许所有可用的 HTTP 动词。

## **配置跨源资源共享(CORS)到 HTTP 方法**

假设我们想配置 cors 只接受 POST 和 GET 方法。对于这种情况，我们将需要提供方法作为第二个参数，其中包含我们希望允许的一组方法。

```
const express = require(‘express’);
const app = express()
const cors = require(‘cors’)
const port = 5000
app.use(cors({
 origin: ‘*’,
 methods: [‘GET’, ‘POST’]
}))app.PUT(‘/user’, (req, res) => {
 res.json({ user: ‘John Philip’, role: ‘Software Developer’, age: ‘21’ });
})app.listen(port, () => {
 console.log(`App is running on port ${port}`);
});
```

从上面的片段来看，我们只接受 GET 和 POST 请求。除了我们已经包括的方法之外，其他 HTTP 方法将被 CORS 阻止。

在我们使用 PUT 发出请求的情况下，CORS 将阻止这个请求，因为它没有配置为接受这样的请求。

## **设置跨源资源共享(CORS)以允许 cookie**

跨源资源共享(CORS)默认情况下不允许 cookies，并将始终阻止它们。要配置我们的应用程序允许 cookie，我们需要设置跨源资源共享(CORS)来允许 cookie。

```
const express = require(‘express’);
const app = express()
const cors = require(‘cors’)
const port = 5000
app.use(cors({
 origin: ‘*’,
 credentials: true
}))app.get(‘/user’, (req, res) => {
 res.json({ user: ‘John Philip’, role: ‘Software Developer’, age: ‘21’ });
})app.listen(port, () => {
 console.log(`App is running on port ${port}`);
});
```

要允许 cookies，我们需要提供凭证的另一个参数，并将其设置为 true。

## **最后的想法**

跨源资源共享(CORS)对于学习和获得其潜在用途非常重要。

感谢您通读这篇文章，希望对您有所帮助。如果你认为其他人可能会从这篇文章中受益，为什么不与他人分享呢？

## **延伸阅读:**

[](/5-programming-languages-you-can-bet-on-to-land-you-a-job-c1e212d6e302) [## 5 种编程语言可以让你找到工作

### 利用这些语言获得你的第一份工作。

javascript.plainenglish.io](/5-programming-languages-you-can-bet-on-to-land-you-a-job-c1e212d6e302) [](/open-advice-for-developers-applying-for-their-first-job-e94e804db613) [## 对申请第一份工作的开发人员的公开建议

### 开发人员申请第一份工作的注意事项。

javascript.plainenglish.io](/open-advice-for-developers-applying-for-their-first-job-e94e804db613) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)