# 用 Vue 3 和 JavaScript 创建一个搜索过滤器应用程序

> 原文：<https://javascript.plainenglish.io/create-a-search-filter-app-with-vue-3-and-javascript-72fce6a96124?source=collection_archive---------6----------------------->

![](img/55ab11917aa4b8c8507b3290acc25483.png)

Photo by [Richard T](https://unsplash.com/@newhighmediagroup?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个搜索过滤器。

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
vue create search-filter
```

并选择所有默认选项来创建项目。

# 创建搜索过滤器

为了创建图像滑块，我们编写:

```
<template>
  <div>
    <input v-model="keyword" placeholder="search" />
    <div v-for="(f, index) of filterImages" :key="index">
      <img :src="f.url" />
      <p>{{ f.description }}</p>
    </div>
  </div>
</template><script>
const images = [
  {
    url: "https://images.dog.ceo/breeds/affenpinscher/n02110627_4597.jpg",
    description: "affenpinscher",
  },
  {
    url: "https://images.dog.ceo/breeds/akita/Akita_Inu_dog.jpg",
    description: "akita",
  },
  {
    url: "https://images.dog.ceo/breeds/retriever-golden/n02099601_7771.jpg",
    description: "golden retriever",
  },
];
export default {
  name: "App",
  data() {
    return { keyword: "", images };
  },
  computed: {
    filterImages() {
      const { images, keyword } = this;
      return images.filter(({ description }) => description.includes(keyword));
    },
  },
};
</script><style scoped>
img {
  width: 200px;
  height: 200px;
}
</style>
```

在模板中，我们有输入元素。

我们用`v-model`将它的输入值绑定到`keyword`反应属性。

为了清楚起见，我们添加了一个占位符。

然后我们循环遍历`filterImages`数组，渲染来自`url`和`description`的图像。

我们必须将`key`设置为一个唯一的键，以便 Vue 3 可以正确地跟踪由`v-for`渲染的 div。

在`script`标签中，我们有一个包含我们想要过滤的数据的`images`数组。

在`data`方法中，我们返回了`keyword`和`images`属性，使它们具有反应性。

`images`来自`images`数组。

然后，为了在我们输入时添加过滤器，我们用匹配我们输入的关键字的图像创建了`filterImages`计算属性。

我们通过调用`this.images`上的`filter`方法并检查`description`来查看`this.description`反应属性是`images`数组中对象的`description`的子字符串。

然后在`style`标签中，我们将所有的 img 元素显示为 200 像素乘 200 像素，以使它们适合页面。

当我们在输入框中输入内容时，我们应该看到匹配的条目显示出来。

# 结论

我们可以用 Vue 3 轻松创建一个搜索过滤器。

喜欢这篇文章吗？如果有，请在[**plain English . io**](https://plainenglish.io/)获取更多类似内容