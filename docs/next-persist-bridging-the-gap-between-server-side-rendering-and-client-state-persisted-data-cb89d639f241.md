# 用 next-persist 弥合 SSR 和客户端状态持久化数据之间的差距

> 原文：<https://javascript.plainenglish.io/next-persist-bridging-the-gap-between-server-side-rendering-and-client-state-persisted-data-cb89d639f241?source=collection_archive---------1----------------------->

![](img/ea0ab538c9559128c9297a820e2c2724.png)

***next-persist*** *是一个轻量级的* ***NPM 包*** *开发该包是为了简化存储和协调非关键、持久客户端数据的过程，同时保留 Next.js 提供的服务器端呈现和静态站点生成的好处。*

在我们深入了解 [**next-persist**](https://www.mostjs.org/) 如何融入开发人员的生态系统之前，我们需要谈谈 Next.js，这是一个由 Vercel 创建的前沿框架，它使开发人员能够轻松创建和部署应用程序，同时提供快速的加载时间。

Next.js 通过将服务器端(SSR)和客户端(CSR)呈现的最佳部分与静态站点生成(SSG)相结合，彻底改变了我们向客户端提供内容的方式。此外，通过抽象配置，如 webpack 和 babel，并结合 Vercel 的 CI/CD，启动并运行您的应用程序变得非常简单。

然而，伴随这些好处而来的是挑战，特别是对持久客户端数据的处理。

**什么是服务器端渲染(SSR)？**

服务器端呈现根据请求创建每个网页，能够存储和提供动态用户数据。这项技术意味着用户不会因为过多的客户端-服务器通信而体验到延迟。

SSR 的一些好处是，由于浏览器通常能够快速呈现服务器生成的 HTML，因此内容可以立即显示。除了要查看的 HTML 之外，浏览器不需要任何其他信息。搜索引擎优化(SEO)也没有问题，因为网络爬虫会直接查看来自服务器的 HTML。

SSR 的缺点是服务器为来自客户端的每个请求构建一个页面。服务器可能会做很多繁重的工作，因为它要加载每个页面，这可能很麻烦。另一个缺点是，虽然服务器总是为每个请求生成 HTML，但在内容交付网络(CDN)级别没有缓存内容。

## **什么是客户端渲染(CSR)？**

客户端呈现利用 JavaScript on demand 在浏览器中呈现每个 HTML 页面。CSR 应用程序不是为每条路线创建一个 HTML 页面，而是在浏览器中动态生成单独的路线。

这种方法的一些好处是，由 create-react-app (CRA)等工具生成的 Javascript 包可以驻留在 CDN 中。这意味着 HTML 页面在全球的边缘位置等待，这样用户就可以方便快捷地访问它们。此外，最初没有 web 服务器与之交互，最初的工作流只是在浏览器和 CDN 之间。

CSR 的一些缺点是，在完全处理完创建虚拟 DOM 的所有 Javascript 之前，您的浏览器将无法显示任何内容。此外，搜索引擎优化会有一些问题。网络爬虫只会看到一个包含 Javascript 包的空白 HTML 页面。

客户端呈现管理动态路由，无需在每次用户请求不同的路由时刷新页面。相比之下，SSR 可以在网站的任何路由的初始负载上显示完全填充的页面。

## **Next.js + SSR + SSG**

Next.js 专注于预渲染，本质上是 CSR 和 SSR 的结合。预先呈现的页面是一个 HTML 框架，它正在等待 AJAX/XHR 用数据重新水合。当获取页面时，内部路由是动态完成的，以利用客户端呈现的网站的优势。

预渲染包括 SSR 和静态站点生成(SSG)。与 SSR 非常相似，SSG 在构建时预渲染所有 HTML 页面，无需客户端渲染。

预渲染应用程序的一个优点是构建时间与用户交互无关，因此即使需要一段时间，用户体验也不会受到影响。一旦 SSG 页面建成，就可以在 CDNs 上使用，这意味着用户可以立即使用该页面。最后，因为 SSG 页面是由 CDN 提供的，所以没有对 web 服务器的请求，也不需要 web 服务器。

## **客户端持久数据**

在客户端持久数据出现之前，服务器是存储和访问用户数据的唯一方式。这意味着，每当应用程序必须使用/更新/共享用户数据时，整个应用程序都必须重新呈现给客户端。Cookies 是 Lou Montulli 在 web 早期创建的客户端持久数据的第一个实现。

每次请求时，Cookies 都会从服务器发送到浏览器。因为它们经常被来回发送，所以最好不要使用它们来存储大量数据，因为这会导致服务器和客户端之间的大量拥塞。

现代 web 浏览器利用 Web 存储 API，允许数据在浏览器中保存为键值对。分配给 localStorage 的空间更多，具体数量取决于您的浏览器。与 cookies 非常相似，localStorage 中的数据将跨会话保持不变。

此外，localStorage 不会在每个请求时都发送到服务器，web 服务器也不能直接写入 localStorage。

虽然 Next.js 非常适合 SSR 和 SSG，但是没有直观的方法来持久化客户端数据。这就是 **next-persist** 前来救援的地方！

## **进入下一个-持续**

那么， **next-persist** 到底是什么，它是如何绑定到 Next.js 和持久化客户端数据的呢？ **next-persist** 是一个轻量级 NPM 包，旨在简化存储和协调非关键、持久客户端数据的过程，同时保留 Next.js 提供的 SSR 和 SSG 的优势

以个人博客为例。在为用户提供某种动态持久化的同时获得 Next.js 的好处不是很好吗？所有这些都不需要担心额外的数据库管理系统的架构和成本？

现在你可以了！ **next-persist** 为您的动态同构 web 应用程序提供了一个简单的解决方案。只需导入 **next-persist** ，设置一个快速配置并整合我们的功能。我们完成剩下的工作，为您提供 SSR 和客户端持久数据的好处。

## **如何在你的 Next.js 应用中使用 next-persist**

首先，您必须在您喜欢的文本编辑器或 IDE 中创建一个 Next.js 应用程序。

安装下一个-从终端持续。

```
npm install next-persist
```

在 Next.js 应用的顶层将`<NextPersistWrapper />`导入到你的前端。

```
// _app.jsx
import PersistWrapper from 'next-persist/lib/NextPersistWrapper';
```

如果利用 localStorage 来持久化客户端状态:将`{ getStorage }`导入到您计划持久化的 reducer 中。

```
// yourReducer.jsx
import { getStorage } from 'next-persist'
```

如果利用 cookies 来保存客户端状态:

在 Next.js 应用程序的顶层将`{ getCookieProps }`导入到你的前端，同时将`{ getCookieStore }`导入到你计划保留的任何 reducer 中。

```
// _app.js
import { getCookieProps } from 'next-persist'

// yourReducer.js
import { getCookieStore } from 'next-persist'
```

## 配置

next-persist 需要一个简单的配置对象，允许您对我们的包的行为进行更改。首先，一个**必需的** `method`键，指示你想要使用哪种存储方法。第二，一个可选的`allowList`键按住一个对象。

```
//_app.js

  const npConfig = {
    method: 'localStorage' or 'cookies'
    allowList: {
      reducerOne: ['stateItemOne', 'stateItemTwo'],
      reducerTwo: [],
    },
  };
```

可以设置`allowList`键，仅允许特定的减速器将特定的状态存储到所选的存储方法中。`allowList`上的键必须与`combineReducers()`中减速器的键相对应。要只存储 reducer 的某些状态，可以将值设置为一个数组，将状态项的名称保存为字符串。

如果您希望存储 reducer 的所有状态，请将该值设置为空数组。如果没有提供 allowList，next-persist 会将所有 reducers 的所有状态存储到所选的存储方法中。

## 包装材料

`<PersistWrapper />`需要一个标签为`wrapperConfig`的道具，该道具将开发者在`_app`组件中声明的配置对象作为参数。

```
Example:

  import { Provider } from "react-redux";
  import store from "../client/store";
  import PersistWrapper from 'next-persist/lib/NextPersistWrapper';

  const npConfig = {
    method: 'localStorage'
    allowList: {
      reducerOne: ['stateItemOne', 'stateItemTwo'],
    },
  };

  const MyApp = ({ Component, pageProps }) => {
    return (
      <Provider store={store}>
        <PersistWrapper wrapperConfig={npConfig}>
          <Component {...pageProps} />
        </PersistWrapper>
      </Provider>
    );
  };

  export default MyApp;
```

## 还原剂

在每个减速器文件中，我们需要从`'next-persist'`导入`getLocalStore`或`getCookieStore`。

声明一个常量，并将调用`getLocalStore`或`getCookieStore`方法的计算结果的值赋给它。

`getLocalStore`或`getCookieStore`有两个参数:

*   字符串:保存在存储器中的缩减器密钥
*   一个对象:reducer 文件中声明的初始状态

将新声明的常量作为 state 的默认参数传递给 reducer。

```
Example:

  import * as types from '../constants/actionTypes';
  import { getLocalStore } from 'next-persist';
  // or
  // import { getCookieStore } from 'next-persist'

  const initialState = {
    // initialState goes here
    stateItemOne: true,
    stateItemTwo: 0,
    stateItemThree: 'foo',
  };

  const persistedState = getLocalStore('reducerOne', initialState);
  // or
  // const persistedState = getCookieStore('reducerOne', initialState);

  const firstReducer = (state = persistedState, action) => {
    // switch case logic in here
    switch (action.type) {
    default:
      return state;
    }
  };

  export default firstReducer;
```

## 饼干

利用 cookie 存储方法提供了利用客户端状态和`getInitialProps`的好处。但是，由于 cookie 大小的限制，它不能用于存储大量数据。

在这个例子中，我们调用`getInitialProps`中的`getCookieProps`，它将返回一个包含所有持久状态值的对象，保存在它们的 reducer 名称的键下。

```
Example:

  MyApp.getInitialProps = async ({ ctx }) => {
    const cookieState = getCookieProps(ctx);
    return {
      pageProps: cookieState,
    };
  }

  export default MyApp;
```

## 结论

感谢您的阅读。我们希望这对您有所帮助。如果你在应用中使用 next-persist，请在评论中告诉我们你的想法。要了解更多关于 **next-persist** 的信息，请访问我们的[网站](https://www.mostjs.org/)。

## 贡献的

如果你愿意为 next-persist 做贡献，请[叉本回购](https://github.com/oslabs-beta/next-persist)。将您的更改提交到命名良好的功能分支，然后打开一个“拉”请求。我们感谢您对这个开源项目的贡献！

## 保持器

*   朱敏瀚:[GitHub](https://github.com/darthchu)/[LinkedIn](https://www.linkedin.com/in/brianwilliamchu/)
*   克里斯托弗·博瑟曼:[GitHub](https://github.com/christopherpbosserman)/[LinkedIn](https://www.linkedin.com/in/christopherpbosserman/)
*   格雷格·莱文-罗泽万恩:[GitHub](https://github.com/grishaLR)/[LinkedIn](https://www.linkedin.com/in/gregory-levine-rozenvayn/)
*   马修·萨尔瓦多: [GitHub](https://github.com/mjsalvador) / [LinkedIn](https://www.linkedin.com/in/matthewsalvador/)

[**next-persist**](https://www.mostjs.org/) 是在 [OSLabs](https://github.com/open-source-labs) 的支持下打造的

*由* [***【朱敏瀚】***](http://medium.com/@darthchu)*[***博瑟曼***](https://medium.com/@christopherpbosserman)*[***格雷戈里-莱文***](http://medium.com/@grisha617)**

****更多内容请看*[***plain English . io***](https://plainenglish.io/)***