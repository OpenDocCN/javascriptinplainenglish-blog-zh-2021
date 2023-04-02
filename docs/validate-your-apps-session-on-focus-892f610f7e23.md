# 使用焦点事件监听器验证 React 应用程序的用户会话

> 原文：<https://javascript.plainenglish.io/validate-your-apps-session-on-focus-892f610f7e23?source=collection_archive---------5----------------------->

![](img/7ef19b9368c925f4b8dc6281e0680513.png)

我最近实现了一个特性，当用户在一段时间后返回页面时，它会检查用户的会话有效性。

当我们收到一些客户服务票，跟随着相同的旅程时，就有了对这个特性的需求。

1.  用户登录并正常使用网站
2.  在使用这个网站后，他们会换标签和做其他事情
3.  随着时间的流逝，它们又回到了我们的账上
4.  他们在站点中进行的触发 API 请求的第一次交互将用户注销

我们的网站使用 JWT 与我们的后端认证，他们在 1 小时后到期。JWT 存储在浏览器中，并随每个请求一起发送。成功的请求返回替换现有令牌的刷新令牌。这允许用户与我们的网站持续互动超过一个小时。

但是，如果他们离开网站超过 1 小时并返回，浏览器中的令牌将会过期。如果使用过期的令牌发出请求，我们将返回一个错误。当返回未授权的错误时，前端应用程序将自动注销用户。

结局是对的，但是体验不怎么样。我需要清理最后一步，用户应该在回到标签页后立即注销，而不是在他们提出新的请求后。

我对这个问题的完整解决方案如下。我将在本文的剩余部分一步一步地阅读每一部分。

我的例子使用了 [React](https://reactjs.org/) 、 [Redux Toolkit](https://redux-toolkit.js.org/) 和 [Reach Router](https://reach.tech/router/)

```
useEffect(() => {    
    window.addEventListener("focus", onFocus)    
    return () => {           
      window.removeEventListener("focus", onFocus)    
    }  
}, [])
```

当这个组件第一次加载时，我用我的 onFocus 函数在窗口上注册了一个[焦点事件列表器](https://developer.mozilla.org/en-US/docs/Web/Events)。

return 语句确保在删除组件时删除焦点事件侦听器。

```
const onFocus = () => dispatch(session.effects.checkSessionOnFocus(location))
```

这个函数触发一个状态动作，检查存储的令牌的有效性。我在我的状态中异步运行这个检查，因为在令牌过期的情况下，需要正确关闭一些第三方库。

为了方便客户，我将路由库提供的`location`对象传递给我的效果。这使我可以在他们退出时在应用程序中注册他们的位置。如果他们立即重新登录，我可以将他们重定向到他们原来的位置，而不是让他们返回到我的默认认证路由。

最后要考虑我的功能组件的位置。

```
<App>
  <Provider>
    <Router>
       <AuthenticatedRoutes>
         <WindowFocusHandler /> <-- has access to store and router
       </AuthenticatedRoutes>
    </Router>
  </Provider>
</App>
```

我想确保在呈现该组件时，我需要的所有资源都可用。对我来说，它必须进入我的商店、我的路由器和我的应用程序的认证部分。