# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—验证嵌套对象

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-validate-nested-objects-77a51d32a674?source=collection_archive---------11----------------------->

![](img/39660cba902ded428ff7602b0b7e5ff6.png)

Photo by [Calvin Chin](https://unsplash.com/@winglingsux?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 从表单的引用中调用 Set 表单验证方法

我们可以从`Form`组件的引用中访问`setFieldError`和`setErrors`方法。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" ref="myForm">
    <Field name="email" as="input" />
    <ErrorMessage name="email" />
    <br /> <Field name="password" as="input" />
    <ErrorMessage name="password" />
    <br /> <input type="submit" />
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
    onSubmit(values) {
      this.$refs.myForm.setFieldError("email", "this email is already taken");
      this.$refs.myForm.setErrors({
        email: "this field is already taken",
        password: "someone already has this password",
      });
    },
  },
};
</script>
```

我们从表单的 ref 中调用`setFieldError`和`setErrors`。

# 验证嵌套对象

我们可以用`Field`组件验证嵌套的表单对象。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" :validation-schema="schema">
    <Field name="links.twitter" type="url" />
    <ErrorMessage name="links.twitter" />
    <br /> <Field name="links.github" type="url" />
    <ErrorMessage name="links.github" />
    <br /> <button>Submit</button>
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
      links: yup.object().shape({
        twitter: yup.string().url(),
        github: yup.string().url(),
      }),
    });
    return {
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

我们将`name`属性设置为我们想要在`Field`和`ErrorMessage`组件中验证的字段的路径。

在`schema`对象中，我们做同样的事情。

我们调用`yup.object().shape()`并将`links`属性添加到我们作为参数传入的对象中。

# 验证嵌套数组

我们还可以使用 Vee-Validate 4 来验证嵌套数组。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" :validation-schema="schema">
    <Field name="links[0]" type="url" />
    <ErrorMessage name="links[0]" />
    <br /> <Field name="links[1]" type="url" />
    <ErrorMessage name="links[1]" />
    <br /> <button>Submit</button>
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
      links: yup.array().of(yup.string().url()),
    });
    return {
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

添加数组验证。

我们可以通过编写以下代码来检查字符串数组是否是 URL:

```
yup.array().of(yup.string().url())
```

# 组合 API

如果我们使用组合 API，我们可以向 Vue 3 组件添加验证。

为此，我们写道:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }" :validation-schema="schema">
    <Field name="user.name" as="input" />
    <span id="nameErr">{{ errors["user.name"] }}</span>
    <br /> <Field name="user.addresses[0]" as="input" id="address" />
    <span id="addrErr">{{ errors["user.addresses[0]"] }}</span>
    <br /> <button id="submit">Submit</button>
  </Form>
</template><script>
import { Form, Field } from "vee-validate";
import * as yup from "yup";export default {
  components: {
    Form,
    Field,
  },
  setup() {
    return {
      schema: yup.object({
        user: yup.object({
          name: yup.string().required(),
          addresses: yup.array().of(yup.string().required()),
        }),
      }),
      onSubmit(values) {
        console.log(values);
      },
    };
  },
};
</script>
```

`setUp`方法返回`schema`反应属性和`onSubmit`方法。

# 结论

我们可以用组合 API 验证表单，并验证对象和嵌套数组。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**