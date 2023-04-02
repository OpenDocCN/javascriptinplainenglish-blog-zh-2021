# 用 Vue 3 和 JavaScript 创建一个贷款计算器应用

> 原文：<https://javascript.plainenglish.io/create-a-loan-calculator-app-with-vue-3-and-javascript-8e4b9a19d919?source=collection_archive---------9----------------------->

![](img/88c17a5be55609c5c2feb50374a711ad.png)

Photo by [Alexander Schimmeck](https://unsplash.com/@alschim?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个贷款计算器应用程序。

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
vue create loan-calculator
```

并选择所有默认选项来创建项目。

# 创建贷款计算器应用程序

我们可以通过编写以下内容来创建贷款计算器应用程序:

```
<template>
  <form @submit.prevent="calculate">
    <div>
      <label>loan amount</label>
      <input v-model.number="loanAmount" />
    </div>
    <div>
      <label>interest rate</label>
      <input v-model.number="interestRate" />
    </div>
    <div>
      <label>number of months to pay off loan</label>
      <input v-model.number="numMonths" />
    </div>
    <button type="submit">calculate monthly payment</button>
  </form>
  <p>monthly payment: {{ monthlyPayment.toFixed(2) }}</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      loanAmount: 0,
      interestRate: 0,
      numMonths: 0,
      monthlyPayment: 0,
    };
  },
  computed: {
    formValid() {
      const { loanAmount, interestRate, numMonths } = this;
      return (
        +loanAmount >= 0 &&
        0 <= +interestRate &&
        +interestRate <= 100 &&
        +numMonths > 0
      );
    },
  },
  methods: {
    calculate() {
      if (!this.formValid) {
        return;
      }
      const { loanAmount, interestRate, numMonths } = this;
      this.monthlyPayment = (loanAmount * (1 + interestRate / 100)) / numMonths;
    },
  },
};
</script>
```

我们创建一个包含贷款金额、利率和还清贷款的月数字段的表单。

它们都绑定到一个带有`v-model`指令的 reactive。

并且它们都有`number`修饰符来自动将输入的值转换成数字。

我们还有提交按钮，让我们触发`submit`事件来运行`calculate`方法。

`prevent`让我们阻止默认的服务器端提交行为。

`data`方法返回一个带有反应属性及其初始值的对象。

我们还有`formValid` computed 属性来返回表单有效的条件。

`loanAmount`必须大于等于 0。

`interestRate`必须介于 0 和 100 之间。

并且`numMonths`必须大于 0。

我们使用`+`符号来轻松地将它们转换成数字。

并且`calculate`方法检查`formValid` computed 属性以查看表单是否有效。

然后用该方法的最后一行计算月还款额。

在模板中，我们显示四舍五入到两位小数的每月付款。

`toFixed`方法执行舍入并返回字符串形式的值。

# 结论

我们可以用 Vue 3 和 JavaScript 创建一个贷款计算器。

*获取更多内容请点击*[***plain English . io***](https://plainenglish.io/)