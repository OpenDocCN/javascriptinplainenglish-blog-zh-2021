# 使用 vue2-simple-calendar 向我们的 Vue 应用程序添加简单日历

> 原文：<https://javascript.plainenglish.io/adding-a-simple-calendar-to-our-vue-app-with-vue2-simple-calendar-572090ec5798?source=collection_archive---------17----------------------->

![](img/be14759c40f68a653f6d5c4d67492216.png)

Photo by [Estée Janssens](https://unsplash.com/@esteejanssens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

手动添加日历小部件是非常痛苦的。

因此，创建了许多日历组件库。

vue2-simple-calendar 是一个库。

在本文中，我们将了解如何使用 vue2-simple-calendar 库添加日历。

# 入门指南

我们通过安装 NPM 来添加我们的库。

为此，我们运行:

```
npm i vue2-simple-calendar
```

# 使用日历组件

我们可以通过添加 CSS 代码来添加日历组件。

创建一个名为`vue2-simple-calendar.css`的文件，并添加:

```
.vue-calendar {
  display: grid;
  grid-template-rows: 10% 90%;
  background: #fff;
  margin: 0 auto;
}
.calendar-header {
  align-items: center;
}
.header-left,
.header-right {
  flex: 1;
}
.header-center {
  flex: 3;
  text-align: center;
}
.title {
  margin: 0 5px;
}
.next-month,
.prev-month {
  cursor: pointer;
}
.calendar-body {
  display: grid;
  grid-template-rows: 5% 95%;
}
.days-header {
  display: grid;
  grid-auto-columns: 14.25%;
  grid-template-areas: "a a a a a a a";
  border-top: 1px solid #e0e0e0;
  border-left: 1px solid #e0e0e0;
  border-bottom: 1px solid #e0e0e0;
}
.days-body {
  display: grid;
  grid-template-rows: auto;
}
.day-number {
  text-align: right;
  margin-right: 10px;
}
.day-label {
  text-align: center;
  border-right: 1px solid #e0e0e0;
}
.week-row {
  display: grid;
  grid-template-areas: "a a a a a a a";
  grid-row-gap: 5px;
  grid-auto-columns: 14.25%;
  border-left: 1px solid #e0e0e0;
}
.week-day {
  padding: 4px;
  border-right: 1px solid #e0e0e0;
  border-bottom: 1px solid #e0e0e0;
}
.week-day.disabled {
  background-color: #f5f5f5;
}
.week-day.not-current > .day-number {
  color: #c3c3c3;
}
.week-day.today > .day-number {
  font-weight: 700;
  color: red;
}
.events {
  font-size: 12px;
  cursor: pointer;
  padding: 0 0 0 4px;
}
.events .event {
  height: 18px;
  line-height: 18px;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
  margin: 0 4px 2px 0;
  color: rgba(0, 0, 0, 0.87);
  background-color: #d4dcec;
}
.events .more-link {
  color: rgba(0, 0, 0, 0.38);
}
```

这是相同的代码，就像在[https://codesandbox.io/s/93pjr734r4?的例子 file =/src/assets/vue 2-simple-calendar . CSS:0-1549](https://codesandbox.io/s/93pjr734r4?file=/src/assets/vue2-simple-calendar.css:0-1549)。

它没有任何样式，所以我们必须自己添加。

然后在`main.js`中，我们添加:

```
import Vue from "vue";
import App from "./App.vue";
import vueCalendar from "vue2-simple-calendar";
import "./assets/vue2-simple-calendar.css";Vue.use(vueCalendar, {});
Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

注册插件。

然后在我们的组件中，我们编写:

```
<template>
  <vue-calendar
    :show-limit="3"
    :events="events"
    @show-all="showAll"
    @day-clicked="dayClicked"
    @event-clicked="eventClicked"
    @month-changed="monthChanged"
  ></vue-calendar>
</template>

<script>
export default {
  methods: {
    showAll(events) {
      console.log(events);
    },
    dayClicked(day) {
      console.log(day);
    },
    eventClicked(event) {
      console.log(event);
    },
    monthChanged(start, end) {
      console.log(start, end);
    },
    highlightDays(days) {
      console.log(days);
    }
  },
  created() {
    this.$calendar.eventBus.$on("show-all", events => this.showAll(events));
    this.$calendar.eventBus.$on("day-clicked", day => this.dayClicked(day));
    this.$calendar.eventBus.$on("event-clicked", event =>
      this.eventClicked(event)
    );
    this.$calendar.eventBus.$on("month-changed", (start, end) =>
      this.monthChanged(start, end)
    );
  }
};
</script>
```

`vue-calendar`组件呈现日历。

它渲染各种事件。

`show-all`是我们显示日子时发出的。

`day-clicked`是我们点击某一天时发出的。

`event-clicked`是我们点击一个事件时发出的。

当我们更改日历上的月份时会发出`month-changed`。

# 结论

我们可以用 vue2-simple-calendar 组件添加一个简单的日历组件。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**