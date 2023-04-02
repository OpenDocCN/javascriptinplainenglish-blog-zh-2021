# 使用交叉点观察器 API 为 Vue.js 3 应用程序添加无限滚动

> 原文：<https://javascript.plainenglish.io/add-infinite-scrolling-to-a-vue-js-3-app-with-the-intersection-observer-api-706c169947c3?source=collection_archive---------24----------------------->

![](img/1c2f892bbfb2f6d16ef6f68474572a3e.png)

Photo by [Galen Crout](https://unsplash.com/@galen_crout?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无限滚动是我们必须经常添加到 Vue 3 应用程序中的东西。

在本文中，我们将了解如何使用交叉点观察器 API 为 Vue 3 应用程序添加无限滚动。

# 使用交叉点观察器 API 添加无限滚动

交叉点 API 让我们可以在 Vue 3 应用中轻松添加无限滚动。

为此，我们为最后一个元素分配一个 ref，并观察该元素何时显示在屏幕上。

然后当数组改变时，我们将 ref 重新分配给最后添加的元素。

例如，我们可以写:

```
<template>
  <div
    v-for="(a, i) of arr"
    :key="a"
    :ref="i === arr.length - 1 ? 'last' : undefined"
  >
    {{ a }}
  </div>
</template><script>
export default {
  name: "App",
  data() {
    return {
      page: 1,
      arr: Array(30)
        .fill()
        .map((_, i) => i),
      observer: undefined,
    };
  },
  methods: {
    async addObserver() {
      await this.$nextTick();
      const options = {
        root: document,
        rootMargin: "20px",
        threshold: 1,
      }; const callback = (entries) => {
        if (entries[0].isIntersecting) {
          this.arr = [
            ...this.arr,
            ...Array(30)
              .fill()
              .map((_, i) => i + 30 * (this.page - 1)),
          ];
          this.page++;
        }
      };
      this.observer = new IntersectionObserver(callback, options);
      this.observer.observe(this.$refs.last);
    },
  },
  mounted() {
    this.addObserver();
  },
  watch: {
    arr: {
      deep: true,
      handler() {
        this.addObserver();
      },
    },
  },
};
</script>
```

我们有一系列从组件模板中的`arr`数组呈现的 div。

通过检查项目的索引是否与`arr.length — 1`相同来设置`ref`道具。

如果是，那么它是最后一项，所以我们给它分配一个 ref。

否则，我们不会给它分配一个引用。

`data`方法返回`page`数字和`arr`数组以及要渲染的数据。

在`methods`对象中，我们有`addObserver`方法来添加交叉点观察器，并使用它来观察我们指定了 ref 的元素何时出现在屏幕上。

为此，我们调用`$nextTick`来确保元素被渲染。

然后，我们设置检测交叉点的选项。

`root`是包含我们所关注的项目的元素。

`rootMargin`是确定项目何时被视为在屏幕上的边距。

`threshold`是要显示的元素的阈值。它是元素出现在屏幕上的部分。它是一个介于 0 和 1 之间的数字。

接下来，我们使用了`callback`函数来检查`isIntersecting`属性，以查看最后一个元素是否出现。

如果有，那么我们通过在数组中放入更多的条目来更新数组`arr`。

我们还更新了`page`值。

接下来，我们用`callback`和`options`创建`IntersectionObserver`实例。

然后我们在它上面调用`observe`,这个元素被赋予了 ref，看着它出现在屏幕上。

我们在组件已安装并且`arr`数组发生变化时调用该方法。

在组件被渲染之后,`mounted`钩子运行，因此我们可以获得分配了 ref 的元素，并观察它出现在屏幕上。

现在，当我们向下滚动时，我们应该会看到更多的项目出现。

# 结论

我们可以轻松地使用交叉点观察器 API 将无限滚动轻松地添加到我们的 Vue 3 应用程序中。

*更多内容尽在*[***plain English . io***](http://plainenglish.io)