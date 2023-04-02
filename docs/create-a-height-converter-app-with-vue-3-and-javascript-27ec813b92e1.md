# 用 Vue 3 和 JavaScript 创建一个高度转换器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-height-converter-app-with-vue-3-and-javascript-27ec813b92e1?source=collection_archive---------17----------------------->

![](img/38e40fdccb8b63ee3d0c79d496b09378.png)

Photo by [Paolo Nicolello](https://unsplash.com/@paul_nic?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，它允许我们创建前端应用程序。

在本文中，我们将了解如何使用 Vue 3 和 JavaScript 创建一个高度转换器应用程序。

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
vue create height-converter
```

并选择所有默认选项来创建项目。

# 创建高度转换应用程序

为了创建高度转换器应用程序，我们写道:

```
<template>
  <form @submit.prevent="submit">
    <div>
      <label>feet</label>
      <input v-model.number="feet" />
    </div>
    <div>
      <label>inches</label>
      <input v-model.number="inches" />
    </div>
    <button type="submit">calculate</button>
  </form>
  <p>{{ centimeters }} cm</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      feet: 0,
      inches: 0,
      centimeters: 0,
    };
  },
  computed: {
    formValid() {
      const { feet, inches } = this;
      return +feet >= 0 && +inches >= 0;
    },
  },
  methods: {
    submit() {
      if (!this.formValid) {
        return;
      }
      const { feet, inches } = this;
      this.centimeters = (feet + inches / 12) * 12 * 2.54;
    },
  },
};
</script>
```

为了创建高度转换器，我们创建了一个有 2 个输入的表单。

一个输入用于输入英尺数。

另一个用于输入英寸数。

我们通过`v-model`将它们与`feet`和`inches`反应性结合在一起。

`number`将输入的值转换为数字。

然后在组件对象中，我们使用`data`方法返回反应属性及其初始值。

我们用`@submit`指令倾听提交事件。

`prevent`允许我们进行客户端表单提交，而不是服务器端提交。

`formValid`计算属性检查`feet`和`inches`值是否有效。

在`submit`方法中，我们用`formValid`检查输入的值是否有效。

然后我们从`feet`和`inches`计算厘米。

我们将括号中的所有内容转换为英尺。

然后我们乘以 12 得到英寸。

然后我们乘以 2.54 得到厘米。

然后我们在模板中显示`centimeters`值。

# 结论

我们可以用 Vue 3 和 JavaScript 创建一个高度转换器。

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似的内容！**

*更内容见于* [***中***](https://plainenglish.io/)