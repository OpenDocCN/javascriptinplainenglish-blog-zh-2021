# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—设置表单验证错误

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-set-form-validation-errors-12715ca0daa1?source=collection_archive---------6----------------------->

![](img/d118d9538471fb04b8a763cda774ab16.png)

Photo by [Trnava University](https://unsplash.com/@trnavskauni?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 初始误差

我们可以用错误消息初始化表单。

例如，我们可以写:

```
<template>
  <Form :initial-errors="initialErrors" :validation-schema="schema">
    <Field name="email" as="input" />
    <ErrorMessage name="email" />
    <br /> <Field name="name" as="input" type="text" />
    <br /> <Field name="password" as="input" type="password" />
    <ErrorMessage name="password" />
    <br /> <button type="submit">Submit</button>
  </Form>
</template><script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      email: yup.string().required().email(),
      name: yup.string().required(),
      password: yup.string().required().min(8),
    }); return {
      schema,
      initialErrors: {
        email: "This email is already taken",
        password: "The password is too short",
      },
    };
  },
};
</script>
```

我们将`initial-errors`道具设置为`initialErrors`反应属性。

它有字段名和相应的错误消息。

然后我们用`ErrorMessage`组件显示它们。

这对于显示从服务器端检索到的错误消息非常方便。

# 手动设置错误

我们也可以使用 Vee-Validate 4 手动设置错误。

我们可以用`setFieldError`方法为一个字段设置错误信息。

我们可以用`setErrors`方法为多个字段设置错误信息。

例如，我们可以写:

```
<template>
  <Form v-slot="{ setFieldError, setErrors }">
    <Field name="email" as="input" />
    <ErrorMessage name="email" />
    <br /> <Field name="password" as="input" />
    <ErrorMessage name="password" />
    <br /> <button type="button" @click="setFieldError('email', 'nope')">
      Set Single Error
    </button>
    <button
      type="button"
      @click="setErrors({ email: 'nope', password: 'wrong' })"
    >
      Set Multiple Errors
    </button>
  </Form>
</template><script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      email: yup.string().required().email(),
      name: yup.string().required(),
      password: yup.string().required().min(8),
    }); return {
      schema,
    };
  },
};
</script>
```

从`Form`组件的插槽支撑中访问`setFieldError`和`setError`方法。

然后我们在按钮的点击处理程序中调用它们。

`setFieldError`将表单字段名和错误消息作为参数。

而`setErrors`分别以表单字段名为关键字，以错误信息为对应值的对象。

我们可以在`submit`处理程序中调用相同的方法。

为此，我们写道:

```
<template>
  <Form @submit="onSubmit">
    <Field name="email" as="input" />
    <ErrorMessage name="email" />
    <br /> <Field name="password" as="input" />
    <ErrorMessage name="password" />
    <br /><input type="submit" />
  </Form>
</template><script>
import { Form, Field, ErrorMessage } from "vee-validate";
import * as yup from "yup";export default {
  components: {
    Form,
    Field,
    ErrorMessage,
  },
  data() {
    const schema = yup.object().shape({
      email: yup.string().required().email(),
      name: yup.string().required(),
      password: yup.string().required().min(8),
    }); return {
      schema,
    };
  },
  methods: {
    onSubmit(values, actions) {
      actions.setFieldError("email", "this email is already taken");
      actions.setErrors({
        email: "this field is already taken",
        password: "someone already has this password",
      });
    },
  },
};
</script>
```

我们从`onSubmit`提交处理程序的`actions`参数中调用相同的方法。

# 结论

我们可以使用 Vee-Validate 4 在 Vue 3 应用中手动设置表单验证错误消息。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)