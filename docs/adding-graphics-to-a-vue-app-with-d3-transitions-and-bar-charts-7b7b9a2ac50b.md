# 使用 D3 向 Vue 应用添加图形—过渡和条形图

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-vue-app-with-d3-transitions-and-bar-charts-7b7b9a2ac50b?source=collection_archive---------8----------------------->

![](img/302c5f3d5530e7e6b89a274fdd838350.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 过渡

我们可以使用 D3 来应用过渡。

例如，我们可以写:

```
<template>
  <div id="app"></div>
</template><script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(() => {
      const t = d3.transition().duration(2000);
      d3.select("body").transition(t).style("background-color", "lightblue");
    });
  },
};
</script>
```

调用`d3.transition`来创建我们的转换对象。

然后我们用`duration`方法设置它的持续时间。

2000 以毫秒为单位。

然后我们用`t`方法调用`transition`方法，在 2 秒内将`body`的背景颜色设置为`lightblue`。

# 动画

我们可以用 D3 添加动画。

例如，我们可以写:

```
<template>
  <div id="app">
    <h3>hello world</h3>
  </div>
</template><script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(() => {
      d3.selectAll("h3")
        .transition()
        .style("font-size", "28px")
        .delay(2000)
        .duration(2000);
    });
  },
};
</script>
```

我们得到了`h3`,然后在 2 秒钟后使字体大小为 28px。

然后我们在 2 秒钟内将大小更改为 28px。

# 绘制图表

D3 对于创建图表很有用。

我们可以用它来创建条形图，圆形图，饼图，甜甜圈，图表等。

# 条形图

我们可以用 D3 创建条形图。

例如，我们可以写:

```
<template>
  <div id="app">
    <div id="svgcontainer"></div>
  </div>
</template><script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  mounted() {
    Vue.nextTick(() => {
      const data = [13, 6, 11, 20, 13]; const width = 500;
      const scaleFactor = 20;
      const barHeight = 30; const graph = d3
        .select("#svgcontainer")
        .append("svg")
        .attr("width", width)
        .attr("height", barHeight * data.length); const bar = graph
        .selectAll("g")
        .data(data)
        .enter()
        .append("g")
        .attr("transform", (d, i) => {
          return "translate(0," + i * barHeight + ")";
        });
      bar
        .append("rect")
        .attr("width", (d) => {
          return d * scaleFactor;
        })
        .attr("height", barHeight - 1)
        .attr("fill", "green"); bar
        .append("text")
        .attr("x", (d) => {
          return d * scaleFactor;
        })
        .attr("y", barHeight / 2)
        .attr("dy", ".35em")
        .text((d) => {
          return d;
        })
        .attr("fill", "red");
    });
  },
};
</script>
```

我们在前几行中设置了条形图的常数和尺寸。

然后我们用下面的代码创建`g`元素:

```
const bar = graph
  .selectAll("g")
  .data(data)
  .enter()
  .append("g")
  .attr("transform", (d, i) => {
    return "translate(0," + i * barHeight + ")";
  });
```

安置酒吧。

接下来，我们使用以下内容为条形图创建矩形:

```
bar
  .append("rect")
  .attr("width", (d) => {
    return d * scaleFactor;
  })
  .attr("height", barHeight - 1)
  .attr("fill", "green");
```

`d`拥有`data`数组中的数字。

我们将它乘以`scaleFactor`得到条形的宽度。

我们将`height`设置为`barHeight — 1`来设置高度，并在条形之间添加一个间隙。

并且`'fill'`被设置为`'green'`。

然后，我们在条形的右侧添加:

```
bar
  .append("text")
  .attr("x", (d) => {
    return d * scaleFactor;
  })
  .attr("y", barHeight / 2)
  .attr("dy", ".35em")
  .text((d) => {
    return d;
  })
  .attr("fill", "red");
```

`'x'`和`'y'`属性设置文本的位置。

`x`在杠后，`y`是`barHeight / 2`。

我们还必须移动`y`坐标，使文本与条对齐。

所以我们将`dy`属性设置为`.35em`。

然后我们返回数字并用`text`方法将其设置为文本。

然后我们调用`attr`，将`'fill'`设置为`'red'`。

# 结论

我们可以在我们的 Vue 应用程序中添加带有 D3 的过渡和条形图。

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**