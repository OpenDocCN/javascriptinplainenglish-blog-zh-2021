# 更多渲染大列表的方法

> 原文：<https://javascript.plainenglish.io/more-ways-to-render-large-lists-with-react-bedb954b8056?source=collection_archive---------14----------------------->

![](img/f270ac1b0d1c50cb09eb7530dfeb9de0.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常不得不在反应应用程序中渲染大列表。

在本文中，我们将研究在 React 应用程序中呈现大列表的方法。

# 虚拟滚动

`react-virtualized`库允许我们将虚拟化列表添加到我们的反应应用程序中。

它只加载屏幕上显示的数据。

要使用它，我们通过运行以下命令安装它:

```
npm i react-virtualized
```

然后我们可以用它来写:

```
import React from "react";
import { List } from "react-virtualized";export default function App() {
  const data = new Array(1000).fill().map((value, id) => ({
    id: id,
    title: id,
    body: id
  })); const renderRow = ({ index, key, style }) => (
    <div>
      <div key={key} style={style} className="post">
        <h3>{data[index].title}</h3>
        <p>item {data[index].body}</p>
      </div>
    </div>
  );
  return (
    <List
      width={window.innerWidth * 0.95}
      height={300}
      rowRenderer={renderRow}
      rowCount={data.length}
      rowHeight={120}
    />
  );
}
```

我们只需要创建`renderRiw`功能，通过它们的`index`和`style`来渲染项目。

`style`由`react-virtualized`计算，以符合列表中的数据。

我们从`data[index]`开始。

`rowCount`设置为总行数。

`height`具有列表的高度。

`rowHeight`有行高。

# 反应窗口

`react-window`是另一个虚拟化的滚动组件。

要安装它，我们运行:

```
npm i react-window
```

然后，我们可以通过书写添加该列表:

```
import React from "react";
import { FixedSizeList as List } from "react-window";export default function App() {
  const data = new Array(1000).fill().map((value, id) => ({
    id: id,
    title: id,
    body: id
  })); const Row = ({ index, key, style }) => (
    <div>
      <div key={key} style={style} className="post">
        <h3>{data[index].title}</h3>
        <p>item {data[index].body}</p>
      </div>
    </div>
  );
  return (
    <List
      width={window.innerWidth * 0.95}
      height={300}
      itemCount={data.length}
      itemSize={120}
    >
      {Row}
    </List>
  );
}
```

我们有`Row`组件，它有行数据。

与上例的`renderRow`功能相同。

我们有带`width` 、`height`的`List`组件，可以计算行数。

`itemSize`有行高。

`itemCount`有要渲染的项目数。

`react-window`比`react-virtualized`更快更小。

# 结论

我们可以用虚拟滚动来渲染大型列表。

喜欢这篇文章吗？如果是这样，通过**[订阅我们的 YouTube 频道](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true)** **获取更多类似内容吧！**

*多内容见于* [***中***](https://plainenglish.io/)