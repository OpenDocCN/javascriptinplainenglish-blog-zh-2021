# 使用 Vue-FullCalendar 将日历添加到 Vue 应用程序

> 原文：<https://javascript.plainenglish.io/add-a-calendar-into-a-vue-app-with-vue-fullcalendar-79b1db7fd6c1?source=collection_archive---------15----------------------->

![](img/de2c5f239f495f5fa58bcea60d8387c1.png)

Photo by [Mockaroon](https://unsplash.com/@mockaroon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

日历是很难从头开始创建的东西。

因此，有许多为 Vue 应用程序创建的日历组件。

在本文中，我们将了解如何使用 Vue-FullCalendar 添加日历。

# 装置

我们可以通过以下方式安装 Vue-FullCalendar 及其插件:

```
npm install --save @fullcalendar/vue @fullcalendar/daygrid @fullcalendar/interaction
```

`@fullcalendar/vue`有 Vue-FullCalendar 插件。

`@fullcalendar/daygrid`让我们在日历中显示日网格。

`@fullcalendar/interaction`让我们与日历互动。

然后，我们可以通过编写以下代码将日历添加到 Vue 组件中:

```
<template>
  <FullCalendar :options="calendarOptions" />
</template><script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
      },
    };
  },
};
</script>
```

属性让我们添加插件来添加我们安装的插件。

并且`initialView`被设置为`'dayGridMonth'`，让我们显示一个以今天的日期作为默认日期的月历。

要将事件添加到日历中，我们可以添加`calendarOptions.events`属性:

```
<template>
  <FullCalendar :options="calendarOptions" />
</template><script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        events: [
          { title: "event 1", date: "2020-12-01" },
          { title: "event 2", date: "2020-12-02" },
        ],
      },
    };
  },
};
</script>
```

`title`有活动标题，`date`有活动日期。

为了监听像点击日期这样的事件，我们可以添加更多的属性。

为了监听日期点击，我们添加了`dateClick`属性:

```
<template>
  <FullCalendar :options="calendarOptions" />
</template><script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        events: [
          { title: "event 1", date: "2020-12-01" },
          { title: "event 2", date: "2020-12-02" },
        ],
        dateClick: this.onDateClick,
      },
    };
  },
  methods: {
    onDateClick(arg) {
      console.log(arg.dateStr);
    },
  },
};
</script>
```

我们将它设置为`onDateClick`事件处理程序，当我们单击一个日期时运行它。

我们可以获得用`dateStr`属性点击的日期的日期字符串。

我们可以添加其他选项，如显示或隐藏周末。

要隐藏周末，我们可以将`calendarOptions.weekends`属性设置为`false`:

```
<template>
  <FullCalendar :options="calendarOptions" />
</template><script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        events: [
          { title: "event 1", date: "2020-12-01" },
          { title: "event 2", date: "2020-12-02" },
        ],
        weekends: false,
      },
    };
  },
};
</script>
```

它还附带了一些有用的实用程序，比如用我们的方式格式化日期的`formatDate`函数:

```
<template>
  <FullCalendar :options="calendarOptions" />
</template><script>
import FullCalendar from "@fullcalendar/vue";
import dayGridPlugin from "@fullcalendar/daygrid";
import interactionPlugin from "@fullcalendar/interaction";
import { formatDate } from "@fullcalendar/vue";const str = formatDate(new Date(), {
  month: "long",
  year: "numeric",
  day: "numeric",
});console.log(str);export default {
  components: {
    FullCalendar,
  },
  data() {
    return {
      calendarOptions: {
        plugins: [dayGridPlugin, interactionPlugin],
        initialView: "dayGridMonth",
        events: [
          { title: "event 1", date: "2020-12-01" },
          { title: "event 2", date: "2020-12-02" },
        ],
        weekends: false,
      },
    };
  },
};
</script>
```

# 结论

我们可以添加 Vue-FullCalendar 库，轻松地将活动日历添加到我们的 Vue 应用程序中。

*阅读更多尽在* [***说白了. io***](https://plainenglish.io/)