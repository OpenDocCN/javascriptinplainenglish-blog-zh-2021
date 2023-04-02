# 使用 Vue 加载覆盖组件将加载微调器添加到 Vue 应用程序

> 原文：<https://javascript.plainenglish.io/add-a-loading-spinner-to-a-vue-app-with-the-vue-loading-overlay-component-f9d64d8aa897?source=collection_archive---------14----------------------->

![](img/3bd88e0da425711719c4e68487107ccf.png)

Photo by [Riku Lu](https://unsplash.com/@riku?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们想在我们的 Vue 应用程序中显示一个加载微调器来指示应用程序正在加载。

在本文中，我们将了解如何使用 Vue 加载覆盖组件向 Vue 应用程序添加加载微调器。

# 装置

要安装这个包，我们可以运行:

```
npm i vue-loading-overlay
```

和 NPM 一起。

# 使用

一旦我们安装了它，我们就可以通过编写以下内容来使用它:

```
<template>
  <div>
    <loading
      :active.sync="isLoading"
      :can-cancel="true"
      :on-cancel="onCancel"
      :is-full-page="fullPage"
    >
    </loading>
    <button @click.prevent="doAjax">fetch Data</button>
  </div>
</template>

<script>
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";export default {
  data() {
    return {
      isLoading: false,
      fullPage: true,
    };
  },
  components: {
    Loading,
  },
  methods: {
    doAjax() {
      this.isLoading = true;
      setTimeout(() => {
        this.isLoading = false;
      }, 5000);
    },
    onCancel() {
      console.log("User cancelled the loader.");
    },
  },
};
</script>
```

我们导入`Loading`组件并在`components`属性中注册它。

此外，我们导入 CSS 文件来添加微调器样式。

然后我们将`loading`组件添加到模板中。

`active`设置为微调器显示时的状态。

`can-cancel`设置为`true`表示我们可以手动关闭旋转器。

`on-cancel`是旋转器关闭时运行的功能。

`is-full-page`是设定微调器将获取整页的条件。

在`methods`属性对象中，我们添加了`doAjax`方法来设置`this.isLoading`以控制微调器何时显示。

`onCancel`是我们关闭微调器时运行的方法。

我们也可以把这个库作为插件来使用。

例如，我们可以写:

```
<template>
  <form @submit.prevent="submit" style="height: 500px" ref="formContainer">
    <button type="submit">Login</button>
  </form>
</template>

<script>
import Vue from "vue";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";
Vue.use(Loading);export default {
  data() {
    return {
      fullPage: false,
    };
  },
  methods: {
    submit() {
      const loader = this.$loading.show({
        container: this.$refs.formContainer,
        canCancel: true,
        onCancel: this.onCancel,
      });
      setTimeout(() => {
        loader.hide();
      }, 5000);
    },
    onCancel() {
      console.log("User cancelled the loader.");
    },
  },
};
</script>
```

我们有一个分配了 ref 的表单。

form 元素将被用作微调器的容器。

然后我们以同样的方式导入模块和 CSS。

接下来，我们调用`Vue.use`来注册插件。

然后我们有`submit`方法调用`this.$loading.show`来显示加载微调器，

`container`被设置为存储在`this.$refs.formContainer`中的表单元素。

`canCancel`设置是否可以关闭旋转器。

`onCancel`设置为我们关闭微调器时想要运行的方法。

因此，当我们单击“登录”时，我们会看到微调器显示 5 秒钟，或者直到我们单击它。

# 结论

我们可以添加一个加载微调到我们的 Vue 应用程序与 Vue 加载覆盖。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)