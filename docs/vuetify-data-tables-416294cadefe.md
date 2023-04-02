# 虚拟化—数据表

> 原文：<https://javascript.plainenglish.io/vuetify-data-tables-416294cadefe?source=collection_archive---------9----------------------->

![](img/639068d5dab180e1814c4489239b15c7.png)

Photo by [Andrew Barrowman](https://unsplash.com/@barrowmanphotography?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuetify 是一个流行的 Vue 应用程序 UI 框架。

在本文中，我们将了解如何使用 Vuetify 框架。

# 数据表

`v-data-table`组件用于显示表格数据。

它包括排序、搜索、分页、编辑和行选择等功能。

例如，我们可以写:

```
<template>
  <v-data-table
    v-model="selected"
    :headers="headers"
    :items="desserts"
    :single-select="singleSelect"
    item-key="name"
    show-select
    class="elevation-1"
  >
    <template v-slot:top>
      <v-subheader>Dessert</v-subheader>
    </template>
  </v-data-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    singleSelect: false,
    selected: [],
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
    ],
    desserts: [
      {
        name: "Frozen Yogurt",
        calories: 159,
        fat: 6.0,
      },
      {
        name: "Ice cream sandwich",
        calories: 237,
        fat: 9.0,
      },
      {
        name: "Eclair",
        calories: 262,
        fat: 16.0,
      },
    ],
  }),
};
</script>
```

我们有了`v-data-table`组件来添加我们的表。

`v-model`有选中的行。

`items`有要展示的物品。

`single-select`让我们切换单选。

`headers`道具有头部。

该值是一个包含一些对象的数组。

`text`属性有列标题文本。

`align`有文字对齐。

`sortable`让我们设置它是否可排序。

`value`有要显示的条目的属性名。

自动包含分页。

# 分组行

我们可以用`group-by`和`group-desc`道具将不同的行组合在一起。

例如，我们可以写:

```
<template>
  <v-data-table
    v-model="selected"
    :headers="headers"
    :items="desserts"
    :single-select="singleSelect"
    item-key="name"
    show-group-by
    group-by="category"
    class="elevation-1"
  >
    <template v-slot:top>
      <v-subheader>Dessert</v-subheader>
    </template>
  </v-data-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "start",
        value: "name",
        groupable: false,
      },
      { text: "Category", value: "category", align: "right" },
      { text: "Dairy", value: "dairy", align: "right" },
    ],
    desserts: [
      {
        name: "Frozen Yogurt",
        category: "Ice cream",
        dairy: "Yes",
      },
      {
        name: "Ice cream sandwich",
        category: "Ice cream",
        dairy: "Yes",
      },
      {
        name: "Eclair",
        category: "Cookie",
        dairy: "Yes",
      },
    ],
  }),
};
</script>
```

我们有`v-data-table`组件来显示组中的项目。

`group-by` prop 采用带有属性键的字符串作为分组依据。

`show-group-by`属性允许我们添加 group by 按钮，让我们根据属性进行分组。

# 按多列排序

我们可以按多列对表格进行排序。

例如，我们可以写:

```
<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    :sort-by="['calories', 'fat']"
    :sort-desc="[false, true]"
    multi-sort
    class="elevation-1"
  ></v-data-table>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    headers: [
      {
        text: "Dessert (100g serving)",
        align: "start",
        sortable: false,
        value: "name",
      },
      { text: "Calories", value: "calories" },
      { text: "Fat (g)", value: "fat" },
    ],
    desserts: [
      {
        name: "Frozen Yogurt",
        calories: 200,
        fat: 6.0,
      },
      {
        name: "Ice cream sandwich",
        calories: 200,
        fat: 9.0,
      },
      {
        name: "Eclair",
        calories: 300,
        fat: 16.0,
      },
    ],
  }),
};
</script>
```

我们添加了带有属性名数组的`sort-by`属性作为排序依据。

`sort-desc`让我们设置是否对`sort-by`中位置的列进行降序排序。

# 结论

我们可以添加可以用 Vuetify 排序和分组的表格。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**