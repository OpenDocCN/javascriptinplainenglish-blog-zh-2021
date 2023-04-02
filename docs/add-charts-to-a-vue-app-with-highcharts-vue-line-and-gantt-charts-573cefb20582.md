# 使用 high Charts-Vue-折线图和甘特图向 Vue 应用程序添加图表

> 原文：<https://javascript.plainenglish.io/add-charts-to-a-vue-app-with-highcharts-vue-line-and-gantt-charts-573cefb20582?source=collection_archive---------5----------------------->

![](img/999d77b67cbc6ce3d90fd71ffe11c74e.png)

Photo by [Chris Liverani](https://unsplash.com/@chrisliverani?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Highcharts-Vue 是一个易于使用的库，允许我们将图表添加到我们的 Vue 应用程序中。

在本文中，我们将了解如何使用 highcharts-vue 库添加图表。

# 折线图

我们可以通过编写以下内容来添加折线图:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import HighchartsVue from "highcharts-vue";Vue.use(HighchartsVue);new Vue({
  el: "#app",
  render: (h) => h(App)
});
```

`App.vue`

```
<template>
  <div>
    <highcharts class="hc" :options="chartOptions" ref="chart"></highcharts>
  </div>
</template><script>
export default {
  data() {
    return {
      chartOptions: {
        series: [
          {
            data: [1, 2, 3],
          },
        ],
      },
    };
  },
};
</script>
```

我们注册了`HighchartsVue`插件，然后在`App.vue`中使用`highcharts`组件。

y 轴的数据在`series.data`属性中。

# 线条图

为了创建甘特图，我们编写:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import Highcharts from "highcharts";
import Gantt from "highcharts/modules/gantt";
import HighchartsVue from "highcharts-vue";Gantt(Highcharts);
Vue.use(HighchartsVue);new Vue({
  el: "#app",
  render: (h) => h(App)
});
```

`App.vue`

```
<template>
  <div>
    <highcharts
      :constructorType="'ganttChart'"
      class="hc"
      :options="chartOptions"
      ref="chart"
    ></highcharts>
  </div>
</template><script>
export default {
  data() {
    return {
      chartOptions: {
        title: {
          text: "Gantt Chart with Progress Indicators",
        },
        xAxis: {
          min: Date.UTC(2021, 10, 17),
          max: Date.UTC(2021, 10, 30),
        }, series: [
          {
            name: "Project 1",
            data: [
              {
                name: "Start",
                start: Date.UTC(2021, 10, 18),
                end: Date.UTC(2021, 10, 25),
                completed: 0.25,
              },
              {
                name: "Test",
                start: Date.UTC(2021, 10, 27),
                end: Date.UTC(2021, 10, 29),
              },
              {
                name: "Develop",
                start: Date.UTC(2021, 10, 20),
                end: Date.UTC(2021, 10, 25),
                completed: {
                  amount: 0.12,
                  fill: "#fa0",
                },
              },
              {
                name: "Test Again",
                start: Date.UTC(2021, 10, 23),
                end: Date.UTC(2021, 10, 26),
              },
            ],
          },
        ],
      },
    };
  },
};
</script>
```

我们调用`main.js`中的`Gantt`函数来添加甘特图。

然后我们可以使用`highcharts`组件来呈现图表。

`title`有标题。

`xAxis`具有 x 轴数值范围。

`series`有数据。

`name`有酒吧的名称。

`start`和`end`是开始和结束日期。

`completed`有进度值。

# 结论

我们可以使用 highcharts-vue 轻松添加折线图和甘特图。

*更多内容请看*[***plain English . io***](http://plainenglish.io)