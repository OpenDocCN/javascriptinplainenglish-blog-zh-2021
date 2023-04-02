# 用模拟服务工作者和类型脚本模拟 API 请求

> 原文：<https://javascript.plainenglish.io/mocking-an-api-request-with-mock-service-worker-and-typescript-3a92fee48e11?source=collection_archive---------18----------------------->

![](img/95bc91d4dc0c5b4f8b0f0b340147eb04.png)

> 测试软件对于构建应用程序的开发周期至关重要。一个强大的测试套件给开发人员一种自由感，可以根据需要组织和重构代码库，而不用担心不知不觉地破坏了某些东西。

我使用 [Blogflow.io](https://github.com/CodyBontecou/blogflow.io/) 作为学习 TypeScript 的手段，同时构建一个工具来帮助在整个网络上自动发布博客帖子。

该应用程序的很大一部分需要集成第三方 API 来与诸如 Medium、Hashnode、Reddit 等服务进行通信。

很难测试第三方 API。我们不想每次运行测试套件时都碰到它们的端点。相反，我们选择模拟响应，假设给定特定的输入，API 将输出特定的响应。

[模拟服务工作者(MSW)](https://mswjs.io/) 提供了一种简单的方法来拦截这些 API 调用，这样我们的测试就不会触及第三方端点，也不会与实时数据交互。

## 设置和安装

我本打算带你去设置 MSW，但是他们提供了如此清晰的文档，我认为除了把你和他们联系起来之外，做任何事情都是不公平的。

如果你想看看我是如何在我的项目中与 dotenv 和 TypeScript 这样的包一起设置它的，欢迎你来查看我的 [repo](https://github.com/CodyBontecou/blogflow.io) 。

## 模拟媒体的 API

下面的所有内容都假设您遵循了[设置和安装](#installation)或者对 MSW 有所了解。

为了模仿 Medium 的创建 Post 请求，我在这里检查了他们的 API。

他们提供了一个示例响应:

```
HTTP/1.1 201 OK
Content-Type: application/json; charset=utf-8

{
  "data": {
    "id": "e6f36a",
    "title": "Liverpool FC",
    "authorId": "5303d74c64f66366f00cb9b2a94f3251bf5",
    "tags": ["football", "sport", "Liverpool"],
    "url": "https://medium.com/@majelbstoat/liverpool-fc-e6f36a",
    "canonicalUrl": "http://jamietalbot.com/posts/liverpool-fc",
    "publishStatus": "public",
    "publishedAt": 1442286338435,
    "license": "all-rights-reserved",
    "licenseUrl": "https://medium.com/policy/9db0094a1e0f"
  }
```

用 MSW 嘲讽这一点很简单。这几乎是一种复制粘贴:

```
//  src/mocks/handlers.ts

import { rest } from 'msw'

export const handlers = [
1\. rest.post('https://api.medium.com/*', (req, res, ctx) => {
    return res(
2\.    ctx.status(201),
3\.    ctx.json({
        data: {
          id: 'e6f36a',
          title: 'Liverpool FC',
          authorId: '5303d74c64f66366f00cb9b2a94f3251bf5',
          tags: ['football', 'sport', 'Liverpool'],
          url: 'https://medium.com/@majelbstoat/liverpool-fc-e6f36a',
          canonicalUrl: 'http://jamietalbot.com/posts/liverpool-fc',
          publishStatus: 'public',
          publishedAt: 1442286338435,
          license: 'all-rights-reserved',
          licenseUrl: 'https://medium.com/policy/9db0094a1e0f',
        },
      })
    )
  }),
]
```

1.  我设置这个处理程序来拦截对任何以`[https://api.medium.com/*](https://api.medium.com/*.)` [开头的 URL 的 POST 请求。](https://api.medium.com/*.)
2.  `*`代表一个通配符，意思是每当我的应用程序试图向一个以 https://api.medium.com/,开头的 URL 发送 POST 请求时，它都会拦截它并在 3 返回提供的响应。
3.  我们正在设置想要测试的 HTTP 响应状态代码。
4.  这是我们定义希望从 POST 请求返回的 JSON 响应的地方。

## 边缘案例

某些软件包需要额外的配置。这些主要是[笑话](https://jestjs.io/)问题，而不是 MSW，但是我在设置这个的时候遇到了它们。我决定记录下来，以防其他人像我一样遇到这些问题。

## [宠爱](https://github.com/motdotla/dotenv)

在`jest.config.ts`文件中，确保您有以下内容:

```
// jest.config.ts
module.exports = {
  setupFiles: ['dotenv/config'],
}
```

## **设置测试文件**

您需要设置您的 jest 测试来侦听、重置和关闭 MSW 服务器。

如果您使用 Create React App，您可能已经有了一个名为“src/setupTests.js”的文件。

否则，您需要自己创建一个设置文件。

然后，添加以下代码:

```
// src/setupTests.jsimport { server } from ‘./mocks/server.js’// Establish API mocking before all tests.beforeAll(() => server.listen())// Reset any request handlers that we may add during the tests,// so they don’t affect other tests.afterEach(() => server.resetHandlers())// Clean up after the tests are finished.afterAll(() => server.close())
```

这将设置您的 Jest 测试环境，以便在 Jest 生命周期的不同阶段启动 MSW 服务器、重置它并关闭它。

然后，您需要在“jest.config.ts”文件中添加一行:

```
// jest.config.ts
module.exports = {
    setupFilesAfterEnv: [‘<rootDir>/src/setupTests.ts’],
}
```

错误:ENOENT:没有这样的文件或目录，打开“文件”

我正在 Blogflow 阅读降价文件。在编写测试之前，我使用了如下相对路径:

```
const data = matter(readFile('./file.md'))
```

我的测试不喜欢这样，并抛出了错误`Error: ENOENT: no such file or directory, open "file"`

[这个](https://stackoverflow.com/a/59179782/6642089) Stackoverflow 的帖子解释了我需要使用`_dirname`。这段代码现在看起来像下面的代码片段。现在我的测试和代码如预期运行。

```
const data = matter(readFile(__dirname + '/file.md'))
```

## 结论

对我来说，这都是相当新的，但是我相信这种测试是有价值的。

一个直接的例子是模拟加载到组件中的响应。很难通过实时数据了解每个州。模拟某些会改变组件呈现方式的 HTTP 状态代码和响应对象要容易得多。

我希望本文能有所帮助。如果您在推特上有任何问题、评论或建议请告诉我 [@codybontecou](https://twitter.com/CodyBontecou)

*多内容于* [***普通英语中***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费周报在这里***](http://newsletter.plainenglish.io/) ***。***