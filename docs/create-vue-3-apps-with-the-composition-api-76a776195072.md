# 使用复合 API 创建 Vue 3 应用程序

> 原文：<https://javascript.plainenglish.io/create-vue-3-apps-with-the-composition-api-76a776195072?source=collection_archive---------20----------------------->

![](img/be38e1d732fab76135b81f6a6a56f21c.png)

Photo by [Weston MacKinnon](https://unsplash.com/@betteratf8?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 自带内置的 Composition API。

它让我们可以轻松地提取逻辑，而不必担心代码中`this`的值。

使用 TypeScript 也能更好地工作，因为不再需要键入`this`的值。

在本文中，我们将看看如何用复合 API 创建 Vue 3 应用程序。

# 基本示例

我们可以通过定义反应属性并在模板中使用它们来创建一个基本的应用程序。

例如，我们可以写:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ count }}
  </div>
</template><script>
import { ref } from "vue";export default {
  setup() {
    const count = ref(0); function increment() {
      count.value++;
    } return {
      count,
      increment,
    };
  },
};
</script>
```

我们用`ref`函数定义了`count`无功属性。

0 是它的初始值。

我们添加了`increment`函数来更新它的值。

它的更新不同于选项 API 中的更新。我们必须更新`value`属性，用原始值更新反应属性。

然后我们返回`count`和`increment`，这样我们就可以使用它们作为模板。

`setup`是一个在我们挂载组件时运行的方法。

我们可以用`reactive`函数定义对象值反应属性。

为此，我们写道:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ state.count }}
  </div>
</template><script>
import { reactive } from "vue";export default {
  setup() {
    const state = reactive({
      count: 0,
    });
    function increment() {
      state.count++;
    } return {
      state,
      increment,
    };
  },
};
</script>
```

我们用一个初始对象值调用`reactive`。

然后我们将其分配给`state`反应属性。

在`increment`函数中，我们更新`state.count`属性来更新它的值。

我们返回`state`和`count`以便在模板中使用它们。

# 计算属性

为了创建一个计算属性，我们可以使用`computed`函数。

为此，我们写道:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="increment">increment</button>
    {{ state.count }}
    {{ double }}
  </div>
</template><script>
import { reactive, computed } from "vue";export default {
  setup() {
    const state = reactive({
      count: 0,
    });
    const double = computed(() => state.count * 2); function increment() {
      state.count++;
    } return {
      state,
      double,
      increment,
    };
  },
};
</script>
```

我们将一个回调传递到`computed`方法中，以返回我们想要的计算属性的值。

可以在我们传递给`reactive`的对象中调用`computed`来添加计算的属性作为另一个反应属性的属性。

# 观察者

我们可以使用`watch`功能在 Vue 应用程序中添加一个观察器。

例如，我们可以写:

```
<template>
  <div>
    <button [@click](http://twitter.com/click)="increment">increment</button>
    {{ state.count }}
  </div>
</template><script>
import { reactive, watch } from "vue";export default {
  setup() {
    const state = reactive({
      count: 0,
    });
    function increment() {
      state.count++;
    }
    watch(
      () => state.count,
      (count) => {
        console.log(count);
      },
      { immediate: true }
    );
    return {
      state,
      increment,
    };
  },
};
</script>
```

来补充一下。

`watch`的第一个参数是一个返回`state.count`反应属性的函数。

在第二个参数中，我们用`count`获取`state.count`的最新值并记录下来。

第三个参数是一个带有观察器选项的对象。

我们可以在那里设置`deep`和`immediate`，就像我们对选项 API 所做的那样。

`deep`表示观察对象的所有嵌套属性的变化。

`immediate`表示当组件安装后，观察器立即运行。

# 结论

我们可以使用 Vue 3 组合 API 来定义我们的组件。

我们在 options API 中拥有的所有东西仍然可用，只是做了一些改进。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)