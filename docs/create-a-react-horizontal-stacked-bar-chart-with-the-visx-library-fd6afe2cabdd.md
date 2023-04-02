# 用 Visx 库创建一个 React 水平堆积条形图

> 原文：<https://javascript.plainenglish.io/create-a-react-horizontal-stacked-bar-chart-with-the-visx-library-fd6afe2cabdd?source=collection_archive---------12----------------------->

![](img/ac1477f200e661461403f4a3d09b31b4.png)

Photo by [Johann Trasch](https://unsplash.com/@cocktailbart?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将水平堆积条形图添加到 React 应用程序中。

# 安装所需的软件包

我们必须安装一些模块。

首先，我们运行:

```
npm i @visx/axis @visx/grid @visx/group @visx/legend @visx/mock-data @visx/responsive @visx/scale @visx/shape @visx/tooltip
```

安装软件包。

# 创建图表

我们可以通过添加模块提供的项目来创建图表。

我们使用来自`@visx/mock-data`模块的数据。

为了创建水平堆叠条形图，我们编写:

```
import React from "react";
import { BarStackHorizontal } from "@visx/shape";
import { Group } from "@visx/group";
import { AxisBottom, AxisLeft } from "@visx/axis";
import cityTemperature from "@visx/mock-data/lib/mocks/cityTemperature";
import { scaleBand, scaleLinear, scaleOrdinal } from "@visx/scale";
import { timeParse, timeFormat } from "d3-time-format";
import { Tooltip, defaultStyles, useTooltip } from "@visx/tooltip";
import { LegendOrdinal } from "@visx/legend";const purple1 = "#6c5efb";
const purple2 = "#c998ff";
export const purple3 = "#a44afe";
export const background = "#eaedff";
const defaultMargin = { top: 40, left: 50, right: 40, bottom: 100 };
const tooltipStyles = {
  ...defaultStyles,
  minWidth: 60,
  backgroundColor: "rgba(0,0,0,0.9)",
  color: "white"
};const data = cityTemperature.slice(0, 12);
const keys = Object.keys(data[0]).filter((d) => d !== "date");const temperatureTotals = data.reduce((allTotals, currentDate) => {
  const totalTemperature = keys.reduce((dailyTotal, k) => {
    dailyTotal += Number(currentDate[k]);
    return dailyTotal;
  }, 0);
  allTotals.push(totalTemperature);
  return allTotals;
}, []);const parseDate = timeParse("%Y-%m-%d");
const format = timeFormat("%b %d");
const formatDate = (date) => format(parseDate(date));const getDate = (d) => d.date;
const temperatureScale = scaleLinear({
  domain: [0, Math.max(...temperatureTotals)],
  nice: true
});
const dateScale = scaleBand({
  domain: data.map(getDate),
  padding: 0.2
});
const colorScale = scaleOrdinal({
  domain: keys,
  range: [purple1, purple2, purple3]
});let tooltipTimeout;const Example = ({ width, height, events = false, margin = defaultMargin }) => {
  const {
    tooltipOpen,
    tooltipLeft,
    tooltipTop,
    tooltipData,
    hideTooltip,
    showTooltip
  } = useTooltip();
  const xMax = width - margin.left - margin.right;
  const yMax = height - margin.top - margin.bottom;temperatureScale.rangeRound([0, xMax]);
  dateScale.rangeRound([yMax, 0]);return width < 10 ? null : (
    <div>
      <svg width={width} height={height}>
        <rect width={width} height={height} fill={background} rx={14} />
        <Group top={margin.top} left={margin.left}>
          <BarStackHorizontal
            data={data}
            keys={keys}
            height={yMax}
            y={getDate}
            xScale={temperatureScale}
            yScale={dateScale}
            color={colorScale}
          >
            {(barStacks) =>
              barStacks.map((barStack) =>
                barStack.bars.map((bar) => (
                  <rect
                    key={`barstack-horizontal-${barStack.index}-${bar.index}`}
                    x={bar.x}
                    y={bar.y}
                    width={bar.width}
                    height={bar.height}
                    fill={bar.color}
                    onClick={() => {
                      if (events) alert(`clicked: ${JSON.stringify(bar)}`);
                    }}
                    onMouseLeave={() => {
                      tooltipTimeout = window.setTimeout(() => {
                        hideTooltip();
                      }, 300);
                    }}
                    onMouseMove={() => {
                      if (tooltipTimeout) clearTimeout(tooltipTimeout);
                      const top = bar.y + margin.top;
                      const left = bar.x + bar.width + margin.left;
                      showTooltip({
                        tooltipData: bar,
                        tooltipTop: top,
                        tooltipLeft: left
                      });
                    }}
                  />
                ))
              )
            }
          </BarStackHorizontal>
          <AxisLeft
            hideAxisLine
            hideTicks
            scale={dateScale}
            tickFormat={formatDate}
            stroke={purple3}
            tickStroke={purple3}
            tickLabelProps={() => ({
              fill: purple3,
              fontSize: 11,
              textAnchor: "end",
              dy: "0.33em"
            })}
          />
          <AxisBottom
            top={yMax}
            scale={temperatureScale}
            stroke={purple3}
            tickStroke={purple3}
            tickLabelProps={() => ({
              fill: purple3,
              fontSize: 11,
              textAnchor: "middle"
            })}
          />
        </Group>
      </svg>
      <div
        style={{
          position: "absolute",
          top: margin.top / 2 - 10,
          width: "100%",
          display: "flex",
          justifyContent: "center",
          fontSize: "14px"
        }}
      >
        <LegendOrdinal
          scale={colorScale}
          direction="row"
          labelMargin="0 15px 0 0"
        />
      </div>
      {tooltipOpen && tooltipData && (
        <Tooltip top={tooltipTop} left={tooltipLeft} style={tooltipStyles}>
          <div style={{ color: colorScale(tooltipData.key) }}>
            <strong>{tooltipData.key}</strong>
          </div>
          <div>{tooltipData.bar.data[tooltipData.key]}℉</div>
          <div>
            <small>{formatDate(getDate(tooltipData.bar.data))}</small>
          </div>
        </Tooltip>
      )}
    </div>
  );
};export default function App() {
  return (
    <div className="App">
      <Example width={500} height={300} />
    </div>
  );
}
```

我们创建了`purple`、`purple2`和`purple3`变量来设置条形的颜色。

`background`有背景色。

`defaultMargin`为图表留有页边距。

有工具提示的样式。

`data`有条形的数据。

`keys`有 y 轴的数据。

我们计算`temperatureTotals`，以便确定 x 轴的最大值。

接下来，我们使用`parseDate`和`format`函数来解析数据中的日期，并将它们格式化以显示在 y 轴上。

然后我们为 x 轴创建`temperatureScale`。

`dateScale`为 y 轴。

`colorScale`用于堆叠的棒材。

然后我们创建`Example`组件来添加图表。

我们调用`useTooltip`钩子来返回一个对象，让我们呈现工具提示来显示数据值。

`BarStackHorizontal`组件具有用于水平堆叠条的容器。

我们将比例设置为`xScale`和`yScale`道具的值。

`color`设置色阶。

在`BarStackHorizontal`组件的子组件中，我们为条形渲染矩形。

这是我们添加`onMouseMove`道具的地方，当我们移动鼠标时，它会显示带有条形数据的工具提示。

当鼠标离开工具栏时，我们调用`hideTooltip`来隐藏工具提示。

`AxisLeft`有 y 轴，显示日期。

并且`AxisBottom`具有带温度数据的 x 轴。

然后，我们为带有`LegendOrdinal`组件的条形添加图例。

并且`Tooltip`组件有工具提示。

# 结论

我们可以使用 Visx 库在 React 应用程序中添加水平堆叠条形图。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)