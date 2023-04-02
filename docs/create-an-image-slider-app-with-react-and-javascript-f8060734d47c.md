# 用 React 和 JavaScript 创建一个图像滑块应用程序

> 原文：<https://javascript.plainenglish.io/create-an-image-slider-app-with-react-and-javascript-f8060734d47c?source=collection_archive---------13----------------------->

![](img/f61544eee27863d5f21847ff9cc4150e.png)

Photo by [Nathan Anderson](https://unsplash.com/@nathananderson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个图像滑块应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app image-slider
```

和 NPM 一起创建我们的 React 项目。

# 创建图像滑块应用程序

为了创建图像滑块应用程序，我们编写:

```
import { useState } from "react";const images = [
  "https://i.picsum.photos/id/1/200/300.jpg?hmac=jH5bDkLr6Tgy3oAg5khKCHeunZMHq0ehBZr6vGifPLY",
  "https://i.picsum.photos/id/2/200/300.jpg?hmac=HiDjvfge5yCzj935PIMj1qOf4KtvrfqWX3j4z1huDaU",
  "https://i.picsum.photos/id/3/200/300.jpg?hmac=o1-38H2y96Nm7qbRf8Aua54lF97OFQSHR41ATNErqFc"
];export default function App() {
  const [index, setIndex] = useState(0); const next = () => {
    setIndex((i) => (i + 1) % images.length);
  }; const prev = () => {
    setIndex((i) => (i - 1) % images.length);
  }; return (
    <div className="App">
      <button onClick={prev}>&lt;</button>
      <img src={images[index]} alt="" />
      <button onClick={next}>&gt;</button>
    </div>
  );
}
```

在`images`数组中我们有 3 个图像 URL。

在`App`组件中，我们有由`setIndex`设置的`index`状态。

我们将其初始值设置为 0。

然后我们用`next`和`prev`函数通过增加 1 来设置索引，然后通过除以`images.length`得到余数。

这将获取下一个要显示的图像的索引。

`prev`是类似的，除了我们减去 1 而不是增加，以获得前一个图像的索引。

到达最后一张图片后，我们将返回第一张图片，并单击“下一页”按钮。

在到达第一幅图像后，我们显示最后一幅图像，并单击“上一页”按钮。

然后我们返回带有按钮的 JSX，当我们点击它们时调用`next`和`prev`函数。

我们在`img`元素中显示图像。

我们还可以通过编写以下内容来制作一个自动移动到下一张幻灯片的图像滑块:

```
import { useEffect, useState } from "react";const images = [
  "https://i.picsum.photos/id/1/200/300.jpg?hmac=jH5bDkLr6Tgy3oAg5khKCHeunZMHq0ehBZr6vGifPLY",
  "https://i.picsum.photos/id/2/200/300.jpg?hmac=HiDjvfge5yCzj935PIMj1qOf4KtvrfqWX3j4z1huDaU",
  "https://i.picsum.photos/id/3/200/300.jpg?hmac=o1-38H2y96Nm7qbRf8Aua54lF97OFQSHR41ATNErqFc"
];export default function App() {
  const [index, setIndex] = useState(0); const next = () => {
    setIndex((i) => (i + 1) % images.length);
  }; useEffect(() => {
    const timer = setInterval(() => {
      next();
    }, 1000);
    return () => {
      clearInterval(timer);
    };
  }, []);
  return (
    <div className="App">
      <img src={images[index]} alt="" />
    </div>
  );
}
```

除了我们移除了`prev`函数之外，大部分代码都是相同的。

我们还添加了带有回调的`useEffect`钩子，每秒钟用`setInterval`调用`next`。

当我们卸载组件时，我们返回一个回调来调用`clearIntveral`清除计时器。

第二个参数中的空数组让我们仅在挂载组件时运行`useEffect`回调。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个图像滑块。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)