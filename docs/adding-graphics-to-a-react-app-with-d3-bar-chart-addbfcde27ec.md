# 使用 D3 向 React 应用程序添加图形—条形图

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-react-app-with-d3-bar-chart-addbfcde27ec?source=collection_archive---------13----------------------->

![](img/9b9c02b574924de64b4c4953d80d5408.png)

Photo by [Alex Knight](https://unsplash.com/@agkdesign?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 创建条形图

我们可以在 React 应用程序中用 D3 创建一个条形图，方法是读入数据，创建轴，然后添加条形。

例如，我们可以写:

`public/data.csv`

```
year,population
2006,20
2008,25
2010,38
2012,61
2014,43
2016,26
2017,62
```

`src/App.js`

```
import React, { useEffect } from "react";
import * as d3 from "d3";const createBarChart = async () => {
  const svg = d3.select("svg"),
    margin = 200,
    width = svg.attr("width") - margin,
    height = svg.attr("height") - margin; svg
    .append("text")
    .attr("transform", "translate(100,0)")
    .attr("x", 50)
    .attr("y", 50)
    .attr("font-size", "20px")
    .attr("class", "title")
    .text("Population bar chart"); const x = d3.scaleBand().range([0, width]).padding(0.4),
    y = d3.scaleLinear().range([height, 0]);
  const g = svg.append("g").attr("transform", "translate(100, 100)");
  const data = await d3.csv("data.csv"); x.domain(
    data.map(function (d) {
      return d.year;
    })
  );
  y.domain([
    0,
    d3.max(data, function (d) {
      return d.population;
    })
  ]); g.append("g")
    .attr("transform", `translate(0, ${height})`)
    .call(d3.axisBottom(x))
    .append("text")
    .attr("y", height - 250)
    .attr("x", width - 100)
    .attr("text-anchor", "end")
    .attr("font-size", "18px")
    .attr("stroke", "blue")
    .text("year"); g.append("g")
    .append("text")
    .attr("transform", "rotate(-90)")
    .attr("y", 6)
    .attr("dy", "-5.1em")
    .attr("text-anchor", "end")
    .attr("font-size", "18px")
    .attr("stroke", "blue")
    .text("population"); g.append("g").attr("transform", "translate(0, 0)").call(d3.axisLeft(y));
  g.selectAll(".bar")
    .data(data)
    .enter()
    .append("rect")
    .attr("class", "bar")
    .style("fill", "lightgreen")
    .on("mouseover", onMouseOver)
    .on("mouseout", onMouseOut)
    .attr("x", function (d) {
      return x(d.year);
    })
    .attr("y", function (d) {
      return y(d.population);
    })
    .attr("width", x.bandwidth())
    .transition()
    .ease(d3.easeLinear)
    .duration(200)
    .delay(function (d, i) {
      return i * 25;
    })
    .attr("height", function (d) {
      return height - y(d.population);
    }); function onMouseOver(d, i) {
    d3.select(this).attr("class", "highlight"); d3.select(this)
      .transition()
      .duration(200)
      .attr("width", x.bandwidth() + 5)
      .attr("y", function (d) {
        return y(d.population) - 10;
      })
      .attr("height", function (d) {
        return height - y(d.population) + 10;
      }); g.append("text")
      .attr("class", "val")
      .attr("x", function () {
        return x(d.year);
      })
      .attr("y", function () {
        return y(d.value) - 10;
      });
  } function onMouseOut(d, i) {
    d3.select(this).attr("class", "bar"); d3.select(this)
      .transition()
      .duration(200)
      .attr("width", x.bandwidth())
      .attr("y", function (d) {
        return y(d.population);
      })
      .attr("height", function (d) {
        return height - y(d.population);
      }); d3.selectAll(".val").remove();
  }
};export default function App() {
  useEffect(() => {
    createBarChart();
  }, []); return (
    <div className="App">
      <svg width="500" height="500"></svg>
    </div>
  );
}
```

我们在模板中添加了`svg`元素。

然后我们写下标题:

```
svg
  .append("text")
  .attr("transform", "translate(100,0)")
  .attr("x", 50)
  .attr("y", 50)
  .attr("font-size", "20px")
  .attr("class", "title")
  .text("Population bar chart");
```

`x`和`y`是文本左上角的 x 和 y 坐标。

`transform`通过翻译来转换文本。

`font-size`有标题的字体大小。

然后我们创建用于轴的`x`和`y`范围:

```
const x = d3.scaleBand().range([0, width]).padding(0.4),
  y = d3.scaleLinear().range([height, 0]);
const g = svg.append("g").attr("transform", "translate(100, 100)");
const data = await d3.csv("data.csv");

x.domain(
  data.map(function(d) {
    return d.year;
  })
);
y.domain([
  0,
  d3.max(data, function(d) {
    return d.population;
  }),
]);
```

我们用`domain`方法设置`x`和`y`的域。

然后我们用`axisBottom`方法创建 x 轴:

```
g.append("g")
  .attr("transform", `translate(0, ${height})`)
  .call(d3.axisBottom(x))
  .append("text")
  .attr("y", height - 250)
  .attr("x", width - 100)
  .attr("text-anchor", "end")
  .attr("font-size", "18px")
  .attr("stroke", "blue")
  .text("year");
```

`attr`方法设置所有的 CSS 样式。

然后，我们通过书写来添加 y 轴的标签:

```
g.append("g")
  .append("text")
  .attr("transform", "rotate(-90)")
  .attr("y", 6)
  .attr("dy", "-5.1em")
  .attr("text-anchor", "end")
  .attr("font-size", "18px")
  .attr("stroke", "blue")
  .text("population");
```

然后我们加上 y 轴本身，写为:

```
g.append("g").attr("transform", "translate(0, 0)").call(d3.axisLeft(y));
```

我们通过书写来添加小节:

```
g.selectAll(".bar")
  .data(data)
  .enter()
  .append("rect")
  .attr("class", "bar")
  .style("fill", "lightgreen")
  .on("mouseover", onMouseOver)
  .on("mouseout", onMouseOut)
  .attr("x", function(d) {
    return x(d.year);
  })
  .attr("y", function(d) {
    return y(d.population);
  })
  .attr("width", x.bandwidth())
  .transition()
  .ease(d3.easeLinear)
  .duration(200)
  .delay(function(d, i) {
    return i * 25;
  })
  .attr("height", function(d) {
    return height - y(d.population);
  });
```

我们添加了一个`mouseover`事件监听器，当我们将鼠标悬停在它上面时，它会展开该栏。

此外，我们添加了`mouseout`事件监听器，以便在我们将鼠标从工具条上移开时将工具条恢复到其原始大小。

我们设置了`x`和`y`属性，这样我们可以将它定位在 x 轴上。

然后，当它加载`transition`、`ease`和`duration`调用时，我们添加一些转换。

最后，我们通过在最后一个`attr`调用中设置`height`属性，将条形的高度设置为。

# 结论

我们可以用 D3 从 CSV 数据创建一个条形图。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**