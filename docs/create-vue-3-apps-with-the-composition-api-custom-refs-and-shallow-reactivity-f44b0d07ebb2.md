# 使用组合 API 创建 Vue 3 应用程序—自定义引用和浅层反应

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-custom-refs-and-shallow-reactivity-f44b0d07ebb2?source=collection_archive---------17----------------------->

![](img/160c17952e0c6187dc43c5108be5e611.png)

Photo by [Jaunathan Gagnon](https://unsplash.com/@jaunathang?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# `customRef`

我们可以使用`customRef`函数来创建一个自定义 ref。

例如，我们可以写:

```
<template>
  <div>
    <input v-model="text" />
    {{ text }}
  </div>
</template><script>
import { customRef } from "vue";const useDebouncedRef = (value, delay = 200) => {
  let timeout;
  return customRef((track, trigger) => {
    return {
      get() {
        track();
        return value;
      },
      set(newValue) {
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          value = newValue;
          trigger();
        }, delay);
      },
    };
  });
};export default {
  name: "App",
  setup() {
    return {
      text: useDebouncedRef("hello world"),
    };
  },
};
</script>
```

我们创建了`useDebounceRef`函数，它返回由`customRef`函数创建的自定义 ref。

它使用一个带有`track`函数的回调函数来跟踪该值。

setter 调用`trigger`来触发状态更新。

我们将 setter 中的`value`传递给`newValue`，以便更新项目。

# `markRaw`

我们可以调用`markRaw`函数来标记一个对象，这样它就永远不会被转换成代理。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { isReactive, markRaw, reactive } from "vue";export default {
  name: "App",
  setup() {
    const foo = markRaw({});
    console.log(isReactive(reactive(foo)));
    return { foo };
  },
};
</script>
```

控制台日志记录了`false`，因为我们调用了`markRaw`来禁用我们传递给它的对象的反应。

但是，如果我们将一个对象标记为 raw，并在另一个对象中引用该对象，那么它们将被视为不相等，即使它们具有相同的引用:

```
<template>
  <div></div>
</template><script>
import { isReactive, markRaw, reactive } from "vue";export default {
  name: "App",
  setup() {
    const foo = markRaw({
      nested: {},
    }); const bar = reactive({
      nested: foo.nested,
    }); console.log(foo.nested === bar.nested);
    return { foo };
  },
};
</script>
```

我们将`bar.nested`设置为`foo.nested`，但是控制台日志是`false`。

# `shallowReactive`

我们可以用`shallowReactive`函数创建一个浅层反应对象。

reactive 属性仅限于对象的顶级属性。

例如，我们可以写:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ state.foo }}
    {{ state.nested.bar }}
  </div>
</template><script>
import { isReactive, shallowReactive } from "vue";export default {
  name: "App",
  setup() {
    const state = shallowReactive({
      foo: 1,
      nested: {
        bar: 2,
      },
    }); const increment = () => {
      state.foo++;
      state.nested.bar++;
    };
    console.log(isReactive(state.nested.bar));
    return { state, increment };
  },
};
</script>
```

在`increment`函数中，我们增加了`state.foo`和`state.nested.bar`，它们都将在模板中更新。

但是当我们用`isReactive`记录`state.nested.bar`时，我们会记录`false`。

因为它不是反应式的，所以不会触发观察器运行:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="increment">increment</button>
    {{ state.foo }}
    {{ state.nested.bar }}
  </div>
</template><script>
import { isReactive, shallowReactive, watch } from "vue";export default {
  name: "App",
  setup() {
    const state = shallowReactive({
      foo: 1,
      nested: {
        bar: 2,
      },
    }); const increment = () => {
      state.foo++;
      state.nested.bar++;
    }; watch(state.nested.bar, (bar) => {
      console.log(bar);
    }); return { state, increment };
  },
};
</script>
```

那么当`state.nested.bar`更新时，第二个参数中的`watch`回调将不会运行。

# 结论

我们可以使用 Vue 3 的组合 API 提供的各种功能来创建各种反应性和非反应性属性。

*更多内容看*[***plain English . io***](https://plainenglish.io/)