# 如何用 Vue.js 正确地观察嵌套数据

> 原文：<https://javascript.plainenglish.io/how-to-properly-watch-for-nested-data-with-vue-js-3ac7ca964067?source=collection_archive---------7----------------------->

![](img/693724f381c632998bee756015ab60c7.png)

Photo by [Mateusz Stępień](https://unsplash.com/@m_stepien?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

观察深度嵌套的对象状态和道具是我们在 Vue.js 应用程序中经常要做的事情。

在本文中，我们将研究如何正确地观察 Vue.js 组件中的嵌套数据。

# 深度观察者

我们可以向`watch`属性中的组件添加深度观察器。

例如，我们可以写:

`App.vue`

```
<template>
  <div id="app">
    <button
      @click="
        id++;
        getTodo(id);
      "
    >
      increment id
    </button>
    <Todo :todo="todo" />
  </div>
</template><script>
import Todo from "./components/Todo";export default {
  name: "App",
  components: {
    Todo,
  },
  data() {
    return {
      todo: {},
      id: 1,
    };
  },
  methods: {
    async getTodo(id) {
      const results = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${id}`
      );
      const data = await results.json();
      this.todo = data;
    },
  },
};
</script>
```

`Todo.vue`

```
<template>
  <div class="hello"></div>
</template><script>
export default {
  name: "Todo",
  props: {
    todo: Object,
  },
  watch: {
    todo: {
      handler(val) {
        console.log(val);
      },
      deep: true,
    },
  },
};
</script>
```

我们有一个按钮，当我们用给定的`id`获取一个新的`todo`对象时，它会调用`getTodo`。

`getTodo`从响应中更新`todo`反应属性。

我们将`todo`值传递给`Todo`组件的`todo`属性。

然后在`Todo`组件中，我们观察具有`watch`属性的`todo`道具。

我们使用带有`val`参数的`handler`函数来获取最新的值。

`deep`设置为`true`，这样我们就可以观察物体道具的属性。

# 计算属性

我们可以创建一个计算属性来从反应属性中获取属性。

例如，我们可以写:

`Todo.vue`

```
<template>
  <div>{{ todoTitle }}</div>
</template><script>
export default {
  name: "Todo",
  props: {
    todo: Object,
  },
  computed: {
    todoTitle() {
      return this.todo.title;
    },
  },
};
</script>
```

我们保持`App.vue`不变。

我们创建了返回`this.todo.title`属性的`todoTitle`计算属性。

然后，我们可以在模板中使用它，就像其他任何反应属性一样。

每当`this.todo`对象中的任何属性被更新时，`todoTitle`将被更新。

# 观察对象的属性

我们还可以观察一个对象的属性。

例如，我们可以写:

```
<template>
  <div class="hello"></div>
</template><script>
export default {
  name: "Todo",
  props: {
    todo: Object,
  },
  watch: {
    "todo.title": {
      handler(val) {
        console.log(val);
      },
    },
  },
};
</script>
```

然后`todo`道具的`title`属性被观察者观察。

这是因为`'todo.title'`是`todo`道具的`title`属性。

`val`将具有`todo`属性的`title`属性值。

我们可以从 watcher 函数中得到`newVal`和`oldVal`:

```
<template>
  <div class="hello"></div>
</template><script>
export default {
  name: "Todo",
  props: {
    todo: Object,
  },
  watch: {
    "todo.title": {
      handler(newVal, oldVal) {
        console.log(newVal, oldVal);
      },
    },
  },
};
</script>
```

# 结论

我们可以通过向带有属性路径的`watch`属性对象添加方法，用观察器来观察嵌套的属性。

此外，我们可以将`deep`设置为`true`来观察深度嵌套的属性。

感谢您的阅读，希望这篇文章对您有所帮助。

[*更多内容敬请关注*](http://plainenglish.io/)