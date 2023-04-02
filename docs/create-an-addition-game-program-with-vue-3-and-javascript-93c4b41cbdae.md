# 用 Vue 3 和 JavaScript 创建一个附加游戏程序

> 原文：<https://javascript.plainenglish.io/create-an-addition-game-program-with-vue-3-and-javascript-93c4b41cbdae?source=collection_archive---------20----------------------->

![](img/b29c74bdc1e9f8430cc362deeff3f29b.png)

Photo by [Ross Sneddon](https://unsplash.com/@rosssneddon?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，它允许我们创建前端应用程序。

在本文中，我们将研究如何用 Vue 3 和 JavaScript 创建一个附加游戏程序。

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
vue create addition-game
```

并选择所有默认选项来创建项目。

# 创建加法游戏

为了创建添加应用程序，我们写道:

```
<template>
  <form @submit.prevent="submit">
    <div>
      <label>{{ num1 }} + {{ num2 }}</label>
      <input v-model.number="sum" />
    </div> <button type="submit">check</button>
  </form>
  <button type="button" @click="generateQuestion">start game</button>
  <p>score: {{ score }}</p>
</template><script>
export default {
  name: "App",
  data() {
    return {
      num1: 0,
      num2: 0,
      sum: 0,
      score: 0,
    };
  },
  computed: {
    formValid() {
      const { sum } = this;
      return +sum >= 0;
    },
  },
  methods: {
    submit() {
      if (!this.formValid) {
        return;
      }
      const { sum, num1, num2 } = this;
      if (num1 + num2 === sum) {
        this.score++;
      }
      this.generateQuestion();
    },
    generateQuestion() {
      this.num1 = Math.ceil(Math.random() * 10);
      this.num2 = Math.ceil(Math.random() * 10);
    },
  },
};
</script>
```

我们用`form`元素创建一个表单。

为了听取意见，我们听取了`submit`事件。

`prevent`修改器允许我们进行客户端提交，而不是服务器端提交。

在表格中，我们有一个输入让我们输入答案。

我们将输入的`sum`反应属性答案与`v-model`绑定。

我们使用`number`修改器将输入的值自动转换成数字。

设置为`submit`的`type`按钮通过发出`submit`事件来触发表单提交。

在组件对象中，我们使用`data`方法返回一个具有所有反应特性初始值的对象。

`formValid`计算属性让我们检查`sum`是否大于 0。

在`submit`法中，我们用`formValid`反应性来检查表格是否有效。

得到`num1`、`num2`、`sum`值，检查`num1 + num2`是否等于`sum`。

如果它们相等，那么我们将`score`增加 1。

我们可以假设它们都是数字，因为`num1`和`num2`是用`Math.random`方法生成的。

我们用`formValid`计算属性验证了`sum`是更早的一个数字。

我们调用`generateQuestion`生成`num1`和`num2`。

`Math.random`返回一个介于 0 和 1 之间的数字，所以我们必须把它乘以一个数字，这样才能得到更大范围的数字。

`Math.ceil`将数字四舍五入至最接近的整数。

当我们点击开始游戏按钮并提交答案后，就会调用`generateQuestion`。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个加法游戏程序。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)