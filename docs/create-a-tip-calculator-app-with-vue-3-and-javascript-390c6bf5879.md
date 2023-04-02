# 用 Vue 3 和 JavaScript 创建一个小费计算器应用

> 原文：<https://javascript.plainenglish.io/create-a-tip-calculator-app-with-vue-3-and-javascript-390c6bf5879?source=collection_archive---------21----------------------->

![](img/ce988ce8643fd3913edb4cb0c86edab9.png)

Photo by [Alex Iby](https://unsplash.com/@alexiby?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个小费计算器应用程序。

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

# 创建小费计算器应用程序

为了创建小费计算器应用程序，我们编写:

```
<template>
  <form @submit.prevent="calculate">
    <div>
      <label>bill amount</label>
      <input v-model.number="billAmount" />
    </div> <div>
      <label>percentage tip</label>
      <input v-model.number="percentageTip" />
    </div> <button type="submit">calculate</button>
  </form>
  <p>tip amount: {{ tipAmount.toFixed(2) }}</p>
  <p>total: {{ total.toFixed(2) }}</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      billAmount: 0,
      percentageTip: 0,
      tipAmount: 0,
      total: 0,
    };
  },
  computed: {
    formValid() {
      const { billAmount, percentageTip } = this;
      return +billAmount > 0 && +percentageTip > 0;
    },
  },
  methods: {
    calculate() {
      const { billAmount, percentageTip } = this;
      this.tipAmount = billAmount * (percentageTip / 100);
      this.total = billAmount * (1 + percentageTip / 100);
    },
  },
};
</script>
```

我们在模板中添加一个表单元素。

然后我们用`@submit`指令监听`submit`事件。

`prevent`让我们停止服务器端表单提交，转而进行客户端表单提交。

在表单中，我们有输入，让我们输入账单金额和百分比小费。

`v-model`指令让我们将输入的值绑定到一个反应属性。

`number`让我们将输入的值自动转换成数字。

然后我们展示`tipAmount`和`total`。

`toFixed`将数字转换为两位小数。

在组件对象中，我们在`data`方法中返回一个带有反应属性初始值的对象。

我们用`formValid`反应属性检查输入的值是否有效。

在其中，我们检查`billAmount`和`percentageTip`是否大于 0。

在`calculate`方法中，我们得到`billAmount`和`percentageTip`并计算`tipAmount`和`total`。

使用`number`它们会自动转换成数字，因此我们不必再次转换它们。

我们已经知道这些值是有效的，所以它们必须是数字。

现在，当我们输入值并点击“计算”时，我们会看到小费金额和总数。

# 结论

我们可以用 Vue 3 和 JavaScript 创建一个小费计算器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)