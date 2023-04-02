# 使用 Visx 库创建反应面积差异图表

> 原文：<https://javascript.plainenglish.io/create-a-react-area-difference-chart-with-the-visx-library-b2eadac01ba3?source=collection_archive---------13----------------------->

![](img/10975bc44b3b3cf817f1ed54fe8ebbef.png)

Photo by [Paulius Dragunas](https://unsplash.com/@paulius005?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将面积差异图表添加到 React 应用程序中。

# 安装所需的库

我们必须安装 Visx 库提供的多个模块来创建面积差异图。

为此，我们运行:

```
npm i @visx/axis @visx/curve @visx/grid @visx/group @visx/mock-data @visx/responsive @visx/scale @visx/shape @visx/threshold
```

# 创建图表

一旦我们安装了所有需要的库，我们通过编写以下内容来添加图表:

```
import React from "react";
import { Group } from "@visx/group";
import { curveBasis } from "@visx/curve";
import { LinePath } from "@visx/shape";
import { Threshold } from "@visx/threshold";
import { scaleTime, scaleLinear } from "@visx/scale";
import { AxisLeft, AxisBottom } from "@visx/axis";
import { GridRows, GridColumns } from "@visx/grid";
import cityTemperature from "@visx/mock-data/lib/mocks/cityTemperature";export const background = "#f3f3f3";const date = (d) => new Date(d.date).valueOf();
const ny = (d) => Number(d["New York"]);
const sf = (d) => Number(d["San Francisco"]);const timeScale = scaleTime({
  domain: [
    Math.min(...cityTemperature.map(date)),
    Math.max(...cityTemperature.map(date))
  ]
});
const temperatureScale = scaleLinear({
  domain: [
    Math.min(...cityTemperature.map((d) => Math.min(ny(d), sf(d)))),
    Math.max(...cityTemperature.map((d) => Math.max(ny(d), sf(d))))
  ],
  nice: true
});const defaultMargin = { top: 40, right: 30, bottom: 50, left: 40 };function Theshold({ width, height, margin = defaultMargin }) {
  if (width < 10) return null;const xMax = width - margin.left - margin.right;
  const yMax = height - margin.top - margin.bottom;timeScale.range([0, xMax]);
  temperatureScale.range([yMax, 0]);return (
    <div>
      <svg width={width} height={height}>
        <rect
          x={0}
          y={0}
          width={width}
          height={height}
          fill={background}
          rx={14}
        />
        <Group left={margin.left} top={margin.top}>
          <GridRows
            scale={temperatureScale}
            width={xMax}
            height={yMax}
            stroke="#e0e0e0"
          />
          <GridColumns
            scale={timeScale}
            width={xMax}
            height={yMax}
            stroke="#e0e0e0"
          />
          <line x1={xMax} x2={xMax} y1={0} y2={yMax} stroke="#e0e0e0" />
          <AxisBottom
            top={yMax}
            scale={timeScale}
            numTicks={width > 520 ? 10 : 5}
          />
          <AxisLeft scale={temperatureScale} />
          <text x="-70" y="15" transform="rotate(-90)" fontSize={10}>
            Temperature (°F)
          </text>
          <Threshold
            id={`${Math.random()}`}
            data={cityTemperature}
            x={(d) => timeScale(date(d)) ?? 0}
            y0={(d) => temperatureScale(ny(d)) ?? 0}
            y1={(d) => temperatureScale(sf(d)) ?? 0}
            clipAboveTo={0}
            clipBelowTo={yMax}
            curve={curveBasis}
            belowAreaProps={{
              fill: "violet",
              fillOpacity: 0.4
            }}
            aboveAreaProps={{
              fill: "green",
              fillOpacity: 0.4
            }}
          />
          <LinePath
            data={cityTemperature}
            curve={curveBasis}
            x={(d) => timeScale(date(d)) ?? 0}
            y={(d) => temperatureScale(sf(d)) ?? 0}
            stroke="#222"
            strokeWidth={1.5}
            strokeOpacity={0.8}
            strokeDasharray="1,2"
          />
          <LinePath
            data={cityTemperature}
            curve={curveBasis}
            x={(d) => timeScale(date(d)) ?? 0}
            y={(d) => temperatureScale(ny(d)) ?? 0}
            stroke="#222"
            strokeWidth={1.5}
          />
        </Group>
      </svg>
    </div>
  );
}export default function App() {
  return (
    <div className="App">
      <Theshold width="500" height="300" />
    </div>
  );
}
```

我们使用 Visx 库提供的模拟数据来创建图表。

我们为 x 轴创建`timeScale`刻度。

我们为 y 轴创建了`temperatureScale`。

我们分别调用`scaleTime`和`scaleLinear`来缩放数据显示图表。

接下来，我们用`defaultMargin`对象设置边距。

然后我们创建`Threshold`组件，它有面积差图。

在其中，我们计算了`xMax`和`yMax`值，以分别创建 x 轴和 y 轴的最大值。

然后我们调用`range`方法为图表创建时间和温度刻度。

接下来，我们添加`svg`元素来添加图表的容器。

`rect`有包围图表的矩形。

`Group`有我们需要形成图表的项目。

`GridRows`有网格行。

我们将`scale`支柱设置到`temperatureScale`来显示温度。

同样，我们对`GridColumns`组件做同样的事情，但是`scale`被设置为`timeScale`。

`line`有图表的周界线。

`AxisBottom`有 x 轴。

`AxisLeft`是 y 轴。

我们添加了`Threshold`组件来填充线条。

我们添加带有`LinePath`组件的行。

我们通过设置`data`道具来设置数据。

`x`和`y`道具返回 x 和 y 值。

最后，在`App`中，我们呈现我们创建的`Threshold`组件，并设置`width`和`height`来显示图表。

# 结论

我们可以使用 Visx 库在 React 应用程序中轻松创建面积差异图表。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)