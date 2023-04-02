# 用 Vue 3 和 JavaScript 创建一个随机引用文本生成器

> 原文：<https://javascript.plainenglish.io/create-a-random-quote-text-generator-with-vue-3-and-javascript-5d95a666e874?source=collection_archive---------13----------------------->

![](img/047023bbbd4988f507abb6d5bfef435c.png)

Photo by [David Kovalenko](https://unsplash.com/@davidkovalenkoo?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个随机文本生成器。

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
vue create quote-text-generator
```

并选择所有默认选项来创建项目。

# 创建报价文本生成器

现在我们已经创建了项目，我们可以进入`App.vue`文件并编写:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="generate">generate</button>
    <p>{{ quote.quote }}</p>
    <p>{{ quote.cite }}</p>
  </div>
</template><script>
const quotes = [
  {
    quote:
      "One of my most productive days was throwing away 1,000 lines of code.",
    cite: "Ken Thompson",
  },
  {
    quote:
      "I have always wished for my computer to be as easy to use as my telephone; my wish has come true because I can no longer figure out how to use my telephone.",
    cite: "Bjarne Stroustrup",
  },
  {
    quote: "When in doubt, use brute force.",
    cite: "Ken Thompson",
  },
  {
    quote: "Talk is cheap. Show me the code.",
    cite: "Linus Torvalds",
  },
  {
    quote:
      "Always code as if the guy who ends up maintaining your code will be a violent psychopath who knows where you live.",
    cite: "Martin Golding",
  },
  {
    quote:
      "Most good programmers do programming not because they expect to get paid or get adulation by the public, but because it is fun to program.",
    cite: "Linus Torvalds",
  },
  {
    quote:
      "Most software today is very much like an Egyptian pyramid with millions of bricks piled on top of each other, with no structural integrity, but just done by brute force and thousands of slaves.",
    cite: "Alan Kay",
  },
  {
    quote:
      "Most of you are familiar with the virtues of a programmer. There are three, of course: laziness, impatience, and hubris",
    cite: "Larry Wall",
  },
  {
    quote:
      "First learn computer science and all the theory. Next develop a programming style. Then forget all that and just hack.",
    cite: "George Carrette",
  },
];export default {
  name: "App",
  data() {
    return { quote: {} };
  },
  methods: {
    generate() {
      const index = Math.floor(Math.random() * quotes.length);
      this.quote = quotes[index];
    },
  },
};
</script>
```

我们在模板中有 generate 按钮来从`quotes`数组中获取报价。

然后我们显示所选条目的`quote`和`cite`属性。

在模板中，我们有选择报价的`generate`方法。

我们通过调用`Math.floor`来向下舍入到最接近的整数。

我们通过写`Math.random() * quotes.length`得到一个介于 0 和`quotes.length`之间的随机数。

然后`quotes[index]`得到选择，我们将其分配给`this.quote`，这样我们就可以显示选择。

我们还必须通过返回一个具有`quote`属性的对象来定义`data`函数中的`this.quote`。

# 结论

我们可以用 Vue 3 创建一个很容易生成随机引用文本。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**