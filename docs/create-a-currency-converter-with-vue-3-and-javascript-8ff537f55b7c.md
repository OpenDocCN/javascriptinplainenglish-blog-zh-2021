# 用 Vue 3 和 JavaScript 创建一个货币转换器

> 原文：<https://javascript.plainenglish.io/create-a-currency-converter-with-vue-3-and-javascript-8ff537f55b7c?source=collection_archive---------9----------------------->

![](img/2bd5698120ad321a5f02e3ba8ec83b5d.png)

Photo by [Jason Leung](https://unsplash.com/@ninjason?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个货币转换器。

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
vue create currency-converter
```

并选择所有默认选项来创建项目。

# 创建货币转换器

为了创建货币转换器，我们编写:

```
<template>
  <form [@submit](http://twitter.com/submit).prevent="convert">
    <div>
      <label>value</label>
      <input v-model.number="value" />
    </div>
    <div>
      <label>from currency</label>
      <select v-model="fromCurrency">
        <option v-for="c of fromCurrencies" :key="c">{{ c }}</option>
      </select>
    </div>
    <div>
      <label>to currency</label>
      <select v-model="toCurrency">
        <option v-for="c of toCurrencies" :key="c">{{ c }}</option>
      </select>
    </div>
    <button type="submit">convert</button>
  </form>
  <div>
    {{ value }} {{ fromCurrency }} is {{ result.toFixed(2) }} {{ toCurrency }}
  </div>
</template><script>
const currencies = ["EUR", "USD", "CAD"];
export default {
  name: "App",
  data() {
    return {
      value: 0,
      fromCurrency: "",
      toCurrency: "",
      currencies,
      result: 0,
    };
  },
  computed: {
    fromCurrencies() {
      const { toCurrency, currencies } = this;
      return currencies.filter((c) => c !== toCurrency);
    },
    toCurrencies() {
      const { fromCurrency, currencies } = this;
      return currencies.filter((c) => c !== fromCurrency);
    },
    formValid() {
      const { value, fromCurrency, toCurrency } = this;
      return +value >= 0 && fromCurrency && toCurrency;
    },
  },
  methods: {
    async convert() {
      const { fromCurrency, toCurrency, value, formValid } = this;
      if (!formValid) {
        return;
      }
      const res = await fetch(
        `https://api.exchangeratesapi.io/latest?base=${fromCurrency}`
      );
      const { rates } = await res.json();
      this.result = value * rates[toCurrency];
    },
  },
};
</script>
```

我们有一个表单，可以输入要转换的货币值。

从货币下拉菜单中，我们可以选择要转换的货币。

“兑换货币”下拉菜单让我们选择要兑换的货币。

我们绑定来自输入的所有值，并使用`v-model`选择下拉列表以反映属性。

`@submit`指令监听当我们单击 convert 时发出的提交事件。

`prevent`修饰符让我们做客户端表单提交。

在脚本标签中，我们有一个包含货币列表的`currencies`数组。

`data`方法返回我们使用的反应属性。

`fromCurrencies` computed 属性有我们可以转换的货币列表。

我们过滤掉在“兑换货币”下拉列表中选择的货币。

类似地,`toCurrencies`下拉列表也用于“兑换货币”下拉列表，并过滤掉“兑换货币”下拉列表中的选项。

`formValid`计算属性检查`value`是否大于或等于 0。

`convert`方法从自由外汇汇率 API 获取汇率。

`base`查询参数设置要转换的货币。

我们用`fetch`得到比率，并用它来计算结果。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个货币转换器。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)