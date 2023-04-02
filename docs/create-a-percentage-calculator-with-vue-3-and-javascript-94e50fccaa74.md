# 用 Vue 3 和 JavaScript 创建一个百分比计算器

> 原文：<https://javascript.plainenglish.io/create-a-percentage-calculator-with-vue-3-and-javascript-94e50fccaa74?source=collection_archive---------13----------------------->

![](img/44362944bf604c0ef65c4679f8b20685.png)

Photo by [Amol Tyagi](https://unsplash.com/@amoltyagi2?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个百分比计算器。

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
vue create percentage-calculator
```

并选择所有默认选项来创建项目。

# 创建百分比计算器

为了创建百分比计算器，我们编写:

```
<template>
  <form @submit.prevent="calculate">
    <div>
      <label>points given</label>
      <input v-model.number="pointsGiven" />
    </div> <div>
      <label>points possible</label>
      <input v-model.number="pointsPossible" />
    </div>
    <button type="submit">calculate</button>
  </form>
  <div>percentage:{{ percentage }}</div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      pointsGiven: 0,
      pointsPossible: 0,
      percentage: 0,
    };
  },
  computed: {
    formValid() {
      const { pointsGiven, pointsPossible } = this;
      return +pointsGiven >= 0 && +pointsPossible > 0;
    },
  },
  methods: {
    calculate() {
      if (!this.formValid) {
        return;
      }
      const { pointsGiven, pointsPossible } = this;
      this.percentage = (pointsGiven / pointsPossible) * 100;
    },
  },
};
</script>
```

我们有一个带有`@submit`指令的表单，让我们在点击带有`type` `submit`的按钮时监听发出的`submit`事件。

`prevent`修饰符阻止服务器端提交，让我们做客户端表单提交。

然后，我们有输入给定的点和点可能的值。

我们用`v-model`指令将输入值绑定到反应属性。

`number`修改器自动将输入值转换成数字。

然后，我们单击“计算”按钮提交表单。

在它下面，我们有一个 div 来显示计算出的`percentage`。

在组件对象中，我们用`data`方法返回一个带有反应属性及其初始值的对象。

在`formValid`计算属性中，我们检查`pointsGiven`和`pointsPossible`是否是有效值。

`pointsPossible`应该大于 0，因为我们不能被 0 整除。

然后在那下面，我们有`calculate`方法，它检查`formValid`属性是否是`true`。

如果是`true`，那么我们计算百分比。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个百分比计算器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)