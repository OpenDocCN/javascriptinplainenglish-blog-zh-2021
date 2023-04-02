# 让我们用 JavaScript 获取 API 来寻找口袋妖怪

> 原文：<https://javascript.plainenglish.io/lets-hunting-the-pokemons-w-fetch-api-javascript-1a95d30b0d10?source=collection_archive---------3----------------------->

![](img/e81a5b932641213fc33d88b5aafb1e01.png)

Photo by [Michael Rivera 🇵🇭](https://unsplash.com/@mykelgran?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

大家好！今天我列了一个口袋妖怪的清单。收集了这么多真的很兴奋。好吧，跟我来，我们去猎口袋妖怪。

现在我将向你展示如何从**口袋妖怪**获得口袋妖怪的数据。所以，在我们开始之前，我想和你分享一些关于 PokeAPI 和从 JavaScript 获取 API 函数的细节。

# 波基亚皮

根据官方网站，

> 你需要的所有神奇宝贝数据都在一个地方，
> 通过现代 RESTful API 轻松访问。

是的，PokeAPI 是口袋妖怪数据的提供者，基于 RESTful API。如果你访问官方网站，你会发现很多你可以利用的资源。

![](img/f6559f25a017e88ebe42ca9ac1ccbd7a.png)

# 获取 API

根据[文档](https://developer.mozilla.org/):

> 获取 API 提供了获取资源的接口(包括通过网络)。任何使用过`[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest)`的人都会觉得它很熟悉，但是新的 API 提供了一个更加强大和灵活的特性集。
> 
> Fetch 提供了对`[Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)`和`[Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)`对象(以及其他与网络请求相关的事物)的通用定义。这将允许它们在未来任何需要的地方使用，无论是服务工作者、缓存 API，还是其他处理或修改请求和响应的类似东西，或者任何可能需要您以编程方式生成响应的用例(即，使用计算机程序或个人编程指令)。
> 
> 它还定义了相关的概念，如 CORS 和 HTTP 源头语义，取代了它们在别处的单独定义。

# 实践

将以下代码复制粘贴到文本编辑器中。

打开你的 VS 代码中的`index.html`，运行到浏览器。还有 tada——我们抓住他们了！你可以在官方网站上了解更多。我将删除“参考”部分的链接。在我的下一篇文章中，我将尝试用 **Axios** 来使用这个 API(绝对是另一个资源 API)。

![](img/d41f5a0890da8e73067028f479934d37.png)

# 警惕！

如果你们来自印度尼西亚，想要支持我越来越多的写作，希望你们能从钱包里拿出一点来。你可以通过一些方式分享你的天赋，

## 萨韦里亚

[https://saweria.co/pandhuwibowo](https://saweria.co/pandhuwibowo)

![](img/0089e6c52b43886c90f7f853a7b8a73b.png)

## 特拉克特尔

[https://trakteer.id/goodpeopletogivemoney](https://trakteer.id/goodpeopletogivemoney)

![](img/d26e4901a3c5106b7c99a3c8a99d74a0.png)

# 参考

[](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) [## 获取 API-Web API | MDN

### 获取 API 提供了获取资源的接口(包括通过网络)。对…似乎很熟悉

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) [](https://pokeapi.co/) [## 波凯 API

### 一个开放的用于神奇宝贝数据的 RESTful API

pokeapi.co](https://pokeapi.co/) [](https://en.wikipedia.org/wiki/Pok%C3%A9mon) [## 神奇宝贝-维基百科

### 神奇宝贝，在日本也被称为口袋妖怪，是日本媒体特许经营的神奇宝贝公司，一个…

en.wikipedia.org](https://en.wikipedia.org/wiki/Pok%C3%A9mon) 

**给朋友打电话**

*朋友们你们好，支持我，让我还能写出其他有趣的文章。你可以买到原装的、自制的产品，当然也可以只在*[*@ beneteen*](http://twitter.com/beneteen)*或者*[*beneteen.com*](https://beneteen.com/)*买到本土品牌。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)