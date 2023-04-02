# Vuetify —板材、小吃店和骨架装载机

> 原文：<https://javascript.plainenglish.io/vuetify-sheets-snackbars-and-skeleton-loaders-4ce29db452e5?source=collection_archive---------4----------------------->

![](img/06014a92b45f5dad2e107a2929dcb970.png)

Photo by [Ricardo Henrique Vergilio](https://unsplash.com/@rickvergilius?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuetify 是一个流行的 Vue 应用程序 UI 框架。

在本文中，我们将了解如何使用 Vuetify 框架。

# 工作表

我们可以使用`v-sheets`组件在我们的应用程序中添加内容容器。

例如，我们可以写:

```
<template>
  <v-container>
    <v-row justify="space-around">
      <v-col v-for="elevation in elevations" :key="elevation" cols="12" md="4">
        <v-sheet class="pa-12" color="grey lighten-3">
          <v-sheet :elevation="elevation" class="mx-auto" height="100" width="100"></v-sheet>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    elevations: [12, 24],
  }),
};
</script>
```

给我们的床单添加不同层次的阴影。

# 瓷砖

`tile`属性使工作表成为矩形:

```
<template>
  <v-container>
    <v-row justify="space-around">
      <v-col>
        <v-sheet class="pa-12" color="grey lighten-3">
          <v-sheet tile class="mx-auto" height="100" width="100"></v-sheet>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({}),
};
</script>
```

# 颜色和尺寸

我们可以改变床单的颜色和大小。

例如，我们可以写:

```
<template>
  <v-container>
    <v-row class="flex-child">
      <v-col class="d-flex" cols="12">
        <v-sheet class="d-flex" color="grey lighten-3" height="100">
          <sheet-footer>lorem ipsum</sheet-footer>
        </v-sheet>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({}),
};
</script>
```

添加一张背景为灰色、高度为 100 像素的工作表。

# 骨架装载机

`v-skeleton-loader`组件让我们提供正在加载的指示。

例如，我们可以这样使用它:

```
<template>
  <v-container class="grey">
    <v-row justify="center">
      <v-col class="mb-12" cols="12" md="4">
        <v-skeleton-loader
          :loading="loading"
          :transition="transition"
          height="94"
          type="list-item-two-line"
        >
          <v-card>
            <v-card-title>Title</v-card-title>
            <v-card-text>Card Text</v-card-text>
          </v-card>
        </v-skeleton-loader>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    loading: true,
    transition: "scale-transition",
  }),
};
</script>
```

我们有`v-skeleton-loader`组件来添加框架加载器。

`loading`道具可以设置为加载状态。

而`transition`是我们想要显示的过渡的名称。

# 小吃店

snackbar 让我们向用户显示一条消息。

小吃店可以定位和延迟可以消除。

为了添加它，我们添加了`v-snackbar`组件:

```
<template>
  <div class="text-center">
    <v-btn dark color="red darken-2" @click="snackbar = true">Open Snackbar</v-btn> <v-snackbar v-model="snackbar" :multi-line="multiLine">
      {{ text }}
      <template v-slot:action="{ attrs }">
        <v-btn color="red" text v-bind="attrs" @click="snackbar = false">Close</v-btn>
      </template>
    </v-snackbar>
  </div>
</template>
<script>
export default {
  name: "HelloWorld",
  data: () => ({
    multiLine: true,
    snackbar: false,
    text:
      "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi a neque arcu. Phasellus ac tincidunt elit. I",
  }),
};
</script>
```

我们有由`v-btn`触发的`v-snackbar`组件。

`snackbar`状态控制 snackbar 的打开状态。

在`v-snackbar`中，我们将`attrs`传递给`v-btn`的道具，这样它就可以用作 snackbar 按钮。

当我们点击它时，我们将`snackbar`设置为`false`，这样它就可以被关闭。

`multi-line`道具让它多行显示文本。

# 结论

我们可以使用工作表作为内容的容器。

零食条让我们显示信息。

骨架加载器对于显示加载指示器很有用。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**