# 使用 D3 向 Vue 应用添加图形

> 原文：<https://javascript.plainenglish.io/adding-graphics-to-a-vue-app-with-d3-8bdfc92a8235?source=collection_archive---------8----------------------->

![](img/9ab337004ead92ef230b907d1075a894.png)

Photo by [Alekon pictures](https://unsplash.com/@alekonpictures?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

D3 让我们可以轻松地向前端 web 应用添加图形。

Vue 是一个流行的前端 web 框架。

他们合作得很好。在本文中，我们将了解如何使用 D3 为 Vue 应用添加图形。

# 入门指南

我们通过运行`npm i d3`来安装 D3。

然后我们可以在我们的 Vue 应用程序中使用它。

# 数据连接

现在我们安装了 D3，我们可以在我们的应用程序中使用它。

D3 让我们可以轻松地将一组条目呈现到一个列表中。

为此，我们写道:

```
<template>
  <div id="app">
    <ul id="list">
      <li v-for="n of arr.length"></li>
    </ul>
  </div>
</template><script>
import * as d3 from "d3";
import Vue from "vue";export default {
  name: "App",
  data() {
    return {
      arr: [10, 20, 30, 25, 15],
    };
  },
  mounted() {
    Vue.nextTick(() => {
      d3.select("#list")
        .selectAll("li")
        .data(this.arr)
        .text((d) => d);
    });
  },
};
</script>
```

将`arr`中的数字呈现到`li`元素中。

`d3.select`选择 ID 为`list`的`ul`。

然后我们调用`selectAll`来选择里面所有的`li`。

然后我们调用`data`返回数据。

和`text`来设置每个`li`的文本。

现在数字应该在列表中了。

D3 代码在`Vue.nextTick`回调中，这样我们就可以在`li`被渲染后得到它们。

# 挽救（saving 的简写）

我们可以用 D3 在 Vue 应用中添加 SVG。

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
      const width = 300;
      const height = 300;
      const svg = d3
        .select("#svgcontainer")
        .append("svg")
        .attr("width", width)
        .attr("height", height);
      svg
        .append("line")
        .attr("x1", 100)
        .attr("y1", 100)
        .attr("x2", 200)
        .attr("y2", 200)
        .style("stroke", "rgb(255,0,0)")
        .style("stroke-width", 2);
    });
  },
};
</script>
```

我们选择 ID 为`svgcontainer`的 div。

然后我们用`attr`方法设置`svg`的宽度和高度。

然后我们用带有`'line'`参数的`append`方法添加一行。

我们设置`x1`和`y1`属性来添加线条起点的 x 和 y 坐标。

我们对属性为`x2`和`y2`的行尾做同样的处理。

`style`方法设置样式。

`stroke`设置线条颜色，`stroke-width`设置线条宽度。

# 矩形

我们可以通过调用带有`'rect'`参数的`append`方法来添加一个矩形:

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
      const width = 300;
      const height = 300;
      const svg = d3
        .select("#svgcontainer")
        .append("svg")
        .attr("width", width)
        .attr("height", height);
      svg
        .append("rect")
        .attr("x", 20)
        .attr("y", 20)
        .attr("width", 200)
        .attr("height", 100)
        .attr("fill", "green");
    });
  },
};
</script>
```

然后我们设置`x`和`y`属性来添加矩形左上角的 x 和 y 坐标。

并且我们用`'width'`和`'height'`调用`attr`来设置矩形的宽度和高度。

`'fill'`设置矩形的背景颜色。

# 结论

我们可以用 D3 给我们的 Vue 应用添加基本形状。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**