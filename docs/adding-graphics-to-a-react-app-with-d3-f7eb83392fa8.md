# 使用 D3 向 React 应用程序添加图形

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-react-app-with-d3-f7eb83392fa8?source=collection_archive---------16----------------------->

![](img/8dfc15994d5292da1ac7d242b31ab5dd.png)

Photo by [Randy Tarampi](https://unsplash.com/@randytarampi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 入门指南

我们通过运行`npm i d3`来安装 D3。

然后我们可以在我们的 Vue 应用程序中使用它。

# 数据连接

现在我们安装了 D3，我们可以在我们的应用程序中使用它。

D3 让我们可以轻松地将一组条目呈现到一个列表中。

为此，我们写道:

```
import React, { useEffect } from "react";
import * as d3 from "d3";const arr = [10, 20, 30, 25, 15];export default function App() {
  useEffect(() => {
    d3.select("#list")
      .selectAll("li")
      .data(arr)
      .text((d) => d);
  }, []); return (
    <div className="App">
      <ul id="list">
        {arr.map(() => (
          <li></li>
        ))}
      </ul>
    </div>
  );
}
```

我们将 D3 代码放入`useEffect`回调中以获取列表，然后选择所有的`li`元素。

然后我们将数字放入`li`元素中。

# 挽救（saving 的简写）

我们可以使用 D3 将 SVG 添加到我们的组件中。

为此，我们写道:

```
import React, { useEffect } from "react";
import * as d3 from "d3";export default function App() {
  useEffect(() => {
    const width = 300;
    const height = 300;
    const svg = d3
      .select("#svgcontainer")
      .append("svg")
      .attr("width", width)
      .attr("height", height);
    svg
      .append("line")
      .attr("x1", 100)
      .attr("y1", 100)
      .attr("x2", 200)
      .attr("y2", 200)
      .style("stroke", "rgb(255,0,0)")
      .style("stroke-width", 2);
  }, []); return (
    <div className="App">
      <div id="svgcontainer"></div>
    </div>
  );
}
```

添加一行。

我们有:

```
const svg = d3
  .select("#svgcontainer")
  .append("svg")
  .attr("width", width)
  .attr("height", height);
```

将`svg`添加到 ID 为`svgcontainer`的 div 中。

我们用`attr`方法设置`svg`的`width`和`height`。

然后我们通过书写添加该行:

```
svg
  .append("line")
  .attr("x1", 100)
  .attr("y1", 100)
  .attr("x2", 200)
  .attr("y2", 200)
  .style("stroke", "rgb(255,0,0)")
  .style("stroke-width", 2);
```

我们用`'line'`调用`append`来添加行。

然后我们添加`x1`和`y1`属性来添加线条起点的坐标。

我们添加了`x2`和`y2`属性来添加线条末端的坐标。

此外，我们设置线条的笔画颜色。

我们设置笔画宽度来设置线条粗细。

# 矩形

我们可以用`append`方法添加一个矩形，用`'rect'`作为参数。

例如，我们可以写:

```
import React, { useEffect } from "react";
import * as d3 from "d3";export default function App() {
  useEffect(() => {
    const width = 300;
    const height = 300;
    const svg = d3
      .select("#svgcontainer")
      .append("svg")
      .attr("width", width)
      .attr("height", height);
    svg
      .append("rect")
      .attr("x", 20)
      .attr("y", 20)
      .attr("width", 200)
      .attr("height", 100)
      .attr("fill", "green");
  }, []); return (
    <div className="App">
      <div id="svgcontainer"></div>
    </div>
  );
}
```

我们添加`svg`的方式与前面的例子相同。

然后我们用`append`方法添加矩形。

`x`和`y`属性是圆圈左上角的 x 和 y 坐标。

`width`和`height`属性是矩形的宽度和高度。

而`fill`是矩形的背景色。

# 结论

我们可以用 D3 给 React 应用程序添加基本形状。