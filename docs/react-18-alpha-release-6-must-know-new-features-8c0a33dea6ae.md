# React 18 Alpha 版本:6 个必须知道的新功能

> 原文：<https://javascript.plainenglish.io/react-18-alpha-release-6-must-know-new-features-8c0a33dea6ae?source=collection_archive---------5----------------------->

![](img/8933e4fa3854e49902a096a7f2866351.png)

React

*React 核心团队最近发布了 React 18 的 alpha 版本。这个版本更关注用户体验和内部架构的变化，包括对并发特性的适应。*

我们可以使用以下工具立即安装 React 18:

```
npm install react@alpha
```

和 ReactDOM，

```
npm install react-dom@alpha
```

**有什么新消息？**

# 1.新的根 API

我们通常会创建一个这样的根级 DOM，并附加 React 应用程序。这现在已经被废弃，现在被称为“遗留根 API”。

```
import React from 'react';
import ReactDOM from 'react-dom';const container = document.getElementById('root') ReactDOM.render(<App />, container);
```

相反，React18 中引入了一个新的`Root API`,如下所示:

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'App'const container = document.getEleementById('root')const root = ReactDOM.createRoot(container)root.render(<App />)
```

React 18 将同时搭载`Legacy Root API`和`New Root API`，以保持应用从 React 17(或更老版本)到 React 18 的平稳过渡。

**在传统根 API 上使用新的根 API**

新的 Root API 有很多改进:

**答:易于使用的水合物函数，因为我们可以将可选的布尔值直接传递给根。**

**传统根 API:**

```
import ReactDOM from 'react-dom'
import App from 'App'const container = document.getElementById('app');ReactDOM.hydrate(<App />, container)
```

**新的根 API:**

```
import ReactDOM from ‘react-dom’;
import App from 'App';const container = document.getElementById('root');const root = ReactDOM.createRoot(container, { hydrate: true });root.render(<App />);
```

点击阅读更多关于水合作用[的信息。](https://stackoverflow.com/questions/46516395/whats-the-difference-between-hydrate-and-render-in-react-16)

**b .渲染回调的改进:**

在遗留的根 API 中，我们可以传递一个渲染回调函数。这是一个匿名函数，在挂载根组件后呈现/运行。

```
import React from 'react';
import ReactDOM from 'react-dom';
import App from 'App'const container = document.getElementById('root')ReactDOM.render(<App />, container, function(){
    console.log('render only after initial component rendering')
})console.log('render at very last')
```

这种方法在新的根 API 中有所改变。React 团队建议不要使用回调，而是使用`requestIdleCallback`甚至本地`setTimeout`。

# 2.startTransition API

这是这个版本中引入的一个新 API，它有助于保持当前网页的响应性，同时能够进行大量的非阻塞 UI 更新。

`startTransition`的一个重要用例可能是当用户开始在搜索框中键入时。输入值必须立即更新，而搜索结果可能会等待几毫秒(如用户所预期的)。

这个 API 提供了区分快速更新和延迟更新的方法。

延迟的更新(即，从一个 UI 视图到另一个的转换)被称为**转换更新**。

对于像打字、悬停、点击这样的紧急更新，我们称之为道具/功能，通常是这样的:

```
setText(input)
```

对于非紧急或繁重的 UI 更新，我们可以将其包装在一个`startTransition` API 中，如下所示:

```
startTransition(() => { setText(input);});
```

# 3.严格效果进入严格模式

React18 现在将和`Strict Effects`模式一起发售`<StrictMode />`。就像严格模式一样，这将用于开发构建和改进的 DX。

当组件被包装在`Strict Effects`中时，React 将确保“有意”运行副作用两次，以检测异常行为/模式，这通常是使用`useEffect`安装和清理功能时的一个痛点。

运行两次效果有点像:*mount->unmount->mount*

# 4.SSR 改进

服务器端渲染(SSR)在这个版本中得到了架构上的革新，包括首次加载屏幕时间的改进。

在以前的版本(直到 React 17)中，SSR 必须先加载整个页面，然后才能开始对页面进行水合处理。

这在反应堆 18 中发生了变化。现在我们可以使用`<Suspense />`将 React 组件分成更小的块。

这个现在叫做`selective hydration`。

假设我们在屏幕上有 4 - 5 个不同的组件。现在封装一个组件将会在代码加载后开始合并这个特定的组件，并且不会阻塞页面的其余部分。

通过这种策略，页面中更重要的部分/组件可以首先变得交互(在极慢的连接下)，而其他组件将继续保持良好的用户体验。

```
<Layout>
  <Suspense fallback={<LoadingSpinner />}>
    <DelayedComponent />
  <Suspense />
<Layout />
```

在这里，`<Delayed />`组件将不会被解析，直到数据被获取。到那时，组件将回落到`<LoadingSpinner />`。

我们可以使用`<Suspense />`让几个组件在不同时间获取数据，保持重要组件的交互。

# 5.悬念列表

React 18 的另一个并发特性，它“编排”了大量数据提取组件在屏幕上出现的顺序。

一个`<SuspenseList />`用值 forward、backward 或 together 接受`revealOrder` prop。

```
<SuspenseList revealOrder="forwards">
  <Suspense fallback={<LoadingSpinner />}>
    <CardComponent id={1} />
  </Suspense>
  <Suspense fallback={<LoadingSpinner />}>
    <CardComponent id={2} />
  </Suspense>
 </SuspenseList>
```

这里，卡组件将向前显示(直到获取数据，将退回到 LoadingSpinner 组件)。类似地，`backwards`会以相反的顺序显示卡片，而 together 道具会“一起”渲染所有东西

# 6.useDeferredValue

`useDeferredValue`接受一个状态值，一个以毫秒为单位的超时，并返回该值的“延迟版本”。该值滞后于提供的超时秒数。

```
const deferredValue = useDeferredValue(value, { timeoutMs: 3000 });
```

这可能是文本输入字段的一个用例。文本输入会立即呈现在屏幕上。然而，`<CardLists />`文本属性接收一个`useDeferredValue`并返回一个滞后 3 秒的`defferedText`。

这导致延迟了卡片列表组件，同时仍然允许用户让文本字段感觉很快。

```
function App() {
  const [text, setText] = useState("");
  const deferredText = useDeferredValue(text, { timeoutMs: 2000 });   return (
    <div className="App">
    <input value={text} onChange={handleChange} /> <CardLists text={deferredText} />
    </div>
  );
 }
```

# 包扎

React 18 主要是关于并发特性，而不是一个成熟的并发模式(从 React 16 开始，这个模式已经被大肆宣传了)。这样做的原因是应用程序和库的作者可以有一个平稳的过渡，而不是任何突破性的变化。

React 18 目前是 alpha 版本，不适合量产。因此，API 可能会不断发展，直到它在今年年底(预计)达到稳定版本。

我们关于 React 18 的帖子到此结束。

## 我长期以来收集的一些重要资源:

1.  [https://chan.dev/posts/concurrent-mode-is-dead/](https://chan.dev/posts/concurrent-mode-is-dead/)
2.  https://dev.to/cassidoo/react-18-alpha-is-out-now-what-2apj
3.  【https://github.com/reactwg/react-18/discussions/4 
4.  [https://github.com/reactwg/react-18/discussions/37](https://github.com/reactwg/react-18/discussions/37)
5.  [https://JavaScript . works-hub . com/learn/react-18-is-here-what-new-9b46a？UTM _ source = dev _ to&UTM _ medium = blog _ xpost](https://javascript.works-hub.com/learn/react-18-is-here-whats-new-9b46a?utm_source=dev_to&utm_medium=blog_xpost)

希望你喜欢这篇文章！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)