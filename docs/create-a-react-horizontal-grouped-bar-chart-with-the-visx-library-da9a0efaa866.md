# 用 Visx 库创建一个 React 水平分组条形图

> 原文：<https://javascript.plainenglish.io/create-a-react-horizontal-grouped-bar-chart-with-the-visx-library-da9a0efaa866?source=collection_archive---------15----------------------->

![](img/0ede457d9a36f4741bb54654338167c7.png)

Photo by [Adam Wilson](https://unsplash.com/@fourcolourblack?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将水平分组条形图添加到 React 应用程序中。

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
import { BarGroupHorizontal, Bar } from "@visx/shape";
import { Group } from "@visx/group";
import { AxisLeft } from "@visx/axis";
import cityTemperature from "@visx/mock-data/lib/mocks/cityTemperature";
import { scaleBand, scaleLinear, scaleOrdinal } from "@visx/scale";
import { timeParse, timeFormat } from "d3-time-format";const blue = "#aeeef8";
const green = "#e5fd3d";
const purple = "#9caff6";
const background = "#612efb";
const defaultMargin = { top: 20, right: 20, bottom: 20, left: 50 };const parseDate = timeParse("%Y-%m-%d");
const format = timeFormat("%b %d");
const formatDate = (date) => format(parseDate(date));
function max(arr, fn) {
  return Math.max(...arr.map(fn));
}const data = cityTemperature.slice(0, 4);
const keys = Object.keys(data[0]).filter((d) => d !== "date");const getDate = (d) => d.date;const dateScale = scaleBand({
  domain: data.map(getDate),
  padding: 0.2
});
const cityScale = scaleBand({
  domain: keys,
  padding: 0.1
});
const tempScale = scaleLinear({
  domain: [0, max(data, (d) => max(keys, (key) => Number(d[key])))]
});
const colorScale = scaleOrdinal({
  domain: keys,
  range: [blue, green, purple]
});function Example({ width, height, margin = defaultMargin, events = false }) {
  const xMax = width - margin.left - margin.right;
  const yMax = height - margin.top - margin.bottom;dateScale.rangeRound([0, yMax]);
  cityScale.rangeRound([0, dateScale.bandwidth()]);
  tempScale.rangeRound([0, xMax]);return width < 10 ? null : (
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
        <BarGroupHorizontal
          data={data}
          keys={keys}
          width={xMax}
          y0={getDate}
          y0Scale={dateScale}
          y1Scale={cityScale}
          xScale={tempScale}
          color={colorScale}
        >
          {(barGroups) =>
            barGroups.map((barGroup) => (
              <Group
                key={`bar-group-horizontal-${barGroup.index}-${barGroup.y0}`}
                top={barGroup.y0}
              >
                {barGroup.bars.map((bar) => (
                  <Bar
                    key={`${barGroup.index}-${bar.index}-${bar.key}`}
                    x={bar.x}
                    y={bar.y}
                    width={bar.width}
                    height={bar.height}
                    fill={bar.color}
                    rx={4}
                    onClick={() => {
                      if (events)
                        alert(
                          `${bar.key} (${bar.value}) - ${JSON.stringify(bar)}`
                        );
                    }}
                  />
                ))}
              </Group>
            ))
          }
        </BarGroupHorizontal>
        <AxisLeft
          scale={dateScale}
          stroke={green}
          tickStroke={green}
          tickFormat={formatDate}
          hideAxisLine
          tickLabelProps={() => ({
            fill: green,
            fontSize: 11,
            textAnchor: "end",
            dy: "0.33em"
          })}
        />
      </Group>
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

`background`变量有背景色。

`defaultMargin`有默认边距。

`parseDate`和`format`具有日期解析和格式化功能。

我们从模拟数据中解析日期，这样我们就可以将它们格式化以显示在图表中。

`data`有图表的数据。

`keys`有 x 轴的数据。

`dateScale`有日期刻度。

`cityScale`有城市数据。

`tempScale`具有条形的温度值。

`colorScale`有条块的颜色。

我们计算了`xMax`和`yMax`值，以获得 x 轴和 y 轴的最大值。

然后我们调用`rangeRound`来设置 x 和 y 轴范围的最大值。

接下来，我们返回`svg`元素，并在其中添加图表部分以添加条形图。

`Group`组件是杆件的容器。

`BarGroupHorizontal`让我们水平显示条形组。

我们用`y0`、`y0Scale`和`y1Scale`道具设置`color`、`width`和横杠的刻度。

`xScale`设置 x 轴刻度，即条形刻度。

然后我们映射`barGroups`来返回`map`回调中的`Bar`。

我们用`width`支柱设定杆的长度。

最后，我们添加`AxisLeft`组件来渲染 y 轴。

# 结论

我们可以使用 Visx 提供的模块在 React 应用程序中创建一个水平分组条形图。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)