# 使用组合 API 创建 Vue 3 应用程序—检查反应属性

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-check-reactive-properties-9f3b2f4ebe51?source=collection_archive---------20----------------------->

![](img/24749510bdc0a890a385306bb1e5b2b8.png)

Photo by [Hermes Rivera](https://unsplash.com/@hermez777?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# `toRefs`

我们可以使用`toRefs`函数将引用转换成普通对象。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { reactive, toRefs } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      foo: 1,
      bar: 2,
    }); const stateAsRefs = toRefs(state);
    console.log(stateAsRefs); return {
      state,
    };
  },
};
</script>
```

将`state`反应属性转换为普通对象。

`state.foo`和`stat.bar`是无功属性，其值是我们在`reactive`函数中设置的值。

# `isRef`

`isRef`函数检查变量是否为 ref。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { isRef, reactive, ref } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      foo: 1,
      bar: 2,
    }); const r = ref(0);
    console.log(isRef(state));
    console.log(isRef(r)); return {
      state,
    };
  },
};
</script>
```

我们用`state`调用`isRef`，返回`false`。

而当我们用`r`调用`isRef`时，它返回`true`。

# `isProxy`

`isProxy`函数检查一个对象是被动的还是只读的。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { isProxy, reactive, readonly, ref } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      foo: 1,
      bar: 2,
    });
    const ro = readonly({ foo: 1 }); const r = ref(0);
    console.log(isProxy(state));
    console.log(isProxy(ro));
    console.log(isProxy(r)); return {
      state,
    };
  },
};
</script>
```

前两个控制台日志是日志`true`，因为我们用`reactive`和`readonly`创建了变量。

第三个记录了`false`，因为 ref 不是用`reactive`或`readonly`创建的。

# `isReactive`

我们可以用`isReactive`检查变量是否是从`reactive`创建的。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { isReactive, reactive, readonly, ref } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      foo: 1,
      bar: 2,
    });
    const ro = readonly({ foo: 1 }); const r = ref(0);
    console.log(isReactive(state));
    console.log(isReactive(ro));
    console.log(isReactive(r)); return {
      state,
    };
  },
};
</script>
```

只有`state`是用`reactive`函数创建的，所以只有第一个控制台日志记录`true`。

# `isReadonly`

我们可以检查用`readonly`创建的变量是否为`isReadonly`。

例如，我们可以写:

```
<template>
  <div></div>
</template><script>
import { isReadonly, reactive, readonly, ref } from "vue";
export default {
  name: "App",
  setup() {
    const state = reactive({
      foo: 1,
      bar: 2,
    });
    const ro = readonly({ foo: 1 }); const r = ref(0);
    console.log(isReadonly(state));
    console.log(isReadonly(ro));
    console.log(isReadonly(r)); return {
      state,
    };
  },
};
</script>
```

呼叫`isReadonly`。

只有第二控制台日志记录`true`，因为只有`ro`是用`readonly`创建的。

# 结论

我们可以使用 Vue 3 组合 API 中的各种函数对反应属性进行各种检查。

*更多内容看*[***plain English . io***](https://plainenglish.io/)