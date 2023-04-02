# 使用组合 API 创建 Vue 3 应用——生命周期挂钩和引用

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-lifecycle-hooks-and-refs-2a41eee88f6a?source=collection_archive---------18----------------------->

![](img/b2526f27a0c43efaa173a1fad00c5cfb.png)

Photo by [Derek Thomson](https://unsplash.com/@derekthomson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# 生命周期挂钩

Vue 3 的 composition API 也提供了生命周期挂钩。

我们把它们都放在`setup`方法中。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { onMounted, onUnmounted, onUpdated } from "vue";
export default {
  name: "App",
  setup() {
    onMounted(() => {
      console.log("mounted!");
    });
    onUpdated(() => {
      console.log("updated!");
    });
    onUnmounted(() => {
      console.log("unmounted!");
    });
  },
};
</script>
```

我们将回调传递给生命周期函数。

`beforeCreate`和`created`被替换为`setup`方法。

下面是选项 API 挂钩的组合 API 等价物:

*   `beforeMount`->-
*   `mounted`->-`onMounted`
*   `beforeUpdate`->-`onBeforeUpdate`
*   `updated`->-`onUpdated`
*   `beforeDestroy`->-`onBeforeUnmount`
*   `destroyed`->-`onUnmounted`
*   `activated`->-`onActivated`
*   `deactivated`->-`onDeactivated`
*   `errorCaptured`——>——

左侧是选项 API 挂钩，右侧是组合 API 等价物。

组合 API 也有两个调试挂钩:

*   `onRenderTracked`
*   `onRenderTriggered`

我们可以写:

```
export default {
  onRenderTriggered(e) {
    debugger
  }
}
```

检查哪个依赖项导致组件重新呈现。

# 依赖注入

我们可以用`provide`和`inject`函数注入依赖关系。

`provide`和`inject`启用依赖注入，类似于 Vue 2.x 中的 project 和 inject。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { provide, inject } from "vue";const ThemeSymbol = Symbol();const Ancestor = {
  setup() {
    provide(ThemeSymbol, "dark");
  },
};export default {
  name: "App",
  setup() {
    const theme = inject(ThemeSymbol, "light");
    return {
      theme,
    };
  },
};
</script>
```

我们有`Ancestor`组件，它调用`provide`让我们把用`ThemeSymbol`标识的依赖关系传递给`App`组件。

在`App`的`setup`方法中，我们用`ThemeSymbol`调用`inject`来获取从`provide`传入的数据。

如果没有提供标识符`ThemeSymbol`，则`'light'`是默认值。

# 模板参考

组合 API 允许我们访问模板引用。

我们使用`ref`函数来创建 ref。

然后我们可以在模板中将它分配给我们想要的元素或组件。

例如，我们可以写:

```
<template>
  <div ref="root"></div>
</template><script>
import { ref, onMounted } from "vue";export default {
  name: "App",
  setup() {
    const root = ref(null); onMounted(() => {
      console.log(root.value);
    }); return {
      root,
    };
  },
};
</script>
```

我们用`ref`函数创建`root` ref。

然后我们将`ref`的名称设置为`ref`属性。

那么`root.value`将是 div。

如果我们使用一个渲染函数，我们写:

```
<template>
  <div></div>
</template><script>
import { ref, onMounted, h } from "vue";export default {
  name: "App",
  setup() {
    const root = ref(null); onMounted(() => {
      console.log(root.value);
    }); return () =>
      h("div", {
        ref: root,
      });
  },
};
</script>
```

为了将 ref 分配给我们在`h`函数中创建的 div。

# 结论

我们可以用组合 API 将生命周期挂钩和引用添加到我们的 Vue 3 应用程序中。

*更多内容看* [***说白了. io***](https://plainenglish.io/)