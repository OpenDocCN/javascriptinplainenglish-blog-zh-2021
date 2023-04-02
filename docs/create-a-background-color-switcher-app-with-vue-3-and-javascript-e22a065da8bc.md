# 用 Vue 3 和 JavaScript 创建一个背景色转换应用程序

> 原文：<https://javascript.plainenglish.io/create-a-background-color-switcher-app-with-vue-3-and-javascript-e22a065da8bc?source=collection_archive---------10----------------------->

![](img/d2f0653a47da259f873f8184dd5b5611.png)

Photo by [Hanson Lu](https://unsplash.com/@hansonluu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，它允许我们创建前端应用程序。

在本文中，我们将研究如何用 Vue 3 和 JavaScript 创建一个背景颜色转换应用程序。

# 创建项目

我们可以使用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

纱线。

然后我们运行:

```
vue create background-switcher
```

并选择所有默认选项来创建项目。

# 创建背景颜色切换器应用程序

为了创建背景颜色切换器应用程序，我们创建了 4 个圆圈。

当我们单击一个圆时，背景颜色会切换到我们单击的圆的背景颜色。

为此，我们写道:

```
<template>
  <div id="screen" :style="{ 'background-color': backgroundColor }">
    <div
      v-for="c of colors"
      :key="c"
      :style="{
        'background-color': c,
      }"
      class="circle"
      @click="backgroundColor = c"
    ></div>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      colors: ["red", "green", "blue", "yellow"],
      backgroundColor: undefined,
    };
  },
  methods: {},
};
</script><style>
.circle {
  border-radius: 50%;
  width: 50px;
  height: 50px;
  border: 1px solid black;
  display: inline-block;
  cursor: pointer;
}#screen {
  width: 100vw;
  height: 100vh;
}
</style>
```

我们有`colors`反应属性数组，用来在模板中用`v-for`渲染成圆圈。

我们用`style`道具设置每个圆圈的背景颜色。

`key`道具设置为颜色，这是数组的唯一标识。

我们为每个圆圈添加一个点击监听器，将`backgroundColor`设置为颜色`c`。

ID 为`screen`的 div 具有`style`属性，将`background-color` CSS 属性设置为`backgroundColkor`反应性属性。

在样式标签中，我们通过将`border-radius`设置为 50%来制作带有类`circle`圆的 div。

宽度和高度设置为 50px。

`border`设为 1px 厚的黑色边框。

`display`设为`inline-block`使 div 并排显示。

`cursor`设置为`pointer`以便当我们悬停在 div 上时可以看到手。

现在，当我们点击圆圈时，我们看到颜色随着我们点击圆圈而变化。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个背景颜色转换应用程序。