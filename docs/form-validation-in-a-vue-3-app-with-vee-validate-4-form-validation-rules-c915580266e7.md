# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—表单验证规则

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-form-validation-rules-c915580266e7?source=collection_archive---------10----------------------->

![](img/2273cb9979691577f3158093a7b60860.png)

Photo by [Susan Holt Simpson](https://unsplash.com/@shs521?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 多参数规则

我们可以拥有带有多个参数的全局验证规则。

为了定义和使用它们，我们编写:

```
<template>
  <Form @submit="onSubmit">
    <Field name="number" as="input" rules="required|min:0,100" />
    <ErrorMessage name="number" />
    <br /> <button>Submit</button>
  </Form>
</template><script>
import { Form, Field, ErrorMessage, defineRule } from "vee-validate";defineRule("required", (value) => {
  if (!value || !value.length) {
    return "This field is required";
  }
  return true;
});defineRule("min", (value, [min, max]) => {
  if (!value || !value.length) {
    return true;
  }
  const numericValue = +value;
  if (numericValue < min) {
    return `This field must be greater than ${min}`;
  }
  if (numericValue > max) {
    return `This field must be less than ${max}`;
  }
  return true;
});export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {},
  methods: {
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
```

我们用`min`和`max`参数定义了`min`规则。

我们对照它们进行检查，以返回正确的验证结果。

`true`表示该值有效。

否则，我们返回一个错误消息字符串。

然后在`rules`道具中，我们将`required`规则和`min`规则结合起来。

# 模式验证

我们可以将规则添加到验证模式中。

例如，我们可以写:

```
<template>
  <Form @submit="submit" :validation-schema="schema" v-slot="{ errors }">
    <Field name="email" as="input" />
    <span>{{ errors.email }}</span>
    <br /> <Field name="password" as="input" type="password" />
    <span>{{ errors.password }}</span>
    <br /> <button>Submit</button>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";defineRule("required", (value) => {
  if (!value || !value.length) {
    return "This field is required";
  }
  return true;
});defineRule("email", (value) => {
  if (!value || !value.length) {
    return true;
  }
  if (!/[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}/.test(value)) {
    return "This field must be a valid email";
  }
  return true;
});defineRule("minLength", (value, [limit]) => {
  if (!value || !value.length) {
    return true;
  }
  if (value.length < limit) {
    return `This field must be at least ${limit} characters`;
  }
  return true;
});export default {
  components: {
    Form,
    Field,
  },
  data() {
    const schema = {
      email: "required|email",
      password: "required|minLength:8",
    }; return {
      schema,
    };
  },
  methods: {
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
```

我们定义了`required`、`email`和`minLength`规则。

然后我们把它们都放在`schema`对象中。

然后我们将`validation-schema`道具设置为`schema`反应属性。

然后我们通过从`Form`组件的 slot props 中获取`errors`对象来显示错误消息。

现在，当我们使用表单时，验证规则将用于验证表单。

# 结论

我们可以使用 Vee-Validate 4 在 Vue 3 应用中验证更复杂的表单。

*更多内容看* [***说白了. io***](https://plainenglish.io/)