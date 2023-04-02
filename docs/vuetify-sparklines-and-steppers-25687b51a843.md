# 虚拟化-迷你图和步进器

> 原文：<https://javascript.plainenglish.io/vuetify-sparklines-and-steppers-25687b51a843?source=collection_archive---------13----------------------->

![](img/1ce6138a43f3ad686b211600246415c6.png)

Photo by [Jake Hills](https://unsplash.com/@jakehills?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuetify 是一个流行的 Vue 应用程序 UI 框架。

在本文中，我们将了解如何使用 Vuetify 框架。

# 迷你图和仪表板卡

我们可以把迷你图放在卡片里。

例如，我们可以写:

```
<template>
  <v-card class="mt-4 mx-auto" max-width="400">
    <v-sheet
      class="v-sheet--offset mx-auto"
      color="cyan"
      elevation="12"
      max-width="calc(100% - 32px)"
    >
      <v-sparkline :labels="labels" :value="value" color="white" line-width="2" padding="16"></v-sparkline>
    </v-sheet> <v-card-text class="pt-0">
      <div class="title font-weight-light mb-2">User Registrations</div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    labels: ["12am", "3am", "6am", "9am", "12pm", "3pm", "6pm", "9pm"],
    value: [0, 2, 5, 9, 5, 10, 3, 5],
  }),
};
</script>
```

我们添加了`v-sheet`作为`v-sparkline`的容器。

`v-card-text`位于迷你图下方。

`v-sheet`的`color`显示为卡片的背景色。

# 自定义标签

可以通过插入`label`插槽来定制标签。

例如，我们可以写:

```
<template>
  <v-card class="mx-auto text-center" color="green" dark max-width="600">
    <v-card-text>
      <v-sheet color="rgba(0, 0, 0, .12)">
        <v-sparkline
          :value="value"
          color="rgba(255, 255, 255, .7)"
          height="100"
          padding="24"
          stroke-linecap="round"
          smooth
        >
          <template v-slot:label="item">${{ item.value }}</template>
        </v-sparkline>
      </v-sheet>
    </v-card-text> <v-card-text>
      <div class="display-1 font-weight-thin">Sales Last 24h</div>
    </v-card-text>
  </v-card>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    value: [423, 450, 480, 510, 590, 610, 760],
  }),
};
</script>
```

我们用自己的内容填充`label`槽。

`item`变量拥有`value`数组的入口。

# 踏步机

我们可以用`v-stepper`组件通过编号的步骤来显示进度。

例如，我们可以写:

```
<template>
  <v-stepper>
    <v-stepper-header>
      <v-stepper-step complete editable step="1">Select keywords</v-stepper-step> <v-divider></v-divider> <v-stepper-step complete step="2">Create ad group</v-stepper-step> <v-divider></v-divider> <v-stepper-step step="3" editable>Create ad</v-stepper-step>
    </v-stepper-header>
  </v-stepper>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({}),
};
</script>
```

我们添加`v-stepper`组件来为我们的步进组件添加步骤。

`v-stepper-step`有步骤。

用线将台阶隔开。

# 不可编辑的步骤

我们可以用`complete`道具使步骤不可编辑。

例如，我们可以写:

```
<template>
  <v-stepper value="2">
    <v-stepper-header>
      <v-stepper-step step="1" complete>Select keywords</v-stepper-step> <v-divider></v-divider> <v-stepper-step step="2">Create an ad group</v-stepper-step> <v-divider></v-divider> <v-stepper-step step="3">Create an ad</v-stepper-step>
    </v-stepper-header>
  </v-stepper>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({}),
};
</script>
```

# 可选步骤

我们可以添加文本来表示某个步骤是可选的:

```
<template>
  <v-stepper value="2">
    <v-stepper-header>
      <v-stepper-step step="1" complete>Select keywords</v-stepper-step> <v-divider></v-divider> <v-stepper-step step="2">
        Create an ad group
        <small>Optional</small>
      </v-stepper-step> <v-divider></v-divider> <v-stepper-step step="3">Create an ad</v-stepper-step>
    </v-stepper-header>
  </v-stepper>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({}),
};
</script>
```

`small`元素将被放置在主文本的下方。

# 结论

我们可以在卡片上添加迷你图，在步进器上显示步数。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**