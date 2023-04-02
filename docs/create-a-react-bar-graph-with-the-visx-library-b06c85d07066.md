# 用 Visx 库创建一个反应条形图

> 原文：<https://javascript.plainenglish.io/create-a-react-bar-graph-with-the-visx-library-b06c85d07066?source=collection_archive---------7----------------------->

![](img/aeb2d0b974c9965422c89c8da788c1f9.png)

Photo by [Alexander Popov](https://unsplash.com/@5tep5?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将条形图添加到 React 应用程序中。

# 入门指南

首先，我们必须安装 Visx 提供的几个模块。,

为了安装条形图所需的，我们运行:

```
$ npm install --save @visx/mock-data @visx/group @visx/shape @visx/scale
```

`@visx/mock-data`库有模拟数据，我们可以在条形图中使用。

# 创建条形图

为了创建条形图，我们添加以下代码:

```
import React from "react";
import { letterFrequency } from "@visx/mock-data";
import { Group } from "@visx/group";
import { Bar } from "@visx/shape";
import { scaleLinear, scaleBand } from "@visx/scale";const data = letterFrequency;
const width = 500;
const height = 300;
const margin = { top: 20, bottom: 20, left: 20, right: 20 };
const xMax = width - margin.left - margin.right;
const yMax = height - margin.top - margin.bottom;
const x = (d) => d.letter;
const y = (d) => +d.frequency * 100;const xScale = scaleBand({
  range: [0, xMax],
  round: true,
  domain: data.map(x),
  padding: 0.4
});
const yScale = scaleLinear({
  range: [yMax, 0],
  round: true,
  domain: [0, Math.max(...data.map(y))]
});const compose = (scale, accessor) => (data) => scale(accessor(data));
const xPoint = compose(xScale, x);
const yPoint = compose(yScale, y);function BarGraph(props) {
  return (
    <svg width={width} height={height}>
      {data.map((d, i) => {
        const barHeight = yMax - yPoint(d);
        return (
          <Group key={`bar-${i}`}>
            <Bar
              x={xPoint(d)}
              y={yMax - barHeight}
              height={barHeight}
              width={xScale.bandwidth()}
              fill="#fc2e1c"
            />
          </Group>
        );
      })}
    </svg>
  );
}export default function App() {
  return (
    <div>
      <BarGraph />
    </div>
  );
}
```

`data`有我们图表的数据。

`width`和`height`是图形的宽度和高度。

`margin`有边际。

`xMax`具有最大 x 轴值。

`yMax`具有最大 y 轴值。

`x`是返回 x 轴显示数据的函数。

而`y`是返回数据显示在 y 轴上的函数。

`xScale`让我们创建要添加到图表中的 x 轴值。

`yScale`具有图形的 y 轴值。

然后，我们创建`compose`函数来缩放 x 和 y 轴值，以适合图表。

一旦我们这样做了，我们就用`Group`和`Bar`组件创建了`BarGraph`组件。

`Bar`有酒吧。

`Group`有了酒吧的容器。

我们为条设置了`fill`颜色。

以及`x`和`y`值

`y`设置为杆的高度。

`width`根据屏幕尺寸进行缩放。

# 结论

我们可以通过 Visx 库轻松地将条形图添加到 React 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)