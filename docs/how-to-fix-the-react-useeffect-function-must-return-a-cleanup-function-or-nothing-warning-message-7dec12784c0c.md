# 如何修复 React 的“useEffect 函数必须返回一个清理函数或者什么都不返回”警告消息？

> 原文：<https://javascript.plainenglish.io/how-to-fix-the-react-useeffect-function-must-return-a-cleanup-function-or-nothing-warning-message-7dec12784c0c?source=collection_archive---------13----------------------->

![](img/d08f14a8cec183147a4b8710fff01d84.png)

Photo by [Raimond Klavins](https://unsplash.com/@raimondklavins?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果在我们的`useEffect`钩子中有异步函数，我们可能会在控制台中得到“useEffect 函数必须返回一个清理函数或者什么也不返回”的警告。

在本文中，我们将看看如何修复这个警告。

# 将异步函数移出 useEffect 挂钩

为了纠正这个警告，我们不应该在第一个参数中使用异步函数作为回调函数。

`useEffect`在第一个参数中需要一个同步函数。

因此，与其写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [posts, setPosts] = useState({}); useEffect(async () => {
    try {
      const response = await fetch(`https://www.reddit.com/r/react.json`);
      const json = await response.json();
      setPosts(json.data.children.map((it) => it.data));
    } catch (e) {
      console.error(e);
    }
  }, []); return (
    <div className="App">
      <div>{JSON.stringify(posts)}</div>
    </div>
  );
}
```

我们写道:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [posts, setPosts] = useState({});const getPosts = async () => {
    try {
      const response = await fetch(`https://www.reddit.com/r/react.json`);
      const json = await response.json();
      setPosts(json.data.children.map((it) => it.data));
    } catch (e) {
      console.error(e);
    }
  }; useEffect(() => {
    getPosts();
  }, []); return (
    <div className="App">
      <div>{JSON.stringify(posts)}</div>
    </div>
  );
}
```

我们用 promise 代码创建了一个新的`getPosts`函数，而不是使用异步函数作为`useEffect`钩子的回调函数。

我们也可以在`useEffect`回调函数中定义异步函数。

所以我们也可以写:

```
import React, { useEffect, useState } from "react";export default function App() {
  const [posts, setPosts] = useState({}); useEffect(() => {
    const getPosts = async () => {
      try {
        const response = await fetch(`https://www.reddit.com/r/react.json`);
        const json = await response.json();
        setPosts(json.data.children.map((it) => it.data));
      } catch (e) {
        console.error(e);
      }
    }; getPosts();
  }, []); return (
    <div className="App">
      <div>{JSON.stringify(posts)}</div>
    </div>
  );
}
```

如果我们只使用这个函数一次，我们可以把它放在`useEffect`回调函数中。

# 结论

我们可以通过单独定义一个异步函数并使用它来代替传入一个异步函数作为`useEffect`钩子的回调，从而很容易地解决“useEffect 函数必须返回一个清理函数或者什么都不返回”的问题。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)