# 使用 D3 向 Vue 应用程序添加图形—饼图

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-vue-app-with-d3-pie-chart-63b39251ee96?source=collection_archive---------14----------------------->

![](img/ecbd432f9d88be74ae2e80f187a3aa29.png)

Photo by [sheri silver](https://unsplash.com/@sheri_silver?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以很容易地将图形添加到前端网络应用程序中。

Vue 是一个流行的前端网络框架。

他们一起工作很棒。在本文中，我们将研究如何将图形添加到带有 D3 的 Vue 应用程序中。

# 圆形分格统计图表

我们可以在 Vue 应用程序中添加一个包含 D3 的饼图。

例如，我们可以写:

`public/populations.csv`

```
states,percent
California,38.00
New York,18.00
Texas,20.0
```

`App.vue`

```
<template>
  <div id="app">
    <svg width="600" height="400"></svg>
  </div>
</template>
<script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(async () => {
      const svg = d3.select("svg"),
        width = svg.attr("width"),
        height = svg.attr("height"),
        radius = Math.min(width, height) / 2; const g = svg
        .append("g")
        .attr("transform", `translate(${width / 2}, ${height / 2})`); const color = d3.scaleOrdinal(["gray", "green", "brown"]); const pie = d3.pie().value(function (d) {
        return d.percent;
      }); const path = d3
        .arc()
        .outerRadius(radius - 10)
        .innerRadius(0); const label = d3
        .arc()
        .outerRadius(radius)
        .innerRadius(radius - 80); const data = await d3.csv("/populations.csv"); const arc = g
        .selectAll(".arc")
        .data(pie(data))
        .enter()
        .append("g")
        .attr("class", "arc"); arc
        .append("path")
        .attr("d", path)
        .attr("fill", function (d) {
          return color(d.data.states);
        }); arc
        .append("text")
        .attr("transform", function (d) {
          return `translate(${label.centroid(d)})`;
        })
        .text(function (d) {
          return d.data.states;
        }); svg
        .append("g")
        .attr("transform", `translate(${width / 2 - 120},20)`)
        .append("text")
        .text("Top population states in the US")
        .attr("class", "title");
    });
  },
};
</script><style scoped>
.arc text {
  font: 12px arial;
  text-anchor: middle;
}.arc path {
  stroke: #fff;
}.title {
  fill: green;
  font-weight: italic;
}
</style>
```

我们首先获取`svg`元素，并设置饼图的`width`、`height`和`radius`:

```
const svg = d3.select("svg"),
  width = svg.attr("width"),
  height = svg.attr("height"),
  radius = Math.min(width, height) / 2;
```

然后我们通过写作来翻译`svg`:

```
const g = svg
  .append("g")
  .attr("transform", `translate(${width / 2}, ${height / 2})`);
```

接下来，我们通过书写为饼图添加颜色；

```
const color = d3.scaleOrdinal(["gray", "green", "brown"]);
```

然后，我们通过编写以下内容来添加饼图块的数据:

```
const pie = d3.pie().value(function(d) {
  return d.percent;
});
```

接下来，我们通过书写为饼图创建弧线

```
const path = d3
  .arc()
  .outerRadius(radius - 10)
  .innerRadius(0);
```

然后，我们通过书写来创建标签:

```
const label = d3
  .arc()
  .outerRadius(radius)
  .innerRadius(radius - 80);
```

然后我们从`populations.csv`读取数据:

```
const data = await d3.csv("/populations.csv");
```

然后，我们通过写入读取的数据来设置弧线的长度:

```
const arc = g
  .selectAll(".arc")
  .data(pie(data))
  .enter()
  .append("g")
  .attr("class", "arc");
```

然后，我们通过书写来设置饼图块的填充颜色:

```
arc
  .append("path")
  .attr("d", path)
  .attr("fill", function(d) {
    return color(d.data.states);
  });
```

然后，我们通过编写以下内容来添加饼图块的文本:

```
arc
  .append("text")
  .attr("transform", function(d) {
    return `translate(${label.centroid(d)})`;
  })
  .text(function(d) {
    return d.data.states;
  });
```

最后，我们通过以下方式为图表添加标题文本:

```
svg
  .append("g")
  .attr("transform", `translate(${width / 2 - 120},20)`)
  .append("text")
  .text("Top population states in the US")
  .attr("class", "title");
```

现在，我们应该看到一个饼图显示。

# 结论

我们可以在 Vue 应用程序中添加一个包含 D3 的饼图。