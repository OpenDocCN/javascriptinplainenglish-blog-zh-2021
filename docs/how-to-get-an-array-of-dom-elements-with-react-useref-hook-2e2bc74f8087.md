# 如何用 React useRef 钩子获得 DOM 元素的数组

> 原文：<https://javascript.plainenglish.io/how-to-get-an-array-of-dom-elements-with-react-useref-hook-2e2bc74f8087?source=collection_archive---------17----------------------->

![](img/71da4a9867d97ad9bd64d995536756cf.png)

Photo by [Jeffrey F Lin](https://unsplash.com/@jeffreyflin?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望在 React 组件中为呈现的 DOM 元素数组分配一个 ref。

在本文中，我们将看看如何用 React `useRef`钩子获得一组 DOM 元素。

# 创建一个引用数组，并将其存储在一个引用中

我们可以创建一个引用数组，并将它存储在一个引用数组中。

例如，我们可以写:

```
import React, { useEffect, useRef } from "react";const arr = ["left", "right"];
export default function App() {
  const refs = useRef(arr.map(() => React.createRef())); useEffect(() => {
    refs.current[0].current.focus();
  }, []); return (
    <div>
      {arr.map((el, i) => (
        <p key={i}>
          <input ref={refs.current[i]} value={el} onChange={() => {}} />
        </p>
      ))}
    </div>
  );
}
```

我们用`arr.map`回调函数调用`useRef`钩子，将`arr`映射到我们用`React.createRef`创建的 refs 数组。

然后我们有一个`useEffect`回调，当`App`挂载时，它调用`refs.current[0].current.focus()`来关注第一个元素。

最后，我们通过将`ref`属性的值分配给`refs.current[i]`来分配`map`回调中的引用。

现在，当我们安装组件时，我们应该看到第一个输入元素获得了焦点。

或者，我们可以使用`useMemo`钩子通过写入来缓存引用:

```
import React, { useEffect, useMemo } from "react";const arr = ["left", "right"];
export default function App() {
  const refs = useMemo(() => arr.map(() => React.createRef()), []); useEffect(() => {
    refs[0].current.focus();
  }, []); return (
    <div>
      {arr.map((el, i) => (
        <p key={i}>
          <input ref={refs[i]} value={el} onChange={() => {}} />
        </p>
      ))}
    </div>
  );
}
```

我们以同样的方式创建引用，但是我们用`useMemo`包装回调以缓存创建的引用。

然后，我们分配引用并使用它们，就像我们在前面的例子中所做的那样。

# 结论

我们可以用`createRef`函数和`useMemo`或`useRef`钩子创建一个 refs 数组来存储它们。

*更多内容请看*[***plain English . io***](http://plainenglish.io)