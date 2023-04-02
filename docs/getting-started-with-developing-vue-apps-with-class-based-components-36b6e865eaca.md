# 开始使用基于类的组件开发 Vue 应用

> 原文：<https://javascript.plainenglish.io/getting-started-with-developing-vue-apps-with-class-based-components-36b6e865eaca?source=collection_archive---------7----------------------->

![](img/8e7ae3a995a0e0d8f4fb40753f90d346.png)

Photo by [Geert Pieters](https://unsplash.com/@shotsbywolf?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果我们更喜欢使用类，我们可以使用 Vue 自带的基于类的组件 API。

在本文中，我们将看看如何用基于类的组件开发 Vue 应用。

# 入门指南

我们可以像往常一样用 Vue CLI 的`vue create`命令创建我们的 Vue 项目。

然后我们通过运行以下命令来安装`vue-class-component`库:

```
npm install --save vue vue-class-component
```

与 NPM 或:

```
yarn add --save vue vue-class-component
```

用纱线。

如果我们使用 TypeScript，我们还必须将`experimentDecorators`选项添加到`tsconfig.json`中，这样我们就可以使用 decorators。

我们应该把下面这些放进它的`compilerOptions`属性中:

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "es2015",
    "moduleResolution": "node",
    "strict": true,
    "experimentalDecorators": true
  }
}
```

如果我们使用的是 Babel，我们必须通过运行以下命令来安装`@babel/plugin-proposal-decorators`和`@babel/plugin-proposal-class-properties`包:

```
npm install --save-dev @babel/plugin-proposal-decorators @babel/plugin-proposal-class-properties
```

在`.babelrc`中，我们添加:

```
{
  "plugins": [
    ["@babel/proposal-decorators", { "legacy": true }],
    ["@babel/proposal-class-properties", { "loose": true }]
  ]
}
```

让我们添加没有绑定到类的 decorators 和类属性。

# 创建我们的第一个组件

现在我们可以使用`vue-class-component`模型来创建我们的第一个基于类的组件。

例如，我们可以写:

`components/HelloWorld.vue`

```
<template>
  <div>{{ message }}</div>
</template><script>
import Vue from 'vue'
import Component from 'vue-class-component'@Component
export default class HelloWorld extends Vue {
  message = 'Hello World'
}
</script>
```

`App.vue`

```
<template>
  <div id="app">
    <HelloWorld />
  </div>
</template><script>
import HelloWorld from "./components/HelloWorld";export default {
  name: "App",
  components: {
    HelloWorld,
  },
};
</script>
```

在`HelloWorld.vue`中，我们让`HelloWorld`类具有未绑定到`HelloWorld`实例的`message`属性。

我们可以在模板中使用它。

此外，我们可以添加`data`方法并返回一个具有反应属性的对象:

```
<template>
  <div>{{ message }}</div>
</template><script>
import Vue from "vue";
import Component from "vue-class-component";@Component
export default class HelloWorld extends Vue {
  data() {
    return {
      message: "Hello World",
    };
  }
}
</script>
```

用`data`返回的`message`属性是反应性的，所以我们可以在模板中使用它。

要添加方法，我们将它们作为类方法添加:

```
<template>
  <div>
    <button @click="increment">increment</button>
    {{ count }}
  </div>
</template><script>
import Vue from "vue";
import Component from "vue-class-component";@Component
export default class HelloWorld extends Vue {
  count = 0; increment() {
    this.count++;
  }
}
</script>
```

我们添加了`increment`方法来将`count`的反应属性增加 1。

我们将其作为值传递给`@click`指令。

# 结论

我们可以用`vue-class-component`库在我们的 Vue 应用中添加基于类的组件。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)