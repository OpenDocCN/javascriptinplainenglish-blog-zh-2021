# 更新状态时如何减少重新渲染的次数？

> 原文：<https://javascript.plainenglish.io/how-to-reduce-the-number-of-re-renders-when-updating-states-cb283154ed4f?source=collection_archive---------9----------------------->

![](img/16b9db04e35a3b7bdf3f9074196ef6bf.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

每当 React 组件中的状态更新时，都会进行重新呈现。

这意味着当我们更新许多状态时，会有许多重新渲染的工作要做。

在本文中，我们将研究如何减少 React 组件中的重渲染次数。

# 如何减少重新渲染的次数？

我们可以通过减少更新状态的数量来减少重新渲染的次数。

例如，我们可以更新一个对象而不是状态，而不是多个状态。

为此，我们写道:

```
import { useEffect, useState } from "react";export default function App() {
  const [request, setRequest] = useState({
    loading: false,
    data: undefined
  }); const getData = async () => {
    setRequest((request) => ({ ...request, loading: true }));
    const res = await fetch("https://yesno.wtf/api/");
    const data = await res.json();
    setRequest((request) => ({ ...request, data }));
  }; useEffect(() => {
    getData();
  }, []); useEffect(() => {
    if (request.data) {
      setRequest((request) => ({ ...request, loading: false }));
    }
  }, [request]); return <div className="App">{JSON.stringify(request)}</div>;
}
```

我们有`request`状态，它有`loading`和`data`属性。

在`getData`函数中，我们调用`setRequest`来更新`request`状态对象的`loading`属性，方法是传入一个回调并返回一个新对象，它是`request`的副本，但是`loading`被设置为`true`。

在函数结束时，我们用新的值`data`再次调用`setRequest`。

此外，我们有一个检查`request.data`是否被设置的`useEffect`回调，并用一个返回`request`对象副本的回调调用`setRequest`，其中`loading`被设置为`false`。

另一种方法是创建我们自己的钩子来合并不同的状态对象属性。

例如，我们可以写:

```
import { useEffect, useState } from "react";const useMergeState = (initialState) => {
  const [state, setState] = useState(initialState);
  const setMergedState = (newState) =>
    setState((prevState) => ({ ...prevState, newState }));
  return [state, setMergedState];
};export default function App() {
  const [request, setRequest] = useMergeState({
    loading: false,
    data: undefined
  }); const getData = async () => {
    setRequest({ loading: true });
    const res = await fetch("https://yesno.wtf/api/");
    const data = await res.json();
    setRequest({ data });
  }; useEffect(() => {
    getData();
  }, []); useEffect(() => {
    if (request.data) {
      setRequest({ loading: false });
    }
  }, [request, setRequest]);return <div className="App">{JSON.stringify(request)}</div>;
}
```

我们创建了具有`setMergedState`函数的`useMergeState`钩子，该钩子调用`setState`函数，通过`setState`中的回调将`newState`合并到`prevState`中。

然后我们调用`App`中的`useMergeState`返回我们的状态和状态设置器函数。

现在，我们不需要向 state setter 函数传递一个回调来合并状态，而是将我们想要更改的属性传递给`setRequest`来更改属性。

在任一示例中，我们一次更新我们对象中需要的内容，而不是更新多个原始值。

# 结论

我们可以通过将状态放入对象并一次更新它们来减少 React 和 JavaScript 对组件的重新渲染次数。

*更多内容看*[***plain English . io***](https://plainenglish.io/)