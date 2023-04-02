# Vue.js 中的 v-model 和 v-bind 指令有什么区别？

> 原文：<https://javascript.plainenglish.io/whats-the-difference-between-v-model-and-v-bind-directives-in-vue-js-c38a73234c6b?source=collection_archive---------11----------------------->

![](img/c110fb6c9b5aec754e63bcb68388dc12.png)

Photo by [Gilly Stewart](https://unsplash.com/@gillystewart?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 有两个常用的内置指令。

它们是`v-model`和`v-bind`指令。

它们服务于不同的目的。

在本文中，我们将看看 Vue.js 中的`v-model`和`v-bind`指令之间的区别

# v 型装订

`v-bind`让我们在父组件和子组件之间进行单向绑定。

我们可以将数据从父组件传递到子组件。

子组件将接收数据作为道具。

例如，我们可以写:

`App.vue`

```
<template>
  <div id="app">
    <HelloWorld :name="name" />
  </div>
</template><script>
import HelloWorld from "./components/HelloWorld";export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      name: "jane",
    };
  },
};
</script>
```

`components/HelloWorld.vue`

```
<template>
  <div class="hello">hello {{ name }}</div>
</template>
<script>
export default {
  name: "HelloWorld",
  props: {
    name: String,
  },
};
</script>
```

在`App.vue`组件中，我们在带有`:name`指令的模板中有`HelloWorld`组件。

`:name`是`v-bind:name`的简称。

所以我们也可以写:

```
<template>
  <div id="app">
    <HelloWorld v-bind:name="name" />
  </div>
</template><script>
import HelloWorld from "./components/HelloWorld";export default {
  name: "App",
  components: {
    HelloWorld,
  },
  data() {
    return {
      name: "jane",
    };
  },
};
</script>
```

`name`是道具名。

我们将`name`反应属性设置为`name`属性的值。

在`HelloWorld.vue`中，我们在`props`属性中注册了`name`道具。

我们将道具的数据类型设置为`String`。

这是应该传入的数据类型。

并且`name`属性的值不是字符串，那么控制台中将会记录一个错误。

然后我们可以在模板中引用道具的值，或者用`this.name`在组件中引用。

因此，我们应该看到显示“hello jane”。

`v-bind`让我们将数据从父组件传递到子组件。

# v 型车

指令为我们提供了父组件和子组件之间的双向绑定。

这相当于添加了`value`道具并发射了`input`事件。

例如，我们可以写:

`App.vue`

```
<template>
  <div id="app">
    <CustomInput v-model="name" />
    <p>{{ name }}</p>
  </div>
</template><script>
import CustomInput from "./components/CustomInput";export default {
  name: "App",
  components: {
    CustomInput,
  },
  data() {
    return {
      name: "jane",
    };
  },
};
</script>
```

`components/CustomInput.vue`

```
<template>
  <div>
    <input :value="value" @input="$emit('input', $event.target.value)" />
  </div>
</template>
<script>
export default {
  name: "CustomInput",
  props: {
    value: String,
  },
};
</script>
```

在`App.vue`中，我们使用`v-model`将`CustomInput`组件绑定到`name`反应属性。

我们在`CustomInput`下方显示`name`值。

在`CustomInnput`组件中，我们注册了`value`属性。

我们将`value`传递给输入元素的`value`道具。

此外，我们监听输入事件。

当它被发出时，我们调用`$emit`来发出`input`事件，如 emit 的第一个参数所示。

`$event.target.value`有输入值。

由于`CustomInput`接受`value`属性并发出`input`事件，我们可以使用`v-model`在两个组件之间添加双向绑定。

当我们键入输入时，我们看到下面显示的`name`值发生了变化。

我们也可以写:

```
<template>
  <div>
    <input :value="value" @input="onInput" />
  </div>
</template>
<script>
export default {
  name: "CustomInput",
  props: {
    value: String,
  },
  methods: {
    onInput(event) {
      this.$emit("input", event.target.value);
    },
  },
};
</script>
```

在`CustomInput.vue`中。

`$emit`是与`onInput`方法中的`this.$emit`相同的模板。

`$event.target.value`替换为`event.target.value`。

# 结论

`v-bind`为我们提供了从父组件到子组件的单向绑定。

而`v-model`为我们提供了父子之间的双向绑定。

*更多内容请看*[***plain English . io***](http://plainenglish.io)