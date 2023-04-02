# 使用 D3 向 Vue 应用添加图形—拖放、缩放和 CSV

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-vue-app-with-d3-drag-and-drop-zoom-and-csv-2c1404379e9a?source=collection_archive---------9----------------------->

![](img/4d62af93833a332dc9550cc022843c3c.png)

Photo by [Auto Fan](https://unsplash.com/@autofan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 拖放

我们可以使用 D3 轻松地将拖放操作添加到我们的 Vue 应用程序中。

例如，我们可以写:

```
<template>
  <div id="app">
    <svg>
      <g>
        <rect x="40" y="10" width="50" height="50" fill="teal"></rect>
      </g>
    </svg>
  </div>
</template>
<script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(() => {
      d3.select("g")
        .datum({
          x: 0,
          y: 0,
        })
        .call(
          d3.drag().on("drag", function (d) {
            d3.select(this).attr("transform", `translate(${d.x} , ${d.y})`);
          })
        );
    });
  },
};
</script>
```

我们有一个内部为矩形的 SVG。

在`nextTick`回调中，我们调用`d3.select`来获取`g`元素。

然后我们调用`datum`来设置左上角的`x`和`y`坐标。

然后我们通过将`d3.drag().on`方法传入`call`方法来调用`call`方法。

回调得到我们用`this`拖动的元素。

然后我们将`transform`属性设置为拖动位置。

# 变焦

我们可以给形状添加缩放功能。

有了它，我们可以使用鼠标滚轮来放大和缩小 SVG。

例如，我们可以写:

```
<template>
  <div id="app">
    <div id="zoom"></div>
  </div>
</template>
<script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(() => {
      const svg = d3
        .select("#zoom")
        .append("svg")
        .attr("width", 460)
        .attr("height", 460)
        .call(
          d3.zoom().on("zoom", function (d) {
            svg.attr("transform", d.transform);
          })
        )
        .append("g"); svg
        .append("circle")
        .attr("cx", 100)
        .attr("cy", 100)
        .attr("r", 40)
        .style("fill", "#68b2a1");
    });
  },
};
</script>
```

我们有一个 ID 为`zoom`的 div。

在`nextTick`回调中，我们获取 div，然后将`svg`元素添加到其中。

然后我们用`d3.zoom`方法调用`call`方法，这样我们就可以监视缩放。

`d.transform`有一根线可以根据我们放大或缩小的程度来改变尺寸。

然后我们加上可以放大和缩小的圆圈。

`cx`和`cy`有中心的 x 和 y 坐标。

`r`有半径。

`style`有填充样式。

# 读取逗号分隔的值

我们可以直接从格式化数据中读取数据。

例如，我们可以写:

```
<template>
  <div id="app"></div>
</template>
<script>
import * as d3 from "d3";
const string = `year,population\n2011,10\n2012,20\n2013,30\n`;
export default {
  name: "App",
  mounted() {
    const data = d3.csvParse(string, function (d) {
      return {
        year: new Date(+d.year, 0, 1),
        population: d.population,
      };
    });
    console.log(data);
  },
};
</script>
```

用`d3.csvParse`解析 CSV 字符串。

回调让我们在读取数据后返回转换后的数据。

读取条目后，我们返回我们想要的条目的新值。

# 结论

我们可以在我们的 Vue 应用程序中添加拖放、缩放和用 D3 读取 CSV 字符串。