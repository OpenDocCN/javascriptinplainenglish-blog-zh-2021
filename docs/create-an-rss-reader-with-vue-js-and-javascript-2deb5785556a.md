# 用 Vue.js 和 JavaScript 创建一个 RSS 阅读器

> 原文：<https://javascript.plainenglish.io/create-an-rss-reader-with-vue-js-and-javascript-2deb5785556a?source=collection_archive---------6----------------------->

![](img/5f2f7cc79f6e828c4a8e6cf202b80e8e.png)

Photo by [La coccinelle](https://unsplash.com/@wisi?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 是一个易于使用的 JavaScript 框架，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue.js 和 JavaScript 创建一个 RSS 阅读器应用程序。

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
vue create rss-reader
```

并选择所有默认选项来创建项目。

# 创建 RSS 阅读器

为了创建 RSS 阅读器，我们编写:

```
<template>
  <div id="app">
    <form @submit.prevent="getRss">
      <div>
        <label> rss url</label>
        <br />
        <input v-model="rssUrl" />
      </div>
      <input type="submit" />
    </form>
    <div v-for="item of items" :key="item.title">
      <h1>{{ item.title }}</h1>
      <p>{{ item.author }}</p>
      <a :href="item.link">{{ item.link }}</a>
    </div>
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      rssUrl: "",
      items: [],
    };
  },
  methods: {
    async getRss() {
      const urlRegex = /(http|ftp|https):\/\/[\w-]+(\.[\w-]+)+([\w.,@?^=%&amp;:\/~+#-]*[\w@?^=%&amp;\/~+#-])?/;
      if (!urlRegex.test(this.rssUrl)) {
        return;
      }
      const res = await fetch(
        `https://api.allorigins.win/get?url=${this.rssUrl}`
      );
      const { contents } = await res.json();
      const feed = new window.DOMParser().parseFromString(contents, "text/xml");
      const items = feed.querySelectorAll("item");
      this.items = [...items].map((el) => ({
        link: el.querySelector("link").innerHTML,
        title: el.querySelector("title").innerHTML,
        author: el.querySelector("author").innerHTML,
      }));
    },
  },
};
</script>
```

我们有一个带有表单字段的表单，可以让我们输入 RSS 提要的 URL。

我们将输入值绑定到`rssUrl`反应属性。

在表单元素中，我们监听`submit`事件，当我们点击类型为`submit`的输入按钮时，该事件被触发。

`prevent`修饰符让我们做客户端提交，而不是服务器端。

在该表单下面，我们使用`v-for`指令来呈现 RSS 数据，这些数据存储在`items` reactive 属性中。

在脚本中，我们有`getRss`方法。

该方法首先检查`rssUrl`是否有效。

如果是，那么我们调用`fetch`请求从 RSS 提要中获取数据。

我们使用 [allOrigins](https://allorigins.win/) API 向给定的提要发出跨域请求。

我们需要这样做，因为大多数提要都不允许从浏览器进行跨域通信。

该请求具有带有 XML RSS 提要内容的`contents`属性。

然后我们使用来自`DOMParser`构造函数的`parseFromString`方法来解析 XML 字符串。

我们将 XML 字符串作为第一个参数传入。

第二个参数包含我们正在解析的内容类型。

它返回 XML 树 DOM 对象。

这意味着我们可以使用像`querySelectorAll`这样的方法来选择节点。

然后我们可以用`querySelectAll`选择`item`节点。

然后我们使用 spread 操作符将节点列表中的项目扩展到一个数组中。

接下来，我们调用`map`来返回包含我们用`querySelector`选择的节点内容的对象。

现在在模板中，表单下面的 div 应该呈现 RSS 提要内容。

# 结论

我们可以使用 Vue.js 和 JavaScript 轻松创建 RSS 提要。