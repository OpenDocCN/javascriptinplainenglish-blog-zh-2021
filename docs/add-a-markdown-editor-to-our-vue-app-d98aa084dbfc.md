# 向我们的 Vue 应用添加降价编辑器

> 原文：<https://javascript.plainenglish.io/add-a-markdown-editor-to-our-vue-app-d98aa084dbfc?source=collection_archive---------15----------------------->

![](img/e096939cdc15b67a99dfd1d781b21607.png)

Photo by [Ben Hershey](https://unsplash.com/@benhershey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们可以很容易地在我们的 Vue 应用程序中添加一个 Markdown 编辑器。

有了它，用户可以很容易地输入格式化的文本，因为它可以很容易地转换成 HTML。

在本文中，我们将了解如何向我们的 Vue 应用程序添加一个 Markdown 编辑器。

# Mavon 编辑器

Mavon 编辑器包是一个易于使用的包，用于添加 Markdown 编辑器。

我们可以通过使用 NPM 来安装它:

```
npm install mavon-editor --save
```

然后我们可以通过写来使用它:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import mavonEditor from "mavon-editor";
import "mavon-editor/dist/css/index.css";Vue.use(mavonEditor);Vue.config.productionTip = false;
new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div class="mavonEditor">
    <no-ssr>
      <mavon-editor :toolbars="markdownOption" v-model="handbook"/>
    </no-ssr>
  </div>
</template><script>
export default {
  data() {
    return {
      markdownOption: {
        bold: true
      },
      handbook: "#### how to use mavonEditor in nuxt.js"
    };
  }
};
</script>
```

我们将`mavonEditor`插件添加到`main.js`中，这样我们就可以在我们的组件中使用它。

CSS 也是必需的，以便我们可以看到正确的样式。

它通过`v-model`指令绑定到一个州属性，这样我们就可以使用输入的文本做其他事情。

编辑器在左侧，Markdown 输出的预览在右侧。

# 选择

它带有各种各样的道具，我们可以设置这些道具来改变选项。

`value`设置初始值。

`language`设置编辑器的语言。它可以是:

*   `zh-CN`为简体中文
*   `zh-TW`对于繁体中文
*   `en`为英语
*   `fr`为法语
*   `pt-BR`为巴西葡萄牙语
*   `ru`对于俄语
*   `de`对于德语
*   `ja`对于日语

`fontSize`设置字体大小。

`scrollStyle`让我们用鼠标滚轮滚动。

`boxShadow`让我们为编辑器启用方框阴影。

`boxShadowStyle`设置方框阴影的样式。

`teransition`是一个 boolean，用来让 is 启用或禁用过渡效果。

让我们设置预览窗格的背景。

`placeholder`让我们设置占位符。

`editable`让我们设置减价编辑器是否可编辑。

`imageFilter`是对图像文件进行过滤的功能。

`imageClick`是我们点击图像时运行的功能。

`toolbars`让我们添加一个带有对象的工具栏。

例如，我们可以写:

```
<template>
  <div class="mavonEditor">
    <mavon-editor :toolbars="toolbars" v-model="handbook"/>
  </div>
</template><script>
export default {
  data() {
    return {
      toolbars: {
        bold: true,
        italic: true,
        header: true,
        underline: true,
        strikethrough: true,
        mark: true,
        superscript: true,
        subscript: true,
        quote: true,
        ol: true,
        ul: true,
        link: true,
        imagelink: true,
        code: true,
        table: true,
        fullscreen: true,
        readmodel: true,
        htmlcode: true,
        help: true,
        undo: true,
        redo: true,
        trash: true,
        save: true,
        navigation: true,
        alignleft: true,
        aligncenter: true,
        alignright: true,
        subfield: true,
        preview: true
      },
      handbook: "#### how to use mavonEditor in nuxt.js"
    };
  }
};
</script>
```

添加工具栏图标。

像任何文字处理器一样，我们可以用它做许多事情。

# 结论

Mavon editor 是一个有用的 Markdown 编辑器，我们可以将其添加到我们的 Vue 应用程序中。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**