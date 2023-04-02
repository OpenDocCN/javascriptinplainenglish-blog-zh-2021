# 用 Visx 库创建一个反应分组条形图

> 原文：<https://javascript.plainenglish.io/create-a-react-grouped-bar-chart-with-the-visx-library-2c66b62469?source=collection_archive---------9----------------------->

![](img/874a6589adbbff8346e022fd8c0aa4e0.png)

Photo by [Sérgio Alves Santos](https://unsplash.com/@sergio_as?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将分组条形图添加到 React 应用程序中。

# 安装所需的软件包

我们必须安装一些模块来创建分组条形图。

首先，我们运行:

```
npm i @visx/axis @visx/group @visx/mock-data @visx/responsive @visx/scale @visx/shape
```

安装软件包。

# 创建图表

我们可以通过添加模块提供的项目来创建图表。

我们使用来自`@visx/mock-data`模块的数据。

为了创建图表，我们编写:

```
import React from "react";
import { Group } from "@visx/group";
import { BarGroup } from "@visx/shape";
import { AxisBottom } from "@visx/axis";
import cityTemperature from "@visx/mock-data/lib/mocks/cityTemperature";
import { scaleBand, scaleLinear, scaleOrdinal } from "@visx/scale";
import { timeParse, timeFormat } from "d3-time-format";const blue = "#aeeef8";
export const green = "#e5fd3d";
const purple = "#9caff6";
export const background = "#612efb";const data = cityTemperature.slice(0, 8);
const keys = Object.keys(data[0]).filter((d) => d !== "date");
const defaultMargin = { top: 40, right: 0, bottom: 40, left: 0 };const parseDate = timeParse("%Y-%m-%d");
const format = timeFormat("%b %d");
const formatDate = (date) => format(parseDate(date));const getDate = (d) => d.date;const dateScale = scaleBand({
  domain: data.map(getDate),
  padding: 0.2
});
const cityScale = scaleBand({
  domain: keys,
  padding: 0.1
});
const tempScale = scaleLinear({
  domain: [
    0,
    Math.max(...data.map((d) => Math.max(...keys.map((key) => Number(d[key])))))
  ]
});
const colorScale = scaleOrdinal({
  domain: keys,
  range: [blue, green, purple]
});function Example({ width, height, events = false, margin = defaultMargin }) {
  const xMax = width - margin.left - margin.right;
  const yMax = height - margin.top - margin.bottom;
  dateScale.rangeRound([0, xMax]);
  cityScale.rangeRound([0, dateScale.bandwidth()]);
  tempScale.range([yMax, 0]); return width < 10 ? null : (
    <svg width={width} height={height}>
      <rect
        x={0}
        y={0}
        width={width}
        height={height}
        fill={background}
        rx={14}
      />
      <Group top={margin.top} left={margin.left}>
        <BarGroup
          data={data}
          keys={keys}
          height={yMax}
          x0={getDate}
          x0Scale={dateScale}
          x1Scale={cityScale}
          yScale={tempScale}
          color={colorScale}
        >
          {(barGroups) =>
            barGroups.map((barGroup) => (
              <Group
                key={`bar-group-${barGroup.index}-${barGroup.x0}`}
                left={barGroup.x0}
              >
                {barGroup.bars.map((bar) => (
                  <rect
                    key={`bar-group-bar-${barGroup.index}-${bar.index}-${bar.value}-${bar.key}`}
                    x={bar.x}
                    y={bar.y}
                    width={bar.width}
                    height={bar.height}
                    fill={bar.color}
                    rx={4}
                    onClick={() => {
                      if (!events) return;
                      const { key, value } = bar;
                      alert(JSON.stringify({ key, value }));
                    }}
                  />
                ))}
              </Group>
            ))
          }
        </BarGroup>
      </Group>
      <AxisBottom
        top={yMax + margin.top}
        tickFormat={formatDate}
        scale={dateScale}
        stroke={green}
        tickStroke={green}
        hideAxisLine
        tickLabelProps={() => ({
          fill: green,
          fontSize: 11,
          textAnchor: "middle"
        })}
      />
    </svg>
  );
}export default function App() {
  return (
    <div className="App">
      <Example width="500" height="300" />
    </div>
  );
}
```

我们用`blue`、`green`和`purple`变量设置条形的颜色。

`background`是背景色。

`data`变量有我们想要获取并显示在栏中的模拟数据值。

`keys`有 x 轴数值。

`defaultMargin`有页边距样式。

我们从 D3 的时间解析和格式化函数中创建了`parseDate`和`format`函数。

然后我们用`dateScale`和`cityScale`变量创建日期和城市刻度。

`cityScale`值为条形。

`tempScale`是酒吧的高度。

`colorScale`有条形的颜色。

`Example`组件有条形图。我们把所有东西都放在那里。

`xMax`和`yMax`值分别是 x 轴和 y 轴的最大值。

我们用它来设置`dateScale`和`tempScale`的最大值。

在`return`语句中，我们把一切都放在了`svg`元素中。

`Group`有图表组件。

我们将`barGroups`映射到`rect`元素来显示条形。

我们设置`width`和`height`支柱来设置它们的宽度和高度。

x 轴由`AxisBottom`组件渲染。

我们设置`top`道具来设置轴的位置。

`tickFormat`有蜱。

`tickLabelProps`有标签样式。

# 结论

我们可以通过 Visx 库轻松地将分组条形图添加到 React 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)