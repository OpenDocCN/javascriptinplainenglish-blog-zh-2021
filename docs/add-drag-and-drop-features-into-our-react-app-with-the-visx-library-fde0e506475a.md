# 使用 Visx 库将拖放功能添加到我们的 React 应用程序中

> 原文：<https://javascript.plainenglish.io/add-drag-and-drop-features-into-our-react-app-with-the-visx-library-fde0e506475a?source=collection_archive---------10----------------------->

![](img/838bcafe24a782852edc4910f36c56e5.png)

Photo by [Maria Teneva](https://unsplash.com/@miteneva?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它向 React 应用程序添加具有自己风格的线段曲线

# 安装所需的软件包

我们必须安装一些模块来创建拖放。

首先，我们运行:

```
npm i @visx/drag @visx/gradient @visx/responsive @visx/scale
```

安装软件包。

# 添加拖放功能

我们通过编写以下代码来添加拖放功能:

```
import React, { useMemo, useState, useEffect } from "react";
import { scaleOrdinal } from "@visx/scale";
import { LinearGradient } from "@visx/gradient";
import { Drag, raise } from "@visx/drag";const colors = [
  "#025aac",
  "#02cff9",
  "#02efff",
  "#03aeed",
  "#0384d7",
  "#edfdff",
  "#ab31ff",
  "#5924d7"
];const generateCircles = ({ width, height }) =>
  new Array(width < 360 ? 40 : 185).fill(1).map((d, i) => {
    const radius = 25 - Math.random() * 20;
    return {
      id: `${i}`,
      radius,
      x: Math.round(Math.random() * (width - radius * 2) + radius),
      y: Math.round(Math.random() * (height - radius * 2) + radius)
    };
  });function Example({ width, height }) {
  const [draggingItems, setDraggingItems] = useState([]); useEffect(() => {
    if (width > 10 && height > 10)
      setDraggingItems(generateCircles({ width, height }));
  }, [width, height]); const colorScale = useMemo(
    () =>
      scaleOrdinal({
        range: colors,
        domain: draggingItems.map((d) => d.id)
      }),
    [width, height]
  ); if (draggingItems.length === 0 || width < 10) return null; return (
    <div className="Drag" style={{ touchAction: "none" }}>
      <svg width={width} height={height}>
        <LinearGradient id="stroke" from="#ff00a5" to="#ffc500" />
        <rect fill="#c4c3cb" width={width} height={height} rx={14} />{draggingItems.map((d, i) => (
          <Drag
            key={`drag-${d.id}`}
            width={width}
            height={height}
            x={d.x}
            y={d.y}
            onDragStart={() => {
              setDraggingItems(raise(draggingItems, i));
            }}
          >
            {({ dragStart, dragEnd, dragMove, isDragging, x, y, dx, dy }) => (
              <circle
                key={`dot-${d.id}`}
                cx={x}
                cy={y}
                r={isDragging ? d.radius + 4 : d.radius}
                fill={isDragging ? "url(#stroke)" : colorScale(d.id)}
                transform={`translate(${dx}, ${dy})`}
                fillOpacity={0.9}
                stroke={isDragging ? "white" : "transparent"}
                strokeWidth={2}
                onMouseMove={dragMove}
                onMouseUp={dragEnd}
                onMouseDown={dragStart}
                onTouchStart={dragStart}
                onTouchMove={dragMove}
                onTouchEnd={dragEnd}
              />
            )}
          </Drag>
        ))}
      </svg>
      <style jsx>{`
        .Drag {
          display: flex;
          flex-direction: column;
          user-select: none;
        } svg {
          margin: 1rem 0;
        }
        .deets {
          display: flex;
          flex-direction: row;
          font-size: 12px;
        }
        .deets > div {
          margin: 0.25rem;
        }
      `}</style>
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

我们用`generateCircles`函数返回一个包含`id`、`radius`、`x`和`y`属性的对象数组。

`id`是每个圆的唯一 ID。

其他属性用于在页面上呈现圆形。

在`Example`组件中，我们用`draggingItems`状态跟踪被跟踪的项目。

我们观察宽度和高度，并在`useEffect`钩子回调中添加圆圈。

`colorScale`状态让我们根据之前创建的`colors`数组计算颜色的比例。

在`return`语句中，我们有`Drag`组件，它是保存可拖动项目的容器。

然后，我们使用`Drag`组件中的渲染属性来渲染可拖动的项目。

它在`draggingItems`数组中呈现`circles`。

我们从 object 参数传入拖动事件处理程序作为`circle`的道具，使它们可拖动。

它们的位置将用这些事件处理函数来更新。

最后，我们在`style`标签中使用样式来改变容器的样式。

现在，我们应该在屏幕上有可以在盒子周围拖动的圆圈。

# 结论

我们可以使用 Visx 库将拖放功能添加到 React 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)