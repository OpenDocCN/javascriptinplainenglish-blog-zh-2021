# 用 Vue 3 和 JavaScript 创建一个小费计算器

> 原文：<https://javascript.plainenglish.io/create-a-tip-calculator-with-vue-3-and-javascript-a6c128c1f12a?source=collection_archive---------18----------------------->

![](img/2bb5e70985dc2d6ed21205e9222a1de3.png)

Photo by [Sam Dan Truong](https://unsplash.com/@sam_truong?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个小费计算器。

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
vue create tip-calculator
```

并选择所有默认选项来创建项目。

# 创建小费计算器

为了创建小费计算器，我们编写:

```
<template>
  <div>
    <form @submit.prevent="calculate">
      <fieldset>
        <label>subtotal</label>
        <input v-model.number="tip.subtotal" />
      </fieldset> <fieldset>
        <label>number of people sharing the bill</label>
        <input v-model.number="tip.numDiners" />
      </fieldset> <fieldset>
        <label>tip percentage</label>
        <select v-model.number="tip.tipPercentage">
          <option value="0">0%</option>
          <option value="0.05">5%</option>
          <option value="0.1">10%</option>
          <option value="0.15">15%</option>
          <option value="0.2">20%</option>
        </select>
      </fieldset> <button type="submit">Calculate</button>
    </form> <div v-if="result.total">
      <p>total: {{ result.total }}</p>
      <p>total per diner: {{ result.totalPerDiner }}</p>
    </div>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      tip: {
        subtotal: 0,
        numDiners: 0,
        tipPercentage: 0,
      },
      result: {},
    };
  },
  computed: {
    subtotalValid() {
      return +this.tip.subtotal >= 0;
    },
    numDinersValid() {
      return +this.tip.numDiners > 0;
    },
    tipPercentageValid() {
      return +this.tip.tipPercentage >= 0;
    },
  },
  methods: {
    calculate() {
      const { subtotalValid, numDinersValid, tipPercentageValid } = this;
      if (!subtotalValid || !numDinersValid || !tipPercentageValid) {
        return;
      }
      const { subtotal, numDiners, tipPercentage } = this.tip;
      const total = subtotal * (1 + tipPercentage);
      this.result = { total, totalPerDiner: total / numDiners };
    },
  },
};
</script>
```

第一个输入绑定到`tip.subtotal`反应属性，该属性在提示之前有小计。

`v-model`让我们将输入值绑定到反应属性。

`number`修饰符让我们将输入的值自动转换成数字。

同样，我们在“分摊账单的人数”字段中输入分摊账单的人数。

第三个字段具有带小费百分比的`tip.tipPercentage`属性。

为了让用户提交表单，我们添加了一个按钮，将`type`属性设置为`submit`来提交表单。

我们有`@submit`指令让我们运行`calculate`方法来进行计算。

`prevent`修饰符允许我们阻止默认提交行为，这允许我们在客户端而不是服务器端提交。

表单下面的 div 显示结果。

我们只在`result.total`被计算时显示它。

在组件对象中，我们有一个`data`方法，它具有`tip`反应属性的初始值。

`result`有结果对象。

`calculate`方法让我们从表单中获取所有值并计算值。

首先，我们用计算出的属性检查值的有效性。

`subtotalValid`比较小计，确保其大于或等于 0。

我们对其他两个计算属性进行了类似的比较。

我们计算`total`和结果。

该结果显示在模板中。

# 结论

我们可以用 Vue 3 轻松创建一个小费计算器。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**