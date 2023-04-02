# 使用 Composition API 创建 Vue 3 应用程序—参考文献

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-refs-e9e9bde115f3?source=collection_archive---------18----------------------->

![](img/5d6d0c8a86cce606605006c018622ae6.png)

Photo by [Weston Eichner](https://unsplash.com/@westoneichner?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

它让我们可以轻松提取逻辑，而不必担心代码中`this`的值。

它与 TypeScript 一起工作也更好，因为`this`的值不再需要被键入。

在本文中，我们将了解如何使用 Composition API 创建 Vue 3 应用程序。

# 使用带 v-for 的 ref

我们可以为使用`v-for`渲染的项目分配参考。

例如，我们可以写:

```
<template>
  <div
    v-for="(item, i) in list"
    :ref="
      (el) => {
        divs[i] = el;
      }
    "
    :key="i"
  >
    {{ item }}
  </div>
</template><script>
import { ref, reactive, onBeforeUpdate } from "vue";export default {
  setup() {
    const list = reactive([1, 2, 3]);
    const divs = ref([]); onBeforeUpdate(() => {
      divs.value = [];
    }); return {
      list,
      divs,
    };
  },
};
</script>
```

我们通过`ref`功能创建`divs`反应性。

然后，当我们用`v-for`渲染项目时，我们将`el` HTML 元素对象指定为`divs`数组的一个条目。

# 反应性实用程序

Vue 3 组合应用编程接口附带了一些实用功能来完成各种具有反应特性的事情。

## 未精炼的

`unref`函数允许我们返回 ref 的值，或者我们传递给`ref`函数的参数，这取决于变量是否是 ref。

例如，我们可以写:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ count }}
  </div>
</template><script>
import { ref, unref, watch } from "vue";
export default {
  name: "App",
  setup() {
    const count = ref(0);
    const increment = () => {
      count.value++;
    };
    watch(count, () => {
      console.log(unref(count));
    }); return {
      count,
      increment,
    };
  },
};
</script>
```

我们创造了`count`反应性。

在`watch`回调中，我们调用`unref(count)`得到`count`反应性的实际值。

如果它不是引用，它会返回我们传入的变量的值。

## `toRef`

`toRef`功能允许我们为反应源对象上的属性创建一个引用。

例如，我们可以写:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="increment">increment</button>
    {{ count }}
    {{ state.count }}
  </div>
</template><script>
import { reactive, toRef } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      count: 1,
    }); const count = toRef(state, "count");
    const increment = () => {
      state.count++;
    }; return {
      state,
      count,
      increment,
    };
  },
};
</script>
```

我们调用`toRef`从`state.count`属性创建引用。

现在我们可以将它包含在返回的对象中，然后在模板中引用它。

如果我们想把它传递给合成函数，这是很有用的。

例如，我们可以写:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ count }}
    {{ state.count }}
  </div>
</template><script>
import { reactive, toRef, watch } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      count: 1,
    }); const count = toRef(state, "count");
    const increment = () => {
      state.count++;
    }; watch(count, (count) => console.log(count)); return {
      state,
      count,
      increment,
    };
  },
};
</script>
```

我们将`count`传递给`watch`，这样我们就可以观察它的价值。

# 结论

我们可以给 HTML 元素分配引用，让我们可以在组件中访问它们。

我们可以使用 Vue 3 的合成 API 附带的各种函数来操纵 refs。

*多内容见于* [***中***](https://plainenglish.io/)