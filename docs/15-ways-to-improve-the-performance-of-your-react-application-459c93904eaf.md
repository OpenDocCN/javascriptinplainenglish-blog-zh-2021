# 提高 React 应用程序性能的 15 种方法

> 原文：<https://javascript.plainenglish.io/15-ways-to-improve-the-performance-of-your-react-application-459c93904eaf?source=collection_archive---------6----------------------->

开发高性能应用程序必须遵循的原则。

![](img/66f1e8929005214202313710922f6214.png)

Banner Image inspired from Canva

# 入门指南

我不会花太多时间来介绍这个话题。因此，让我们直接进入提高性能的方法。

# **使用 onBlur 从输入值**更新状态

比起直接从 input 元素更新 state 或 redux store，我更喜欢使用 onBlur 属性而不是 onChange。onChange 严重地造成了许多性能问题，尤其是在与 redux 一起使用时，所以要尽量避免。

# 静态组件的用户纯组件

如果你确定任何特定的子组件是静态的，或者不会频繁地改变，那么就把它作为一个纯组件。这避免了荒谬地重新呈现甚至不需要的特定组件。

# 使用记忆优先摇晃树

内存化意味着缓存结果以提高性能。使用 useMemo 钩子或其他方式来记忆组件基本上就是在虚拟 DOM 中缓存组件节点，并且只在特定组件的状态或属性改变时更新。这在处理大型列表集时非常有效。我更喜欢使用列表中的每一项，这样 React DOM 就可以执行树抖动。

# 在 React 挂钩或 componentshouldUpdate 方法中使用条件呈现

无论是使用类组件还是功能组件，都要确保在 useEffect 或 componentShouldUpdate 方法中提供有条件的重新呈现。大多数时候，我们会忘记处理它，即使我们知道这可能会导致不必要的重新渲染。

# 在处理大量图像时使用延迟加载

我已经报道了一个关于 Next.js 的新图像组件的故事。我不知道我们如何在 React Native 中使用它，但在 React 中，总是喜欢延迟加载，特别是当你的应用程序有大量文件渲染时。

[](https://medium.com/nerd-for-tech/a-perfect-way-to-load-images-in-react-f730d00119bf) [## 在 React 中加载图像的完美方式

### 在下一个 JS 中使用图像，缓存和延迟加载——正确的方法

medium.com](https://medium.com/nerd-for-tech/a-perfect-way-to-load-images-in-react-f730d00119bf) 

# 更喜欢分页，而不是获取所有数据

这很容易理解，但是我们仍然避免使用这种现象。提供分页对你的产品的商业方面有影响，因为你的用户很少去第 3 或第 4 页，除非你的网站是亚马逊。但是，快速加载 10 个项目比在 10-20 秒内加载 20 -30 个项目要好得多。此外，获取前 10 项比获取所有项要快得多。

# 首选 GraphQL 以避免过度获取数据

当我在开发比特币和其他货币的图表时，我明白了为什么我们的图表速度慢且有点滞后的主要问题。这是因为我们过度获取数据。对于我来说，过度获取前端不需要的键值对毫无意义。无论如何，我们最终对 REST 端点进行了 GraphQL 查询，这将我们的应用程序性能提高了 40%。这太棒了。

[](/calling-rest-api-inside-graphql-queries-e715c0f2da44) [## 在 GraphQL 查询中调用 REST API

### 您不需要将我们的后端从 REST 切换到 GraphQL，而是在 Graph QL 中获取 REST 查询。

javascript.plainenglish.io](/calling-rest-api-inside-graphql-queries-e715c0f2da44) 

# 避免重新渲染，这是一个常见的错误

重新渲染或不必要的渲染在 React 应用程序中很常见。我不会详细介绍这一点，因为这是一个常见的错误，互联网上有大量的文章可供学习。

# 小心内存泄漏，尤其是在 React Native 中

这很重要。大多数情况下，当您的模拟器在开发过程中关闭时，这是因为内存泄漏。当 JavaScript 函数填满堆堆栈或执行无限循环时，就会发生内存泄漏。因此，请确保结束 while 或 for 循环，或者从您在任何组件中调用的函数返回一些值。

# 如果使用 Axios，请使用 cancel token 属性来避免过度调用 API

我会报道一个关于此事的完整详细的新故事。Axios 确实提供了一种取消令牌的方法来取消 API 请求，以防您已经创建了一个 API。当你想频繁地调用 API 时，这是一个优化且有用的过程。例如用于搜索输入或过滤输入等。

如果你想了解更多信息:

[](https://github.com/axios/axios#cancellation) [## axios/axios

### 基于 Promise 的浏览器和 node . js HTTP 客户端新的 axios docs 网站:单击此处从…

github.com](https://github.com/axios/axios#cancellation) 

# 在 useState 中使用回调函数，而不是调用多个 setState

让我给你举个例子:

```
const [ formValue, setFormValues ] = useState({
  email: String,
  password: String,
  username: String,
  rememberMe: Boolean
});function handleFormChange(e){
  const name = e.target.name;
  const val = e.target.value;
  setFormValues(prev => ({...prev, [name]: val }))
}
```

这是使用 setState 函数中的回调来更新状态的最佳方式，而不是为每个要更新的状态值调用不同的 set state。所以确保你以适当的方式使用了**使用状态**钩子。

# 尽量不要给 useEffect 或 componentDidMount 以及构造函数方法施加太大的压力

大多数时候，我们更喜欢在 componentDidMount 或 useEffect 钩子中进行 API 调用。这是一个好主意，但是有时候，一个组件需要 3-4 个 API 请求。在这种情况下，我们的使用效果或组件已经超负荷或压力过大。即使您想发出 3-4 个 API 请求，也最好使用`**Axios.all**`方法，同时向用户显示一些数据获取指示器。以优先的方式按照特定的顺序进行 API 调用总是一个好方法。

# 在 React Native 中，首选 FlatList 或 SectionList，而不是 map 函数

我已经讲述了一个关于如何将 FlatList 用于记忆的项目以及惰性加载和分页属性的详细故事。这对 React 原生应用的性能非常重要。使用 **ScrollView** 组件而不是 FlatList 确实会对性能领域产生影响。

# 测量页面呈现时间

我还在搜索第三方工具来测量 React 和 React 原生应用中每个页面的页面渲染时间。这对于分析应用程序的整体性能非常有帮助。了解每一个页面在初始呈现时所花费的时间，包括那些 API 调用的时间，将肯定有助于我们提高页面速度，方法是首先对最重要的组件进行优先级排序，并按照特定的顺序进行那些 API 调用。

# 最后，一定要提供映射项的键

我们知道 React 使用虚拟 DOM 来区分或比较节点，React 使用键值。如果您忘记提供密钥，那么所有项目都将被视为相同，React 将无法区分。这使得虚拟 DOM 很难跟踪这些变化。不使用**键**来区分虚拟 DOM 和实际 DOM 意味着您没有以最有效的方式使用虚拟 DOM 属性，这又会导致性能问题。

# 结论

提高应用程序的性能并不是一件容易的事情。这确实需要大量的知识和对框架如何工作的理解。我强烈建议选择贵公司的绩效任务，因为它可以提高你的知识。

我将在以后的文章中介绍更多与性能相关的内容。因此，要获得更新或友好的链接，您可以订阅我们的周刊。

```
[**Weekly magazine**](http://www.ihatereading.in/subscribe)
```

[](/serverless-function-in-next-js-3cd0d22ab983) [## 下一个 JS 中的无服务器功能

### 下一篇 JS 详细了解无服务器功能

javascript.plainenglish.io](/serverless-function-in-next-js-3cd0d22ab983) [](https://medium.com/nerd-for-tech/best-redux-architecture-explained-in-5-minutes-9b993f0169c0) [## 5 分钟解释最佳 Redux 架构。

### 你每次都应该遵循的 Redux 架构。可扩展、高度可扩展且易于随时更换…

medium.com](https://medium.com/nerd-for-tech/best-redux-architecture-explained-in-5-minutes-9b993f0169c0) [](/the-easiest-way-to-manage-token-and-created-protected-pages-in-frontend-c60db33f1921) [## 管理令牌和创建的受保护页面的最简单方法

### 避免在 Redux 或 LocalStorage 中存储身份验证令牌，而是使用 Cookies。

javascript.plainenglish.io](/the-easiest-way-to-manage-token-and-created-protected-pages-in-frontend-c60db33f1921) 

## 进一步阅读

[](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) [## 帮助您在 React 中更快开发的 5 种工具和实践

### React 工具、技巧和最佳实践将帮助您更快地构建应用

javascript.plainenglish.io](/5-tools-practices-to-help-you-develop-faster-in-react-b884c1b20fc2) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。***