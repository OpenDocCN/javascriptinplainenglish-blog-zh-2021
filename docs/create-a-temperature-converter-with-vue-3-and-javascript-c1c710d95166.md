# 用 Vue 3 和 JavaScript 创建一个温度转换器

> 原文：<https://javascript.plainenglish.io/create-a-temperature-converter-with-vue-3-and-javascript-c1c710d95166?source=collection_archive---------15----------------------->

![](img/1388c743e4e033c9043c9892d49af146.png)

Photo by [Karim MANJRA](https://unsplash.com/@karim_manjra?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个温度转换器。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create temperature-converter
```

并选择所有默认选项来创建项目。

# 创建温度转换器

为了创建温度转换器，我们编写:

```
<template>
  <form @submit.prevent="convert">
    <div>
      <label>temperature in celsius</label>
      <input v-model.number="celsius" />
    </div>
    <button type="submit">convert</button>
  </form>
  <div>{{ celsius }}c is {{ fahrenheit }}f</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      celsius: 0,
      fahrenheit: 0,
    };
  },
  computed: {
    formValid() {
      return !isNaN(+this.celsius);
    },
  },
  methods: {
    convert() {
      if (!this.formValid) {
        return;
      }
      this.fahrenheit = this.celsius * (9 / 5) + 32;
    },
  },
};
</script>
```

我们创建了一个输入以摄氏度为单位的表单。

我们将输入值绑定到与`v-model`反应的`celsius`。

`number`修饰符让我们自动将其转换成一个数字。

在`form`中，我们添加了`@submit`指令来监听类型为`submit`的按钮上的点击。

`prevent`修饰符阻止服务器端提交，让我们做客户端提交。

然后在组件对象中，我们有返回`celsius`和`fahrenheit`反应属性的`data`方法。

我们有`formValid`计算属性，它检查`celsius`反应属性是否是一个数字。

然后在`convert`方法中，。我们检查`formValid` computed 属性以查看表单是否有效。

如果是，我们从`celsius`值计算`fahrenheit`值。

最后，在模板中，我们在 div 中显示转换的结果。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个温度。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)