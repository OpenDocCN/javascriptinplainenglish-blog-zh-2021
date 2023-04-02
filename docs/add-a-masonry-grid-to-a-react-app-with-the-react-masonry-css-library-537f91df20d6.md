# 使用 react-masonry-css 库向 React 应用程序添加砖石网格

> 原文：<https://javascript.plainenglish.io/add-a-masonry-grid-to-a-react-app-with-the-react-masonry-css-library-537f91df20d6?source=collection_archive---------7----------------------->

![](img/8d57036fe491fc2a627780adee74e5b7.png)

Photo by [Irina Grigoraş](https://unsplash.com/@irinagrigorash?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可以使用 react-masonry-css 库将砖石网格添加到 React 应用程序中。

在本文中，我们将看看如何使用这个库来添加砖石网格。

# 装置

我们可以通过运行以下命令来安装该软件包:

```
npm install react-masonry-css
```

# 添加网格

安装软件包后，我们通过编写以下内容来添加样式:

`styles.css`

```
.my-masonry-grid {
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  margin-left: -30px;
  width: auto;
}
.my-masonry-grid_column {
  padding-left: 30px;
  background-clip: padding-box;
}.my-masonry-grid_column > div {
  background: yellow;
  margin-bottom: 30px;
}
```

添加背景色并使项目以 flexbox 布局显示。

然后我们可以通过写来使用它:

`App.js`

```
import React from "react";
import Masonry from "react-masonry-css";
import "./styles.css";let items = [
  { id: 1, name: "one" },
  { id: 2, name: "two" },
  { id: 3, name: "three" },
  { id: 4, name: "four" },
  { id: 5, name: "five" }
];items = items.map(function (item) {
  return <div key={item.id}>{item.name}</div>;
});const breakpointColumnsObj = {
  default: 4,
  1100: 3,
  700: 2,
  500: 1
};export default function App() {
  return (
    <div className="App">
      <Masonry
        breakpointCols={breakpointColumnsObj}
        className="my-masonry-grid"
        columnClassName="my-masonry-grid_column"
      >
        {items}
      </Masonry>
    </div>
  );
}
```

我们添加了`breakpointColumnsObj`来设置当我们的屏幕达到给定的宽度时要显示的项目数量。

键是屏幕尺寸，值是要在一行中显示的项目数。

`className`有项目的类名。

`columnClassName`有网格列的类名。

我们呈现了`Masonry`组件中的项目。

类名必须与 CSS 文件中的名称相匹配。

网格是响应性的，所以砖石网格将总是适合屏幕。

# 结论

我们可以使用 react-masonry-css 库轻松地向 React 应用程序添加砖石网格。