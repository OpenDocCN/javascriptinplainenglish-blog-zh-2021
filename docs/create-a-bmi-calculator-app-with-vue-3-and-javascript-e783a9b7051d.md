# 用 Vue 3 和 JavaScript 创建一个身体质量指数计算器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-bmi-calculator-app-with-vue-3-and-javascript-e783a9b7051d?source=collection_archive---------14----------------------->

![](img/b1544d68c4537c3ee63adbe22ca13983.png)

Photo by [Philip Witt](https://unsplash.com/@benzel?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个身体质量指数计算器应用程序。

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
vue create bmi-calculator
```

并选择所有默认选项来创建项目。

# 创建身体质量指数计算器应用程序

为了创建身体质量指数计算器，我们写出:

```
<template>
  <form @submit.prevent="calculate">
    <div>
      <label>height in meters</label>
      <input v-model.number="height" />
    </div> <div>
      <label>mass in kg</label>
      <input v-model.number="mass" />
    </div> <button type="submit">calculate</button>
  </form>
  <p>bmi: {{ bmi }}</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      height: 0,
      mass: 0,
      bmi: 0,
    };
  },
  computed: {
    formValid() {
      const { height, mass } = this;
      return +height > 0 && +mass > 0;
    },
  },
  methods: {
    calculate() {
      if (!this.formValid) {
        return;
      }
      const { height, mass } = this;
      this.bmi = mass / height ** 2;
    },
  },
};
</script>
```

我们创建一个表单并添加带有`@submit`指令的提交事件监听器。

`prevent`让我们进行客户端提交，而不是服务器端提交。

然后我们将输入框添加到 div 中。

我们用`v-model`将输入值绑定到无功属性。

`number`修饰符让我们将输入的值自动转换成数字。

在组件对象中，我们有`data`方法。

它返回一个具有`height`、`mass`和`bmi`反应属性的对象。

然后我们创建`formValid` computed 属性来检查输入的`height`和`mass`是否大于 0。

我们在`calculate`方法中使用它来检查输入的值是否有效。

如果是，那么我们用`height`和`mass`计算`bmi`。

`**`运算符是取幂运算符。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个身体质量指数计算器应用程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**