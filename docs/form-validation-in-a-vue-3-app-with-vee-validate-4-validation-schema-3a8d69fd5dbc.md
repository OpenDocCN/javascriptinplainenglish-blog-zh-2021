# 使用 Vee-Validate 4-验证模式在 Vue 3 应用程序中进行表单验证

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-validation-schema-3a8d69fd5dbc?source=collection_archive---------13----------------------->

![](img/425fa3d8403ff31e6d7528e2d3347475.png)

Photo by [Macau Photo Agency](https://unsplash.com/@macauphotoagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 字段级验证

我们可以用`Field`组件验证字段。

例如，我们可以写:

```
<template>
  <Form v-slot="{ errors }">
    <Field name="field" as="input" :rules="isRequired" />
    <br />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
import { Field, Form } from "vee-validate";
export default {
  components: {
    Field,
    Form,
  },
  methods: {
    isRequired(value) {
      return value ? true : "This field is required";
    },
  },
};
</script>
```

我们有`Field`组件，它有`as`属性来设置要呈现的元素的标签名。

`rules`具有字段验证功能。

如果`value`有效，则`isRequired`函数返回`true`，否则返回验证错误消息。

有我们输入的内容。

我们也可以使用第三方库进行验证。

例如，我们可以通过编写以下代码使用`yup`库进行验证:

```
<template>
  <Form v-slot="{ errors }">
    <Field name="field" as="input" :rules="passwordRules" />
    <br />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
import { Field, Form } from "vee-validate";
import * as yup from "yup";export default {
  components: {
    Field,
    Form,
  },
  data() {
    return {
      passwordRules: yup.string().required().min(8),
    };
  },
};
</script>
```

我们将`passwordRules` reactive 属性设置为`yup.string().required().min(8)`来验证我们输入的值是一个最少包含 8 个字符的字符串。

# 表单级验证

我们还可以使用 Vee-Validate 4 添加表单级验证。

例如，我们可以写:

```
<template>
  <Form @submit="submit" :validation-schema="simpleSchema" v-slot="{ errors }">
    <Field name="email" as="input" />
    <span>{{ errors.email }}</span>
    <br />
    <Field name="password" as="input" type="password" />
    <span>{{ errors.password }}</span>
    <br />
    <button>Submit</button>
  </Form>
</template>
<script>
import { Field, Form } from "vee-validate";
export default {
  components: {
    Field,
    Form,
  },
  data() {
    const simpleSchema = {
      email(value) {
        return /\S+@\S+\.\S+/.test(value) ? true : "email is not valid";
      },
      password(value) {
        return value || "password is required";
      },
    };
    return {
      simpleSchema,
    };
  },
  methods: {
    submit() {},
  },
};
</script>
```

我们将`validation-schema`设置为`simpleSchema`对象，该对象具有我们想要验证的每个字段的验证函数。

`simpleSchema`中的函数名应该与`Field`组件的`name`属性的值相匹配。

# 用 Yup 验证模式

我们可以用`yup`添加验证模式。

为此，我们写道:

```
<template>
  <Form @submit="submit" :validation-schema="schema" v-slot="{ errors }">
    <Field name="email" as="input" />
    <span>{{ errors.email }}</span>
    <br />
    <Field name="password" as="input" type="password" />
    <span>{{ errors.password }}</span>
    <br />
    <button>Submit</button>
  </Form>
</template>
<script>
import { Field, Form } from "vee-validate";
import * as yup from "yup";
export default {
  components: {
    Field,
    Form,
  },
  data() {
    const schema = yup.object().shape({
      email: yup.string().required().email(),
      password: yup.string().required().min(8),
    });
    return {
      schema,
    };
  },
  methods: {
    submit() {},
  },
};
</script>
```

我们用`email`和`password`属性创建了`schema`对象，它们与`Field`组件上的`name`属性值相匹配。

我们调用`yup.object.shape`方法来创建带有`email`和`password`字段的模式，以便对每个字段进行验证。

# 结论

我们可以使用带有 Vee-Validate 的 Yup 库来验证我们的表单字段。

*详见*[***plain English . io***](https://plainenglish.io/)