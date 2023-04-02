# 如何正确地观察 Vue.js 3 组件中的嵌套数据？

> 原文：<https://javascript.plainenglish.io/how-to-properly-watch-for-nested-data-in-vue-js-3-components-712aad7b03a3?source=collection_archive---------3----------------------->

![](img/5cfb23d12173a7c8304d9dbfb5dd09b0.png)

Photo by [Orijit Chatterjee](https://unsplash.com/@orijit57?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们必须注意 Vue 3 组件中的嵌套数据。

在本文中，我们将看看如何在 Vue 3 组件中观察嵌套数据。

# 添加嵌套数据观察器

要添加观察 reactive properties 中嵌套数据的观察器，我们可以将`deep`选项设置为`true`。

例如，我们可以写:

```
<template>
  <div>{{ person }}</div>
</template><script>
export default {
  name: "App",
  watch: {
    person: {
      deep: true,
      immediate: true,
      handler(val) {
        console.log(val);
      },
    },
  },
  data() {
    return {
      person: {
        firstName: "jane",
        lastName: "smith",
      },
    };
  },
};
</script>
```

观看`person`的对象。

我们将`deep`设置为`true`,以便在方法中的任何属性发生变化时运行`handler`方法。

将`immediate`属性设置为`true`以在`person`初始值被设置时运行`handler`方法。

因此，当我们设置`person`反应属性时，我们应该看到`console.log`方法记录了`val`值。

此外，我们可以观察对象中任何单个属性的变化。

例如，我们可以写:

```
<template>
  <div>{{ person }}</div>
</template><script>
export default {
  name: "App",
  watch: {
    "person.firstName": {
      immediate: true,
      handler(val) {
        console.log(val);
      },
    },
  },
  data() {
    return {
      person: {
        firstName: "jane",
        lastName: "smith",
      },
    };
  },
};
</script>
```

我们有 `“person.firstName”`观察器来观察`person.firstName`值的变化。

那么`val`参数应该记录`person.firstName`的值，也就是`'jane'`。

# 结论

我们可以通过 Vue 3 中的观察器轻松地观察反应属性中的嵌套数据。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)