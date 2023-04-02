# 使用 Visx 库将多种样式的线条添加到 React 应用程序中

> 原文：<https://javascript.plainenglish.io/add-lines-with-multiple-styles-into-a-react-app-with-the-visx-library-9069d55c15c1?source=collection_archive---------14----------------------->

![](img/9b417f3798d39102267155a890afa102.png)

Photo by [Waldemar Brandt](https://unsplash.com/@waldemarbrandt67w?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它向 React 应用程序添加具有自己风格的线段曲线

# 安装所需的软件包

我们必须安装一些模块。

首先，我们运行:

```
npm i @visx/curve @visx/gradient @visx/responsive @visx/scale @visx/shape
```

安装软件包。

# 创建多样式线条

我们可以通过添加模块提供的项目来创建图表。

为了添加这一行，我们写:

```
import React, { useMemo } from "react";
import { scaleLinear } from "@visx/scale";
import { curveCardinal } from "@visx/curve";
import { LinePath, SplitLinePath } from "@visx/shape";
import { LinearGradient } from "@visx/gradient";const getX = (d) => d.x;
const getY = (d) => d.y;
const background = "#045275";
const backgroundLight = "#089099";
const foreground = "#b7e6a5";function generateSinPoints({
  width,
  height,
  numberOfWaves = 10,
  pointsPerWave = 10
}) {
  const waveLength = width / numberOfWaves;
  const distanceBetweenPoints = waveLength / pointsPerWave;
  const sinPoints = []; for (let waveIndex = 0; waveIndex <= numberOfWaves; waveIndex += 1) {
    const waveDistFromStart = waveIndex * waveLength; for (let pointIndex = 0; pointIndex <= pointsPerWave; pointIndex += 1) {
      const waveXFraction = pointIndex / pointsPerWave;
      const waveX = pointIndex * distanceBetweenPoints;
      const globalX = waveDistFromStart + waveX;
      const globalXFraction = (width - globalX) / width;
      const waveHeight =
        Math.min(globalXFraction, 1 - globalXFraction) * height;
      sinPoints.push({
        x: globalX,
        y: waveHeight * Math.sin(waveXFraction * (2 * Math.PI))
      });
    }
  } return sinPoints;
}function Example({
  width,
  height,
  numberOfWaves = 10,
  pointsPerWave = 100,
  numberOfSegments = 8
}) {
  const data = useMemo(
    () => generateSinPoints({ width, height, numberOfWaves, pointsPerWave }),
    [width, height, numberOfWaves, pointsPerWave]
  ); const dividedData = useMemo(() => {
    const segmentLength = Math.floor(data.length / numberOfSegments);
    return new Array(numberOfSegments)
      .fill(null)
      .map((_, i) => data.slice(i * segmentLength, (i + 1) * segmentLength));
  }, [numberOfSegments, data]); const getScaledX = useMemo(() => {
    const xScale = scaleLinear({ range: [0, width], domain: [0, width] });
    return (d) => xScale(getX(d)) ?? 0;
  }, [width]); const getScaledY = useMemo(() => {
    const yScale = scaleLinear({ range: [0, height], domain: [height, 0] });
    return (d) => yScale(getY(d)) ?? 0;
  }, [height]); return width < 10 ? null : (
    <div>
      <svg width={width} height={height}>
        <LinearGradient
          id="visx-shape-splitlinepath-gradient"
          from={background}
          to={backgroundLight}
          fromOpacity={0.8}
          toOpacity={0.8}
        />
        <rect
          x={0}
          y={0}
          width={width}
          height={height}
          fill="url(#visx-shape-splitlinepath-gradient)"
          rx={14}
        /> <g transform={`rotate(${0})translate(${-0}, ${-height * 0.5})`}>
          <LinePath
            data={data}
            x={getScaledX}
            y={getScaledY}
            strokeWidth={8}
            stroke="#fff"
            strokeOpacity={0.15}
            curve={curveCardinal}
          /> <SplitLinePath
            segments={dividedData}
            x={getScaledX}
            y={getScaledY}
            curve={curveCardinal}
            styles={[
              { stroke: foreground, strokeWidth: 3 },
              { stroke: "#fff", strokeWidth: 2, strokeDasharray: "9,5" },
              { stroke: background, strokeWidth: 2 }
            ]}
          >
            {({ segment, styles, index }) =>
              index === numberOfSegments - 1 || index === 2 ? (
                segment.map(({ x, y }, i) =>
                  i % 8 === 0 ? (
                    <circle
                      key={i}
                      cx={x}
                      cy={y}
                      r={10 * (i / segment.length)}
                      stroke={styles?.stroke}
                      fill="transparent"
                      strokeWidth={1}
                    />
                  ) : null
                )
              ) : (
                <LinePath
                  data={segment}
                  x={(d) => d.x || 0}
                  y={(d) => d.y || 0}
                  {...styles}
                />
              )
            }
          </SplitLinePath>
        </g>
      </svg>
    </div>
  );
}export default function App() {
  return (
    <div className="App">
      <Example width={500} height={300} />
    </div>
  );
}
```

我们添加了`getX`和`getY`函数来获取 x 和 y 轴的数据。

`background`是背景渐变的颜色之一。

`backgroundLight`具有较浅的背景渐变颜色。

`foreground`有一种线条颜色。

我们用`generateSinPoints`函数生成线的点。

`globalX`有正弦曲线的 x 坐标。

我们使用`Math.sin`方法来创建 y 轴值。

在`Example`组件中，我们用各种样式呈现线条。

我们用`dividedData`变量将线分成几段。

这是通过创建一个值数组并用`slice`分割从`generateSinPoints`创建的值来完成的。

然后我们用`getScaledX`和`getScaledY`变量创建图表的比例。

我们用`scaleLinear`函数创建它们，因为一切都是线性比例。

然后我们用`LinePath`组件渲染左边的线段。

我们使用`SplitLinePath`组件来呈现剩余的片段。

我们从`styles`道具中获取样式，并用在`SplitLinePath`的渲染道具中返回的`LineSegment`组件渲染它们。

# 结论

我们可以在带有 Visx 库的 React 应用程序中创建一条包含多个具有各自风格的线段的线。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)