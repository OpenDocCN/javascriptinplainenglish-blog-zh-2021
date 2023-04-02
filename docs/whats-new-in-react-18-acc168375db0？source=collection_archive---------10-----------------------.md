# React 18 有什么新功能？

> 原文：<https://javascript.plainenglish.io/whats-new-in-react-18-acc168375db0?source=collection_archive---------10----------------------->

![](img/8933e4fa3854e49902a096a7f2866351.png)

[React 18 alpha 版本刚刚公布](https://reactjs.org/blog/2021/06/08/the-plan-for-react-18.html)。React 18 的主题是通过引入开箱即用的功能和由“并发渲染”提供动力的改进来消除 janky 用户体验，从而使 UI 更具性能。React 18 引入了最小的突破性变化。

我们来看看 React 18 的重大更新:

# 根 API

React 18 引入 Root API `ReactDOM.createRoot`。在 React 18 之前，我们使用`ReactDOM.render`向页面渲染一个组件。从 React 18 开始，我们将使用 ReactDOM.createRoot 创建一个根，然后将这个根传递给 render 函数。好消息是，你当前使用`ReactDOM.render`的代码仍然有效，但是，强烈建议开始过渡到`createRoot`，因为`render`从 18 开始将被标记为`deprecated`。电流`ReactDOM.render`仅被提供来缓解向反应 18 的转变。

反应 17:

```
import ReactDOM from 'react-dom';
import App from 'App';const container = document.getElementById('app');ReactDOM.render(<App />, container);
```

反应 18:

```
import ReactDOM from 'react-dom';
import App from 'App';const container = document.getElementById('app');// create a root
const root = ReactDOM.createRoot(container);//render app to root
root.render(<App />);
```

# 自动批处理(开箱即用，可选择退出):

批处理是将多个状态更新组合成一个以防止多次重新呈现的过程。以前，React 批处理发生在由 React 事件系统管理的单个事件回调中的状态更新，但是不批处理发生在事件之外的状态更新。

但是，使用自动批处理，所有更新，甚至在承诺、设置超时内的更新，都将被批处理。看看这个例子-

```
function handleClick() {
    console.log("=== click ===");
    setCount((c) => c + 1); // Does not re-render yet
    setFlag((f) => !f); // Does not re-render yet
    // React will only re-render once at the end (that's batching!) const timeoutCallback = () => {
      // Previously, batching didn't work inside timeouts, fetch, promises.
      // These two setStates caused re-render in React 17.
      // With React 18, these are now batched.
      setCount((c) => c + 1);
      setFlag((f) => !f);
    }; setTimeout(timeoutCallback, 1000);
  }
```

[完整示例见 codesanbox 链接](https://codesandbox.io/s/romantic-pare-efklq?file=/src/index.js:192-695)

**退出:**您可以使用`flushSync`退出自动配料

# 开始过渡(选择加入)

`startTransition`可以用来标记不需要紧急资源进行更新的 UI 更新。例如:当在一个 typeahead 域中键入时，会发生两件事——一个闪烁的光标显示正在键入的内容的视觉反馈，以及一个在后台搜索所键入数据的搜索功能。

向用户展示视觉反馈很重要，因此也很紧迫。搜索不是很紧急，因此可以标记为非紧急。这就是`startTransition`发挥作用的地方。

通过将非紧急的 UI 更新标记为“过渡”，React 将知道哪些更新应该优先，从而更容易优化渲染并消除陈旧的渲染。标记为非紧急`startTransition`的更新可能会被紧急更新中断，如点击或按键。

```
import { startTransition } from 'react'; // Urgent: Show what was typed
setInputValue(input);// Mark any state updates inside as transitions
startTransition(() => {
  // Transition: Show the results
  setSearchQuery(input);
});
```

**与去抖或 setTimeout 有什么不同？**

1.  与 setTimeout 不同，startTransition 会立即执行。setTimeout 有保证的延迟，而 startTransition 的延迟取决于设备的速度和其他紧急渲染。
2.  与 setTimeout 不同，startTransition 更新可以被中断，并且不会冻结页面。
3.  当用 startTransition 标记时，React 可以为您跟踪挂起状态。

# 如何移动反应 18？

```
npm install react@alpha react-dom@alpha
```

将 React.render 更改为 React.createRoot

```
const rootElement = document.getElementById("root");
ReactDOM.createRoot(<App />, rootElement).render(<App />);
```

[查看 React 工作组 GitHub 更新的完整列表](https://github.com/reactwg/react-18/discussions/categories/announcement)

[在你的收件箱里收到这样的文章](https://tinyletter.com/shrutikapoor)

*更多内容请看*[***plain English . io***](http://plainenglish.io)