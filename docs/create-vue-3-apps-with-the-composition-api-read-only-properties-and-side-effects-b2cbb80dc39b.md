# 使用组合 API 创建 Vue 3 应用程序——只读属性和副作用

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-read-only-properties-and-side-effects-b2cbb80dc39b?source=collection_archive---------13----------------------->

![](img/a4653631ea832b55c5c6da9e2413b9bd.png)

Photo by [Mert Kahveci](https://unsplash.com/@mertkahveci?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 自带内置的 Composition API。

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# 只读属性

我们可以用 composition API 向我们的 Vue 3 应用程序添加一个只读属性。

为了添加它，我们使用了`readonly`属性:

```
<template>
  <div>{{ copy }}</div>
</template><script>
import { reactive, readonly } from "vue";
export default {
  name: "App",
  setup() {
    const original = reactive({ count: 0 });
    const copy = readonly(original);
    return {
      copy,
    };
  },
};
</script>
```

我们用`reactive`定义`original`无功属性。

然后我们用`original`调用`readonly`来创建原始文件的只读深层副本。

我们归还它，所以我们可以使用它。

# 观察反应特性

我们可以用`watchEffect`方法观察反应特性。

例如，我们可以写:

```
<template>
  <div>{{ count }}</div>
</template><script>
import { ref, watchEffect } from "vue";
export default {
  name: "App",
  setup() {
    const count = ref(0);
    watchEffect(() => console.log(count.value)); setTimeout(() => {
      count.value++;
    }, 100); return {
      count,
    };
  },
};
</script>
```

当`count`的值在`setTimeout`回调中更新时，我们用回调函数调用`watchEffect`来记录它的值。

`watchEffect`返回一个函数，我们可以用它来停止观察器。

为了使用它，我们写:

```
<template>
  <div>{{ count }}</div>
</template><script>
import { onBeforeUnmount, ref, watchEffect } from "vue";
export default {
  name: "App",
  setup() {
    const count = ref(0);
    const stop = watchEffect(() => console.log(count.value)); setTimeout(() => {
      count.value++;
    }, 100); onBeforeUnmount(() => stop()); return {
      count,
    };
  },
};
</script>
```

当我们卸载组件时，我们在`onBeforeUnmount`回调中调用`stop`来停止观察器。

同样，我们可以用`onInvalidate`函数使副作用无效。

例如，我们可以写:

```
<template>
  <div>{{ size }}</div>
</template><script>
import { onBeforeMount, reactive, watchEffect } from "vue";
export default {
  name: "App",
  setup() {
    const size = reactive({
      width: 0,
      height: 0,
    }); const onResize = () => {
      size.width = window.innerWidth;
      size.height = window.innerHeight;
    };
    onBeforeMount(() => window.addEventListener("resize", onResize)); watchEffect((onInvalidate) => {
      onInvalidate(() => {
        window.removeEventListener("resize", onResize);
      });
    }); return {
      size,
    };
  },
};
</script>
```

调用`window.removeEventListener`删除`onInvalidate`回调中的事件监听器。

当我们通过将屏幕附加为`resize`事件的监听器来改变屏幕时，`onResize`函数设置`size`。

# 结论

我们可以用 Vue 3 的 composition API 添加只读属性和观察副作用。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)