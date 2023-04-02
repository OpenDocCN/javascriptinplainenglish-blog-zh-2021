# 预防—副作用挂钩

> 原文：<https://javascript.plainenglish.io/preact-side-effect-hooks-793583695a90?source=collection_archive---------12----------------------->

![](img/8b0e356f5ab50c709e50f2001e98c007.png)

Photo by [Louis Reed](https://unsplash.com/@_louisreed?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Preact 是一个前端 web 框架，类似于 react。

它比 React 小，也不复杂。

在本文中，我们将了解如何开始使用 Preact 进行前端开发。

# 使用效果

我们使用`useEffect`钩子来提交副作用。

例如，我们可以写:

```
import { render } from "preact";
import { useEffect } from "preact/hooks";function PageTitle({ title }) {
  useEffect(() => {
    document.title = title;
  }, [title]); return <h1>{title}</h1>;
}export default function App() {
  return (
    <div>
      <PageTitle title="hello world" />
    </div>
  );
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们有带`title`道具的`PageTitle`组件。

然后我们可以用`useEffect`钩子的第二个参数来观察它的值。

我们将`document.title`设置为`title`道具的值。

我们还可以在装载组件时使用它来监听事件，在卸载组件时解除事件处理程序的绑定。

例如，我们可以写:

```
import { render } from "preact";
import { useEffect, useState } from "preact/hooks";export default function App() {
  const [width, setWidth] = useState(0); function onResize() {
    setWidth(window.innerWidth);
  } useEffect(() => {
    window.addEventListener("resize", onResize);
    return () => window.removeEventListener("resize", onResize);
  }, []); return <div>Window width: {width}</div>;
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们用`width`状态来设置窗口的宽度。

`onResize`调用`setWidth`设置宽度。

在`useEffect`钩子中，我们调用`window.addEventListener`来监听`resize`事件。

当我们卸载组件时，我们返回回调来删除监听器。

然后我们在`div`中显示`width`。

现在，当我们调整窗口大小时，我们会看到宽度数字的变化。

# useLayoutEffect

`useLayoutEffect`与`useEffect`具有相同的签名，但是一旦组件不同，浏览器有机会绘制时，它就会启动。

# useErrorBoundary

当子组件抛出错误时，`useErrorBoundary`钩子让我们捕捉错误。

然后我们可以用这个钩子抓住它们。

例如，我们可以写:

```
import { render } from "preact";
import { useErrorBoundary } from "preact/hooks";const Child = () => {
  if (Math.random() < 0.5) {
    throw new Error("error");
  }
  return <p>child</p>;
};const Parent = ({ children }) => {
  const [error, resetError] = useErrorBoundary(); if (error) {
    return (
      <div>
        <p>{error.message}</p>
        <button onClick={resetError}>Try again</button>
      </div>
    );
  } else {
    return <div>{children}</div>;
  }
};export default function App() {
  return (
    <div>
      <Parent>
        <Child />
      </Parent>
    </div>
  );
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们有随机抛出错误的`Child`组件。

我们还有`Parent`组件，如果子组件中没有抛出错误，它就会呈现子组件。

如果子组件中有错误抛出，那么我们显示错误并显示一个按钮，当我们单击它时运行`resetError`功能。

`resetError`重新安装组件。

所以当我们在`Child`中出现错误时，我们可以点击重试来刷新子组件。

# 结论

我们可以使用`useEffect`钩子来产生副作用。

我们可以使用`useErrorBoundary`钩子来捕捉子组件引发的错误。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**