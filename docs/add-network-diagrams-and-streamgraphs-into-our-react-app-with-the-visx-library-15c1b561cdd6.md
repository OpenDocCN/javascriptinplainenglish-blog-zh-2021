# 使用 Visx 库将网络图和流图添加到 React 应用程序中

> 原文：<https://javascript.plainenglish.io/add-network-diagrams-and-streamgraphs-into-our-react-app-with-the-visx-library-15c1b561cdd6?source=collection_archive---------12----------------------->

![](img/b366f2c391bbeb08d49e267f09a423f7.png)

Photo by [Patrick Mayor](https://unsplash.com/@pmayor?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将雷达图添加到 React 应用程序中。

# 安装所需的软件包

我们必须安装一些模块。

首先，我们运行:

```
npm i @visx/responsive @visx/network
```

安装网络图的软件包。

我们运行:

```
npm i @visx/responsive @visx/pattern @visx/scale @visx/shape
```

安装流图的软件包。

# 网络图

我们可以通过编写以下内容来添加网络图:

```
import React from "react";
import { Graph } from "@visx/network";const nodes = [
  { x: 50, y: 20 },
  { x: 200, y: 300 },
  { x: 300, y: 40 }
];const links = [
  { source: nodes[0], target: nodes[1] },
  { source: nodes[1], target: nodes[2] },
  { source: nodes[2], target: nodes[0] }
];const graph = {
  nodes,
  links
};const background = "#272b4d";function Example({ width, height }) {
  return width < 10 ? null : (
    <svg width={width} height={height}>
      <rect width={width} height={height} rx={14} fill={background} />
      <Graph graph={graph} />
    </svg>
  );
}export default function App() {
  return (
    <div className="App">
      <Example width={500} height={300} />
    </div>
  );
}
```

我们所要做的就是将`nodes`传递给`Graph`组件来创建网络图。

每个`nodes`条目都有`x`和`y`属性来设置每个节点的坐标。

# 流图

我们可以通过编写以下内容来创建流图:

```
import React, { useState } from "react";
import { Stack } from "[@visx/shape](http://twitter.com/visx/shape)";
import { PatternCircles, PatternWaves } from "[@visx/pattern](http://twitter.com/visx/pattern)";
import { scaleLinear, scaleOrdinal } from "[@visx/scale](http://twitter.com/visx/scale)";
import { transpose } from "d3-array";
import { animated, useSpring } from "react-spring";function useForceUpdate() {
  const [, setValue] = useState(0);
  return () => setValue((value) => value + 1); // update state to force render
}const getPoints = (array, pointCount) => {
  const x = 1 / (0.1 + Math.random());
  const y = 2 * Math.random() - 0.5;
  const z = 10 / (0.1 + Math.random());
  for (let i = 0; i < pointCount; i += 1) {
    const w = (i / pointCount - y) * z;
    array[i] += x * Math.exp(-w * w);
  }
};const generateData = (pointCount, bumpCount) => {
  const arr = [];
  let i;
  for (i = 0; i < pointCount; i += 1) arr[i] = 0;
  for (i = 0; i < bumpCount; i += 1) getPoints(arr, pointCount);
  return arr;
}; const NUM_LAYERS = 20;
const SAMPLES_PER_LAYER = 200;
const BUMPS_PER_LAYER = 10;
const BACKGROUND = "#ffdede";
const range = (n) => Array.from(new Array(n), (_, i) => i);const keys = range(NUM_LAYERS); const xScale = scaleLinear({
  domain: [0, SAMPLES_PER_LAYER - 1]
});
const yScale = scaleLinear({
  domain: [-30, 50]
});
const colorScale = scaleOrdinal({
  domain: keys,
  range: [
    "#ffc409",
    "#f14702",
    "#262d97",
    "white",
    "#036ecd",
    "#9ecadd",
    "#51666e"
  ]
});
const patternScale = scaleOrdinal({
  domain: keys,
  range: [
    "mustard",
    "cherry",
    "navy",
    "circles",
    "circles",
    "circles",
    "circles"
  ]
});const getY0 = (d) => yScale(d[0]) ?? 0;
const getY1 = (d) => yScale(d[1]) ?? 0;function Example({ width, height, animate = true }) {
  const forceUpdate = useForceUpdate();
  const handlePress = () => forceUpdate(); if (width < 10) return null; xScale.range([0, width]);
  yScale.range([height, 0]);
  const layers = transpose(
    keys.map(() => generateData(SAMPLES_PER_LAYER, BUMPS_PER_LAYER))
  ); return (
    <svg width={width} height={height}>
      <PatternCircles
        id="mustard"
        height={40}
        width={40}
        radius={5}
        fill="#036ecf"
        complement
      />
      <PatternWaves
        id="cherry"
        height={12}
        width={12}
        fill="transparent"
        stroke="#232493"
        strokeWidth={1}
      />
      <PatternCircles
        id="navy"
        height={60}
        width={60}
        radius={10}
        fill="white"
        complement
      />
      <PatternCircles
        complement
        id="circles"
        height={60}
        width={60}
        radius={10}
        fill="transparent"
      /> <g onClick={handlePress} onTouchStart={handlePress}>
        <rect
          x={0}
          y={0}
          width={width}
          height={height}
          fill={BACKGROUND}
          rx={14}
        />
        <Stack
          data={layers}
          keys={keys}
          offset="wiggle"
          color={colorScale}
          x={(_, i) => xScale(i) ?? 0}
          y0={getY0}
          y1={getY1}
        >
          {({ stacks, path }) =>
            stacks.map((stack) => {
              // Alternatively use renderprops <Spring to={{ d }}>{tweened => ...}</Spring>
              const tweened = animate
                ? useSpring({ d: path(stack) })
                : { d: path(stack) };
              const color = colorScale(stack.key);
              const pattern = patternScale(stack.key);
              return (
                <g key={`series-${stack.key}`}>
                  <animated.path d={tweened.d || ""} fill={color} />
                  <animated.path
                    d={tweened.d || ""}
                    fill={`url(#${pattern})`}
                  />
                </g>
              );
            })
          }
        </Stack>
      </g>
    </svg>
  );
}export default function App() {
  return (
    <div className="App">
      <Example width={500} height={300} />
    </div>
  );
}
```

我们有一个`useForceUpdate`钩子，当我们点击它时，它会更新流图。

`getPoints`操作流图的点。

数据由`genereateData`功能生成。

常量用于控制我们生成的数据类型。

`xScale`和`yScale`的值介于 x 和 y 尺寸的极值之间。

`colorScale`让颜色范围内生成的颜色值填充 streamgraph 分区。

`patternScale`有流图分区的模式，。

`getY0`和`getY1`让我们获得流图所需的 y 维值。

为了呈现图形，我们使用`PatternCircles`组件来呈现流图中的圆圈。

为了呈现其他形状，我们使用`Stack`组件返回`animated.path`组件来呈现分区形状的路径。

当我们点击形状时，运行`forceUpdate`用新数据重新渲染流图。

# 结论

我们可以使用 Visx 库在 React 应用程序中添加网络图和流图。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)