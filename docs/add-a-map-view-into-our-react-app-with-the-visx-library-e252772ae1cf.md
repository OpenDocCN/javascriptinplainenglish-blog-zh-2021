# 使用 Visx 库将地图视图添加到 React 应用程序中

> 原文：<https://javascript.plainenglish.io/add-a-map-view-into-our-react-app-with-the-visx-library-e252772ae1cf?source=collection_archive---------21----------------------->

![](img/f3cac7d363e65ded211fdcdd77f98a0a.png)

Photo by [Brett Zeck](https://unsplash.com/@iambrettzeck?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Visx 是一个库，让我们可以轻松地将图形添加到 React 应用程序中。

在本文中，我们将了解如何使用它将地图视图添加到 React 应用程序中

# 安装所需的软件包

我们必须安装一些模块来创建地图。

首先，我们运行:

```
npm i @visx/geo @visx/responsive @visx/scale @visx/zoom
```

安装软件包。

# 添加地图

我们可以通过编写以下内容来添加地图:

```
import React, { useState } from "react";
import * as topojson from "topojson-client";
import { scaleQuantize } from "@visx/scale";
import { CustomProjection, Graticule } from "@visx/geo";
import { Projection } from "@visx/geo/lib/types";
import { Zoom } from "@visx/zoom";
import {
  geoConicConformal,
  geoTransverseMercator,
  geoNaturalEarth1,
  geoConicEquidistant,
  geoOrthographic,
  geoStereographic
} from "d3-geo";
import topology from "./world-topo.json";export const background = "#252b7e";
const purple = "#201c4e";
const PROJECTIONS = {
  geoConicConformal,
  geoTransverseMercator,
  geoNaturalEarth1,
  geoConicEquidistant,
  geoOrthographic,
  geoStereographic
};const world = topojson.feature(topology, topology.objects.units);
const color = scaleQuantize({
  domain: [
    Math.min(...world.features.map((f) => f.geometry.coordinates.length)),
    Math.max(...world.features.map((f) => f.geometry.coordinates.length))
  ],
  range: [
    "#019ece",
    "#f4448b",
    "#fccf35",
    "#82b75d",
    "#b33c88",
    "#fc5e2f",
    "#f94b3a",
    "#f63a48",
    "#dde1fe",
    "#8993f9",
    "#b6c8fb",
    "#65fe8d"
  ]
});function Example({ width, height, events = true }: GeoCustomProps) {
  const [projection, setProjection] = useState("geoConicConformal"); const centerX = width / 2;
  const centerY = height / 2;
  const initialScale = (width / 630) * 100; return width < 10 ? null : (
    <>
      <Zoom
        width={width}
        height={height}
        scaleXMin={100}
        scaleXMax={1000}
        scaleYMin={100}
        scaleYMax={1000}
        transformMatrix={{
          scaleX: initialScale,
          scaleY: initialScale,
          translateX: centerX,
          translateY: centerY,
          skewX: 0,
          skewY: 0
        }}
      >
        {(zoom) => (
          <div className="container">
            <svg
              width={width}
              height={height}
              className={zoom.isDragging ? "dragging" : undefined}
            >
              <rect
                x={0}
                y={0}
                width={width}
                height={height}
                fill={background}
                rx={14}
              />
              <CustomProjection
                projection={PROJECTIONS[projection]}
                data={world.features}
                scale={zoom.transformMatrix.scaleX}
                translate={[
                  zoom.transformMatrix.translateX,
                  zoom.transformMatrix.translateY
                ]}
              >
                {(customProjection) => (
                  <g>
                    <Graticule
                      graticule={(g) => customProjection.path(g) || ""}
                      stroke={purple}
                    />
                    {customProjection.features.map(({ feature, path }, i) => (
                      <path
                        key={`map-feature-${i}`}
                        d={path || ""}
                        fill={color(feature.geometry.coordinates.length)}
                        stroke={background}
                        strokeWidth={0.5}
                        onClick={() => {
                          if (events)
                            alert(
                              `Clicked: ${feature.properties.name} (${feature.id})`
                            );
                        }}
                      />
                    ))}
                  </g>
                )}
              </CustomProjection>
              <rect
                x={0}
                y={0}
                width={width}
                height={height}
                rx={14}
                fill="transparent"
                onTouchStart={zoom.dragStart}
                onTouchMove={zoom.dragMove}
                onTouchEnd={zoom.dragEnd}
                onMouseDown={zoom.dragStart}
                onMouseMove={zoom.dragMove}
                onMouseUp={zoom.dragEnd}
                onMouseLeave={() => {
                  if (zoom.isDragging) zoom.dragEnd();
                }}
              />
            </svg>
            {events && (
              <div className="controls">
                <button
                  className="btn btn-zoom"
                  onClick={() => zoom.scale({ scaleX: 1.2, scaleY: 1.2 })}
                >
                  +
                </button>
                <button
                  className="btn btn-zoom btn-bottom"
                  onClick={() => zoom.scale({ scaleX: 0.8, scaleY: 0.8 })}
                >
                  -
                </button>
                <button className="btn btn-lg" onClick={zoom.reset}>
                  Reset
                </button>
              </div>
            )}
          </div>
        )}
      </Zoom>
      <label>
        projection:{" "}
        <select onChange={(event) => setProjection(event.target.value)}>
          {Object.keys(PROJECTIONS).map((projectionName) => (
            <option key={projectionName} value={projectionName}>
              {projectionName}
            </option>
          ))}
        </select>
      </label>
      <style jsx>{`
        .container {
          position: relative;
        }
        svg {
          cursor: grab;
        }
        svg.dragging {
          cursor: grabbing;
        }
        .btn {
          margin: 0;
          text-align: center;
          border: none;
          background: #dde1fe;
          color: #222;
          padding: 0 4px;
          border-top: 1px solid #8993f9;
        }
        .btn-lg {
          font-size: 12px;
          line-height: 1;
          padding: 4px;
        }
        .btn-zoom {
          width: 26px;
          font-size: 22px;
        }
        .btn-bottom {
          margin-bottom: 1rem;
        }
        .controls {
          position: absolute;
          bottom: 20px;
          right: 15px;
          display: flex;
          flex-direction: column;
          align-items: flex-end;
        }
        label {
          font-size: 12px;
        }
      `}</style>
    </>
  );
}export default function App() {
  return (
    <div className="App">
      <Example width={500} height={300} />
    </div>
  );
}
```

`world-topo.json`可在[https://code sandbox . io/s/github/Airbnb/visx/tree/master/packages/visx-demo/src/sandboxes/visx-geo-custom？file=/world-topo.json](https://codesandbox.io/s/github/airbnb/visx/tree/master/packages/visx-demo/src/sandboxes/visx-geo-custom?file=/world-topo.json)

我们添加了`background`和`purple`来为地图添加颜色。

`PROJECTIONS`拥有可用的地图视图类型。

我们通过用 JSON 调用`topojson.feature`方法将数据转换成可以显示的东西。

`scaleQuantize`方法让我们给地图上的国家添加颜色。

在`Example`组件中，我们有`projection`状态来显示给定投影类型的地图。

我们用`centerX`和`centerY`变量设置中心坐标。

我们将`initialScale`变量设置为初始缩放级别。

为了显示地图，我们添加了`Zoom`组件来添加缩放。

然后在它的渲染道具中，我们添加了`CustomProjection`组件来添加地图。

而`Graticule`组件让我们在地图上添加网格线。

在此之下，我们添加矩形，让我们用触摸和鼠标处理程序拖动平移地图。

在它下面，我们添加了按钮来添加缩放和重置缩放功能。

然后我们添加选择下拉菜单，让我们通过改变`projection`状态来选择项目。

我们在`CustomProjection`组件中使用了它。

最后，我们为地图添加样式。

# 结论

我们可以添加一个带有 Visx 库可用组件的地图视图。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容看*[***plain English . io***](https://plainenglish.io/)