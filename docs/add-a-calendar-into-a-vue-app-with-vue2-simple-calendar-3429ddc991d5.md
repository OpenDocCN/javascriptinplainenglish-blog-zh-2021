# 使用 Vue2-Simple-Calendar 将日历添加到 Vue 应用程序

> 原文：<https://javascript.plainenglish.io/add-a-calendar-into-a-vue-app-with-vue2-simple-calendar-3429ddc991d5?source=collection_archive---------16----------------------->

![](img/a393583b1563e96d0d65cbd4f1bb5aaf.png)

Photo by [Waldemar Brandt](https://unsplash.com/@waldemarbrandt67w?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

日历是很难从头开始创建的东西。

因此，有许多为 Vue 应用程序创建的日历组件。

在本文中，我们将了解如何使用 Vue2-Simple-Calendar 添加日历。

# vue 2-简单日历

我们可以通过运行以下命令来安装 Vue2-Simple-Calendar:

```
npm install vue2-simple-calendar
```

与 NPM 或:

```
yarn add vue2-simple-calendar
```

然后我们可以通过写来使用它:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import vueCalendar from "vue2-simple-calendar";
import "./assets/calendar.css";Vue.use(vueCalendar, {});
Vue.config.productionTip = false;new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div id="app">
    <vue-calendar
      :show-limit="3"
      :events="events"
      :disable="disabledDays"
      :highlight="highlightDays"
      @show-all="showAll"
      @day-clicked="dayClicked"
      @event-clicked="eventClicked"
      @month-changed="monthChanged"
    ></vue-calendar>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      events: [
        {
          title: "event",
          start: new Date(),
          end: new Date(),
        },
      ],
      disabledDays: {
        to: new Date(2020, 9, 5),
        from: new Date(2020, 11, 26),
      },
      highlightDays: {
        days: [6, 0],
      },
    };
  },
  methods: {
    showAll(events) {
      // Do something...
    },
    dayClicked(day) {
      // Do something...
    },
    eventClicked(event) {
      // Do something...
    },
    monthChanged(start, end) {
      // Do something...
    },
  },
  created() {
    this.$calendar.eventBus.$on("show-all", (events) => this.showAll(events));
    this.$calendar.eventBus.$on("day-clicked", (day) => this.dayClicked(day));
    this.$calendar.eventBus.$on("event-clicked", (event) => console.log(event));
    this.$calendar.eventBus.$on("month-changed", (start, end) =>
      console.log(start, end)
    );
  },
};
</script>
```

`/assets/calendar.css`

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

我们用`days-header`和`week-row`类添加网格布局。

在`main.js`中，我们添加了`VueCalendar`插件，这样我们就可以在我们的组件中使用它。

我们需要导入`calendar.css`来应用 CSS 样式中的样式。

在`App.vue`中，我们添加了`vue-calendar`组件来添加日历。

`show-limit`显示一天中的最大事件数。

`events`有一个事件数组。

`disable`有我们想要禁用的日期。

`show-all`当单击“显示更多”链接时，发出事件。

`day-clicked`点击某一天时发出。

`event-clicked`点击事件时发出。

`month-changed`在月份改变时发出。

# 结论

Vue2-Simple-Calendar 让我们可以轻松地将活动日历添加到我们的 Vue 应用程序中。

喜欢这篇文章吗？如果有，请在[**plain English . io**](https://plainenglish.io/)获取更多类似内容