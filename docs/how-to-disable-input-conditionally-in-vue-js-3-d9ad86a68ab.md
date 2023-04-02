# 如何在 Vue.js 3 中有条件的禁用输入？

> 原文：<https://javascript.plainenglish.io/how-to-disable-input-conditionally-in-vue-js-3-d9ad86a68ab?source=collection_archive---------8----------------------->

![](img/da12c89c3f0ee6bfa9aec4a61e1e3050.png)

Photo by [Victor Barrios](https://unsplash.com/@thevictorbarrios?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 Vue 3 应用中有条件地禁用输入。

在本文中，我们将研究如何在 Vue 3 中有条件地禁用输入元素。

# 在 Vue.js 3 中有条件地禁用输入

当我们想要禁用输入时，我们可以通过设置`disabled`属性来有条件地禁用 Vue 3 的输入。

例如，我们可以写:

```
<template>
  <input :disabled="disabled" />
  <button @click="disabled = !disabled">toggle disable</button>
</template><script>
export default {
  name: "App",
  data() {
    return {
      disabled: false,
    };
  },
};
</script>
```

我们将输入的`disabled`属性设置为`disabled`反应属性。

在那下面，我们有一个`@click`指令，当我们点击按钮时，它切换`disabled`反应属性。

当`disabled`为`true`时，输入将被禁用。

所以当我们重复点击按钮时，输入将被禁用并再次启用。

# 结论

我们可以用 Vue 3 有条件地禁用一个输入，方法是将输入的`disabled`属性设置为一个表达式，该表达式具有我们希望何时禁用输入的条件。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)