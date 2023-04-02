# 使用 Vue-Simple-Calendar 将日历添加到 Vue 应用程序

> 原文：<https://javascript.plainenglish.io/add-a-calendar-into-a-vue-app-with-vue-simple-calendar-3039323c706?source=collection_archive---------16----------------------->

![](img/5aac6c9e4a16642372f183cd43c5b2fd.png)

Photo by [JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

日历是很难从头开始创建的东西。

因此，有许多为 Vue 应用程序创建的日历组件。

在本文中，我们将了解如何使用 Vue-Simple-Calendar 添加日历。

# 装置

我们可以通过运行以下命令来安装插件:

```
npm i --save vue-simple-calendar
```

# 使用

一旦我们安装了它，我们就可以通过编写以下内容来使用日历:

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
        [@input](http://twitter.com/input)="setShowDate"
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
    CalendarViewHeader,
  },
  methods: {
    setShowDate(d) {
      this.showDate = d;
    },
  },
};
</script>
```

我们设置`show-date`属性来设置默认日期。

然后我们填充`header`槽来显示带有`calendar-view-header`组件的标题渲染。

这让我们可以导航到不同的月份。

我们可以设置 show`displayPeriodUom`属性来显示日历中不同种类的时间段。

我们可以设置`year`来显示年份，设置`week`来显示星期。

默认为`month`。

我们也可以用`startingDayOfWeek`道具设置一周的开始日期。

`dateClasses`是一个对象，不同的日期有不同的日期类。

我们可以通过添加更多道具来增加更多选项:

```
<template>
  <div id="app">
    <div class="calendar-controls">
      <div v-if="message" class="notification is-success">{{ message }}</div> <div class="box">
        <div class="field">
          <label class="label">Period UOM</label>
          <div class="control">
            <div class="select">
              <select v-model="displayPeriodUom">
                <option>month</option>
                <option>week</option>
                <option>year</option>
              </select>
            </div>
          </div>
        </div>
        <div class="field">
          <label class="label">Period Count</label>
          <div class="control">
            <div class="select">
              <select v-model="displayPeriodCount">
                <option :value="1">1</option>
                <option :value="2">2</option>
                <option :value="3">3</option>
              </select>
            </div>
          </div>
        </div>
        <div class="field">
          <label class="checkbox">
            <input v-model="useTodayIcons" type="checkbox" />
            Use icon for today's period
          </label>
        </div>
        <div class="field">
          <label class="checkbox">
            <input v-model="displayWeekNumbers" type="checkbox" />
            Show week number
          </label>
        </div>
        <div class="field">
          <label class="checkbox">
            <input v-model="showTimes" type="checkbox" />
            Show times
          </label>
        </div>
        <div class="field">
          <label class="label">Themes</label>
          <label class="checkbox">
            <input v-model="useDefaultTheme" type="checkbox" />
            Default
          </label>
        </div>
        <div class="field">
          <label class="checkbox">
            <input v-model="useHolidayTheme" type="checkbox" />
            Holidays
          </label>
        </div>
      </div> <div class="box">
        <div class="field">
          <label class="label">Title</label>
          <div class="control">
            <input v-model="newItemTitle" class="input" type="text" />
          </div>
        </div>
        <div class="field">
          <label class="label">Start date</label>
          <div class="control">
            <input v-model="newItemStartDate" class="input" type="date" />
          </div>
        </div>
        <div class="field">
          <label class="label">End date</label>
          <div class="control">
            <input v-model="newItemEndDate" class="input" type="date" />
          </div>
        </div>
        <button class="button is-info" @click="clickTestAddItem">
          Add Item
        </button>
      </div>
    </div>
    <div class="calendar-parent">
      <calendar-view
        :items="items"
        :show-date="showDate"
        :time-format-options="{ hour: 'numeric', minute: '2-digit' }"
        :enable-drag-drop="true"
        :disable-past="disablePast"
        :disable-future="disableFuture"
        :show-times="showTimes"
        :date-classes="myDateClasses"
        :display-period-uom="displayPeriodUom"
        :display-period-count="displayPeriodCount"
        :starting-day-of-week="startingDayOfWeek"
        :period-changed-callback="periodChanged"
        :current-period-label="useTodayIcons ? 'icons' : ''"
        :displayWeekNumbers="displayWeekNumbers"
        :enable-date-selection="true"
        :selection-start="selectionStart"
        :selection-end="selectionEnd"
        @date-selection-start="setSelection"
        @date-selection="setSelection"
        @date-selection-finish="finishSelection"
        @click-date="onClickDay"
        @click-item="onClickItem"
      >
        <calendar-view-header
          slot="header"
          slot-scope="{ headerProps }"
          :header-props="headerProps"
          @input="setShowDate"
        />
      </calendar-view>
    </div>
  </div>
</template>
<script>
import { CalendarView, CalendarViewHeader } from "vue-simple-calendar";
import "vue-simple-calendar/static/css/default.css";
import "vue-simple-calendar/static/css/holidays-us.css";export default {
  name: "app",
  components: {
    CalendarView,
    CalendarViewHeader,
  },
  data() {
    return {
      showDate: this.thisMonth(1),
      message: "",
      startingDayOfWeek: 0,
      disablePast: false,
      disableFuture: false,
      displayPeriodUom: "month",
      displayPeriodCount: 1,
      displayWeekNumbers: false,
      showTimes: true,
      selectionStart: null,
      selectionEnd: null,
      newItemTitle: "",
      newItemStartDate: "",
      newItemEndDate: "",
      useDefaultTheme: true,
      useHolidayTheme: true,
      useTodayIcons: false,
      items: [
        {
          id: "e0",
          startDate: "2020-01-05",
        },
        {
          id: "e1",
          startDate: new Date(),
        },
        {
          id: "e2",
          startDate: new Date(2020, 11, 1),
          endDate: new Date(2020, 11, 10),
          title: "Multi-day item with a long title and times",
        },
      ],
    };
  },
  computed: {
    userLocale() {
      return this.getDefaultBrowserLocale;
    },
    myDateClasses() {
      const o = {
        ides: new Date().getDate() === 1,
      };
      return o;
    },
  },
  methods: {
    periodChanged() {},
    thisMonth(d, h, m) {
      const t = new Date();
      return new Date(t.getFullYear(), t.getMonth(), d, h || 0, m || 0);
    },
    onClickDay(d) {
      this.selectionStart = null;
      this.selectionEnd = null;
      this.message = `You clicked: ${d.toLocaleDateString()}`;
    },
    onClickItem(e) {
      this.message = `You clicked: ${e.title}`;
    },
    setShowDate(d) {
      this.message = `Changing calendar view to ${d.toLocaleDateString()}`;
      this.showDate = d;
    },
    setSelection(dateRange) {
      this.selectionEnd = dateRange[1];
      this.selectionStart = dateRange[0];
    },
    finishSelection(dateRange) {
      this.setSelection(dateRange);
      this.message = `You selected: ${this.selectionStart.toLocaleDateString()} -${this.selectionEnd.toLocaleDateString()}`;
    },
    clickTestAddItem() {
      this.items.push({
        startDate: this.newItemStartDate,
        endDate: this.newItemEndDate,
        title: this.newItemTitle,
        id: "e" + Math.random().toString(36).substr(2, 10),
      });
      this.message = "You added a calendar item!";
    },
  },
};
</script>
```

我们使用`clickTestAddItem`方法将项目添加到`items`数组中，以添加日历事件。

我们还有选择元素来改变显示的周期和周期数。

# 结论

我们可以添加 Vue-Simple-Calendar 组件，在我们的 Vue 应用程序中添加带有许多选项的活动日历。

喜欢这篇文章吗？如果有，请在[**plain English . io**](https://plainenglish.io/)找到更多类似内容