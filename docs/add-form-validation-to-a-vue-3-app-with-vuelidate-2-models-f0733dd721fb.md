# 将表单验证添加到 Vue 3 应用程序中，该应用程序带有 Vue lidate 2-型号和脏污

> 原文：<https://javascript.plainenglish.io/add-form-validation-to-a-vue-3-app-with-vuelidate-2-models-f0733dd721fb?source=collection_archive---------9----------------------->

![](img/13b339d8e81622263b8bafa92311b1ef.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vuelidate 2 是一个流行的为 Vue 3 应用程序制作的表单验证库。

在本文中，我们将了解如何将表单验证添加到带有 Vuelidate 2 的 Vue 3 应用程序中。

# $模型

我们可以将表单域绑定到`$model`属性。

这样，只有当字段变脏时，我们才能显示错误。

例如，我们可以写:

```
<template>
  <div>
    <input v-model="v$.name.$model" />
    <template v-if="v$.name.$dirty">
      <div v-for="error of v$.name.$silentErrors" :key="error.$message">
        <div>{{ error.$message }}</div>
      </div>
    </template>
  </div>
</template><script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";export default {
  name: "App",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      name: "",
    };
  },
  validations() {
    return {
      name: { required },
    };
  },
};
</script>
```

我们有`v$`反应属性，用于进行所有的表单验证检查。

一旦`v$.name.$model`被操纵，`$dirty`就会变成`true`。

我们通过渲染`v$.name.$silentErrors`中的条目来显示错误信息。

此外，我们可以将`$autoDirty`属性设置为`true`以使被操作的字段的`$dirty`属性自动设置为`true`。

为此，我们写道:

```
<template>
  <div>
    <input v-model="v$.name.$model" />
    <template v-if="v$.name.$dirty">
      <div v-for="error of v$.name.$silentErrors" :key="error.$message">
        <div>{{ error.$message }}</div>
      </div>
    </template>
  </div>
</template><script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";export default {
  name: "App",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      name: "",
    };
  },
  validations() {
    return {
      name: { required, $autoDirty: true },
    };
  },
};
</script>
```

# 惰性验证

我们也可以将`$lazy`属性设置为`true`以使 Vuelidate 仅在字段被操作时验证字段。

例如，我们可以写:

```
<template>
  <div>
    <input v-model="v$.name.$model" />
    <template v-if="v$.name.$dirty">
      <div v-for="error of v$.name.$silentErrors" :key="error.$message">
        <div>{{ error.$message }}</div>
      </div>
    </template>
  </div>
</template><script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";export default {
  name: "App",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      name: "",
    };
  },
  validations() {
    return {
      name: { required, $lazy: true },
    };
  },
};
</script>
```

在`validations`方法中设置属性。

# 显示更多错误信息

要显示更多错误信息，我们可以写:

```
<template>
  <div>
    <input v-model="v$.name.$model" />
    <template v-if="v$.name.$dirty">
      <div v-for="error of v$.name.$silentErrors" :key="error.$message">
        <strong>{{ error.$validator }}</strong>
        <span> on property</span>
        <strong>{{ error.$property }}</strong>
        <span> says:</span>
        <strong>{{ error.$message }}</strong>
      </div>
    </template>
  </div>
</template><script>
import useVuelidate from "@vuelidate/core";
import { required } from "@vuelidate/validators";export default {
  name: "App",
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      name: "",
    };
  },
  validations() {
    return {
      name: { required, $lazy: true },
    };
  },
};
</script>
```

`error.$validation`以字符串形式表示验证规则的名称。

`error.$property`将字段名称作为字符串。

`error.$message`有表单验证错误信息。

# 结论

我们可以在 Vue 3 应用程序中设置如何使用 Vuelidate 2 触发表单验证。

此外，我们可以显示比消息更多的错误信息。

[*更多内容参见*](http://plainenglish.io/)