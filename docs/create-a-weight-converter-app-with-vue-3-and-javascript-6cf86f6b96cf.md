# 用 Vue 3 和 JavaScript 创建一个重量转换器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-weight-converter-app-with-vue-3-and-javascript-6cf86f6b96cf?source=collection_archive---------14----------------------->

![](img/ce4e02d64083ec409e4866e990f8c184.png)

Photo by [Victor Freitas](https://unsplash.com/@victorfreitas?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个体重转换器应用程序。

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
vue create weight-converter
```

并选择所有默认选项来创建项目。

# 创建重量转换器应用程序

为了创建重量转换器应用程序，我们编写:

```
<template>
  <form>
    <div>
      <label>weight in pounds</label>
      <input v-model.number="weightInLb" />
    </div>
  </form>
  <p>{{ weightInKg }} kg</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      weightInLb: 0,
    };
  },
  computed: {
    weightInKg() {
      const { weightInLb } = this;
      return +weightInLb * 0.453592;
    },
  },
};
</script>
```

我们添加了带有输入的表单，让用户以磅/为单位输入体重

我们用`v-model`将输入值绑定到`weightInLb`反应属性。

`number`修饰符让我们阻止服务器端提交。

在`data`方法中，我们返回一个具有`weightInLb`反应属性的对象。

然后，我们创建`weightInKg` computed 属性，将磅重量转换为千克重量。

然后我们在模板中显示`weightInKg`。

现在，当我们输入以磅为单位的重量时，我们会自动看到以千克为单位的重量。

`weightInKg`是一个反应性属性，所以`weightInKg`发生变化时会自动更新。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个体重计算器应用程序。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)