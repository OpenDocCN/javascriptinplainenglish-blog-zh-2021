# 用 React 和 JavaScript 创建一个搜索过滤器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-search-filter-app-with-react-and-javascript-5d05679f7315?source=collection_archive---------16----------------------->

![](img/0a1a23354f36916ca9bcabba42b128f3.png)

Photo by [Richard T](https://unsplash.com/@newhighmediagroup?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 React 和 JavaScript 创建一个搜索过滤器应用程序。

# 创建项目

我们可以用 Create React App 创建 React 项目。

要安装它，我们运行:

```
npx create-react-app search-filter
```

和 NPM 一起创建我们的 React 项目。

# 创建搜索过滤器应用程序

为了创建搜索过滤器应用程序，我们编写:

```
import { useState, useMemo } from "react";const images = [
  {
    url: "https://images.dog.ceo/breeds/affenpinscher/n02110627_4597.jpg",
    description: "affenpinscher"
  },
  {
    url: "https://images.dog.ceo/breeds/akita/Akita_Inu_dog.jpg",
    description: "akita"
  },
  {
    url: "https://images.dog.ceo/breeds/retriever-golden/n02099601_7771.jpg",
    description: "golden retriever"
  }
];export default function App() {
  const [keyword, setKeyword] = useState();
  const filteredImages = useMemo(() => {
    if (!keyword) {
      return images;
    }
    return images.filter(({ description }) => description.includes(keyword));
  }, [keyword]); return (
    <div className="App">
      <input value={keyword} onChange={(e) => setKeyword(e.target.value)} />
      <br />
      {filteredImages.map((fi) => {
        return (
          <div key={fi.description}>
            <img
              src={fi.url}
              alt={fi.description}
              style={{ width: 200, height: 200 }}
            />
            <p>{fi.description}</p>
          </div>
        );
      })}
    </div>
  );
}
```

我们有一个`images`数组，我们想用输入框搜索它。

在`App`组件中，我们添加了由 th `useState`钩子创建的`keyword`状态。

然后我们使用`useMemo`钩子来计算`filteredImages`值。

我们添加了一个回调函数来检查`keyword`的值。

如果没有`keyword`值，那么我们返回`images`数组。

否则，我们返回包含`keyword`的`description`的`images`数组项。

第二个参数有一个包含`keyword`变量的数组，因为我们想根据`keyword`值更新`filteredImages`。

`filtereddImages`仅随着`keyword`的变化而更新。

然后在`return`语句中，我们添加了输入框。

我们设置`onChange`处理程序来设置`keyword`状态。

然后我们用`map`方法渲染`filteredImage`项。

# 结论

我们可以用 React 的`useMemo`钩子和 JavaScript 轻松添加一个搜索过滤器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)