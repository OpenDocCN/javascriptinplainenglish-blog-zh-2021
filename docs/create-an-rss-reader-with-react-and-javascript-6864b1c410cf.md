# 用 React 和 JavaScript 创建一个 RSS 阅读器

> 原文：<https://javascript.plainenglish.io/create-an-rss-reader-with-react-and-javascript-6864b1c410cf?source=collection_archive---------4----------------------->

![](img/a325c5fde77eb53fc74ef41c6062ac56.png)

Photo by [Bonnie Kittle](https://unsplash.com/@bonniekdesign?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个 RSS 阅读器。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app rss-reader
```

和 NPM 一起创建我们的 React 项目。

# 创建 RSS 阅读器

为了创建 RSS 阅读器，我们编写:

```
import React, { useState } from "react";export default function App() {
  const [rssUrl, setRssUrl] = useState("");
  const [items, setItems] = useState([]); const getRss = async (e) => {
    e.preventDefault();
    const urlRegex = /(http|ftp|https):\/\/[\w-]+(\.[\w-]+)+([\w.,@?^=%&amp;:\/~+#-]*[\w@?^=%&amp;\/~+#-])?/;
    if (!urlRegex.test(rssUrl)) {
      return;
    }
    const res = await fetch(`https://api.allorigins.win/get?url=${rssUrl}`);
    const { contents } = await res.json();
    const feed = new window.DOMParser().parseFromString(contents, "text/xml");
    const items = feed.querySelectorAll("item");
    const feedItems = [...items].map((el) => ({
      link: el.querySelector("link").innerHTML,
      title: el.querySelector("title").innerHTML,
      author: el.querySelector("author").innerHTML
    }));
    setItems(feedItems);
  }; return (
    <div className="App">
      <form onSubmit={getRss}>
        <div>
          <label> rss url</label>
          <br />
          <input onChange={(e) => setRssUrl(e.target.value)} value={rssUrl} />
        </div>
        <input type="submit" />
      </form>
      {items.map((item) => {
        return (
          <div>
            <h1>{item.title}</h1>
            <p>{item.author}</p>
            <a href={item.link}>{item.link}</a>
          </div>
        );
      })}
    </div>
  );
}
```

我们有存储我们输入的 RSS 提要 URL 的`rssUrl`状态。

而`items`状态存储我们将获得的提要条目。

然后我们定义了`getRSS`函数，当我们单击 submit 时获取 RSS 提要条目。

接下来，我们调用`e.preventDefault()`让我们做客户端提交。

然后我们检查`rssUrl`值是否是一个有效的 URL 字符串。

如果是，那么我们通过 CORS 代理向 RSS 提要发出一个带有`fetch`的 GET 请求。

我们使用 [allOrigins](https://allorigins.win/) API 向给定的提要发出跨域请求。

我们需要这样做，因为大多数提要都不允许从浏览器进行跨域通信。

我们从对象中获取`contents`属性。

然后我们用`DOMParser`实例的`parseFromString`方法解析 XML 字符串。

第一个参数是 XML 字符串。

第二个参数是内容类型字符串。

`feed`是具有整个 XML 树的 XML DOM 对象。

然后我们用`querySelectorAll`得到所有的`item`节点。

然后我们使用 spread 操作符将`items`节点列表扩展到一个数组中。

然后我们可以对它调用`map`来选择带有`querySelector`的`item`节点中的节点，并返回带有`innerHTML`值的对象。

我们调用`setItems`来设置`items`状态。

在那下面，我们有一个将`onSubmit`属性设置为`getRSS`的表单，让我们在点击类型为`submit`的输入时运行该函数。

在表单内部，我们有一个输入，将`onChange`属性设置为一个函数，该函数调用`setRssUrl`将输入值设置为`rssUrl`状态的值。

`e.target.value`有输入值。

`value`被设置为`rssUrl`,这样我们可以看到输入的值。

在表单下面，我们用`map`方法将`items`渲染成 div。

# 结论

我们可以用 React 和 JavaScript 轻松创建一个 RSS 阅读器。