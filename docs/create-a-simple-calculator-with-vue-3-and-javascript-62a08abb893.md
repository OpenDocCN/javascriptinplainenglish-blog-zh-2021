# 用 Vue 3 和 JavaScript 创建一个简单的计算器

> 原文：<https://javascript.plainenglish.io/create-a-simple-calculator-with-vue-3-and-javascript-62a08abb893?source=collection_archive---------11----------------------->

![](img/8c55a91d19dde48c9e7af0df30a23c4f.png)

Photo by [Amol Tyagi](https://unsplash.com/@amoltyagi2?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个简单的计算器。

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
vue create calculator
```

并选择所有默认选项来创建项目。

我们还需要 Math.js 包来计算数学表达式字符串。

要安装它，我们运行:

```
npm install mathjs
```

# 创建计算器

我们可以通过编写以下内容来创建计算器:

```
<template>
  <div>
    <div>{{ expression }}</div>
    <form @submit.prevent="calculate">
      <div>
        <button type="button" @click.stop="expression += '+'">+</button>
        <button type="button" @click.stop="expression += '-'">-</button>
        <button type="button" @click.stop="expression += '*'">*</button>
        <button type="button" @click.stop="expression += '/'">/</button>
      </div>
      <div>
        <button type="button" @click.stop="expression += '.'">.</button>
        <button type="button" @click.stop="expression += '9'">9</button>
        <button type="button" @click.stop="expression += '8'">8</button>
        <button type="button" @click.stop="expression += '7'">7</button>
      </div>
      <div>
        <button type="button" @click.stop="expression += '6'">6</button>
        <button type="button" @click.stop="expression += '5'">5</button>
        <button type="button" @click.stop="expression += '4'">4</button>
        <button type="button" @click.stop="expression += '3'">3</button>
      </div>
      <div>
        <button type="button" @click.stop="expression += '2'">2</button>
        <button type="button" @click.stop="expression += '1'">1</button>
        <button type="button" @click.stop="expression += '0'">0</button>
        <button type="submit">=</button>
      </div>
      <div>
        <button type="button" @click.stop="expression = ''">Clear</button>
      </div>
    </form>
  </div>
</template><script>
import { evaluate } from "mathjs";export default {
  name: "App",
  data() {
    return {
      expression: "",
    };
  },
  methods: {
    calculate() {
      this.expression = evaluate(this.expression);
    },
  },
};
</script><style scoped>
button {
  width: 20px;
}#clear-button {
  width: 50px;
}
</style>
```

首先，我们将`expression`字符串添加到模板的顶部。

然后，我们为计算器添加按钮。

它们用于让我们将字符添加到正在计算的表达式中。

我们通过将字符连接到`expression`反应属性来实现这一点。

除了一个按钮之外，所有按钮都被设置为`type` `button`，这样我们就不会运行`calculate`方法，直到=按钮被点击。

此外，我们有`stop`提供程序来停止`click`事件的传播。

在组件对象中，我们有`calculate`方法来计算我们输入的表达式。

我们有`@submit.prevent`指令，让我们在单击=提交表单时调用`calculate`。

`prevent`让我们阻止默认的服务器端提交机制。

我们从`mathjs`调用`evaluate`方法来评估我们输入的表达式。

然后我们将`this.expression`反应属性设置为返回的结果。

在`style`标签中，我们将按钮宽度设置为 20px，将 clear 按钮设置为 40px，这样文本就会在按钮内部。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松添加一个简单的计算器。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**