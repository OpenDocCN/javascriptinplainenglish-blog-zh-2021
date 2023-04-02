# 使用 vue-simple-calendar 向我们的 Vue 应用程序添加简单日历

> 原文：<https://javascript.plainenglish.io/adding-a-simple-calendar-to-our-vue-app-with-vue-simple-calendar-b0d176cf523?source=collection_archive---------16----------------------->

![](img/1edc9c7860fb48f658d38dc6861629d0.png)

Photo by [Estée Janssens](https://unsplash.com/@esteejanssens?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

手动添加日历小部件是非常痛苦的。

因此，创建了许多日历组件库。

简单日历是一个库。

在本文中，我们将看看如何使用
vue-simple-calendar 库添加日历。

# 入门指南

我们通过安装 NPM 来添加我们的库。

为此，我们运行:

```
npm i vue-simple-calendar
```

# 添加简单日历

我们可以用`calendar-view`组件添加一个简单的日历。

为了补充它，我们写道:

```
<template>
  <div id="app">
    <calendar-view
      :show-date="showDate"
      class="theme-default holiday-us-traditional holiday-us-official"
    >
      <calendar-view-header
        slot="header"
        slot-scope="t"
        :header-props="t.headerProps"
        @input="setShowDate"
      />
    </calendar-view>
  </div>
</template>
<script>
import { CalendarView, CalendarViewHeader } from "vue-simple-calendar";
import "vue-simple-calendar/static/css/default.css";
import "vue-simple-calendar/static/css/holidays-us.css";export default {
  name: "app",
  data() {
    return { showDate: new Date() };
  },
  components: {
    CalendarView,
    CalendarViewHeader
  },
  methods: {
    setShowDate(d) {
      this.showDate = d;
    }
  }
};
</script>
```

我们导入 CSS 并在组件中注册组件。

属性有一个日期对象，它控制要显示的月份。

`calendar-view-header`组件有一个标题，可以让我们浏览月份。

当我们在标题上选择一个月份时，就会发出`input`事件。

# 添加日历事件

我们可以设置`events`道具来用事件填充日历。

例如，我们可以写:

```
<template>
  <div id="app">
    <calendar-view
      :show-date="showDate"
      :events="events"
      class="theme-default holiday-us-traditional holiday-us-official"
      @click-date="onClickDate"
    >
      <calendar-view-header
        slot="header"
        slot-scope="t"
        :header-props="t.headerProps"
        @input="setShowDate"
      />
    </calendar-view>
  </div>
</template>
<script>
import { CalendarView, CalendarViewHeader } from "vue-simple-calendar";
import "vue-simple-calendar/static/css/default.css";
import "vue-simple-calendar/static/css/holidays-us.css";export default {
  name: "app",
  data() {
    return {
      showDate: new Date(),
      events: [
        {
          id: 1,
          startDate: "2020-10-19",
          endDate: "2020-10-19",
          title: "Sample event 1"
        },
        {
          id: 2,
          startDate: "2020-10-06",
          endDate: "2020-10-13",
          title: "Sample event 2"
        }
      ]
    };
  },
  components: {
    CalendarView,
    CalendarViewHeader
  },
  methods: {
    setShowDate(d) {
      this.showDate = d;
    },
    onClickDate(...params) {
      console.log(params);
    }
  }
};
</script>
```

我们有一个`events`数组，我们将它设置为`events`属性的值。

每个条目都有带有唯一 ID 的`id`。

`startDate`有活动的开始日期。

`endDate`有事件的结束日期。

`title`有事件的标题。

`id`和`startDate`为必填项。

`title`默认为`'untitled'`。

它还发出我们可以监听的事件。

例如，我们可以监听`click-date`事件，它将我们点击的日期和鼠标事件作为参数。

这些事件将显示在日历上。

# 时间

vue-simple-calendar 可以通过填充不同的槽来定制。

`periodStart`让我们自定义显示期间的第一个日期。

`periodEnd`让我们自定义显示周期的最后日期。

`displayLocale`让我们显示日历的区域设置。

`monthNames`设置月份名称。

在 https://github.com/richardtallent/vue-simple-calendar#slots 的[有更多的职位。](https://github.com/richardtallent/vue-simple-calendar#slots)

# 结论

vue-simple-calendar 是一个简单的库，用于向我们的 vue 应用程序添加日历。

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**