# 使用复合 API 创建 Vue 3 应用程序—观看和观看效果

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-watch-and-watch-effect-7c2ce455c6a2?source=collection_archive---------20----------------------->

![](img/0edb4341386796045b3fb4abcdd4bbb7.png)

Photo by [Fabian Heimann](https://unsplash.com/@fabianheimann?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 自带内置的 Composition API。

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# `watch`

Vue 3 组合 API 中的`watch`函数与 Vue 2 的`this.$watch`方法或`watch`选项相同。

因此，我们可以用它来观察反应性质的变化。

例如，我们可以写:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="increment">increment</button>
    {{ state.count }}
  </div>
</template><script>
import { reactive, watch } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({ count: 0 }); const increment = () => {
      state.count++;
    };
    watch(
      () => state.count,
      (count, prevCount) => {
        console.log(count, prevCount);
      }
    ); return {
      state,
      increment,
    };
  },
};
</script>
```

我们在第二个参数中看到了一个 getter 函数。

我们在函数的第一个和第二个参数中得到当前和以前的值，作为第二个参数传递给`watch`。

现在，当我们单击“increment”按钮时，我们会看到`state.count`增加。

如果我们有一个原始值的反应属性，我们可以将它直接传递给`watch`的第一个参数:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ count }}
  </div>
</template><script>
import { ref, watch } from "vue";
export default {
  name: "App",
  setup() {
    const count = ref(0);
    const increment = () => {
      count.value++;
    };
    watch(count, (count, prevCount) => {
      console.log(count, prevCount);
    }); return {
      count,
      increment,
    };
  },
};
</script>
```

当我们点击增量按钮时，我们得到与`count`和`prevCount`相同的值。

# 观看多个来源

我们还可以观看多个参考文献。

例如，我们可以写:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ foo }}
    {{ bar }}
  </div>
</template><script>
import { ref, watch } from "vue";
export default {
  name: "App",
  setup() {
    const foo = ref(0);
    const bar = ref(0);
    const increment = () => {
      foo.value++;
      bar.value++;
    };
    watch([foo, bar], ([foo, bar], [prevFoo, prevBar]) => {
      console.log([foo, bar], [prevFoo, prevBar]);
    }); return {
      foo,
      bar,
      increment,
    };
  },
};
</script>
```

我们将`foo`和`bar`引用传入数组。

然后，我们从第二个参数的函数参数数组中获取当前和以前的值。

我们还可以将`onInvalidate`函数传递给第三个参数。

而其他行为也分享给`watchEffect`。

# 结论

我们可以用 Vue 3 的组合 API 观察器来观察反应属性。

*更多内容看* [***说白了. io***](https://plainenglish.io/)