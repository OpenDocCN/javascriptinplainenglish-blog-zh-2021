# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—值匹配和长度验证

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-value-match-and-length-validation-27febff78b5d?source=collection_archive---------20----------------------->

![](img/8070831c082994c7d34a41d0ae3fb6a0.png)

Photo by [Paréj Richárd](https://unsplash.com/@prics?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 是

`is`规则让我们验证输入的值必须与给定值匹配。

匹配是由严格相等决定的。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="is:hello" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  methods: {
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
```

我们通过在冒号后设置要检查的文本来添加规则。

所以当我们输入`'hello'`时，这个字段是有效的。

否则，我们会看到显示一条错误消息。

此外，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" :rules="validations" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  data() {
    return {
      validations: { is: "hello" },
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

添加带有对象的规则。

# 不是

`is_not`规则让我们检查输入的值是否与给定的文本匹配。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="is_not:hello" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  methods: {
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
```

添加规则。

如果我们输入`hello`，那么我们会得到一个错误。

否则，该字段有效。

此外，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" :rules="validations" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  data() {
    return {
      validations: { is_not: "hello" },
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

做同样的事情。

# 长度

我们可以使用`length`规则来验证作为值输入的 iterable 具有给定的长度。

Iterables 包括字符串、数组或者任何可以用`Array.from`转换成数组的东西。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="length:5" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  methods: {
    onSubmit(values) {
      alert(JSON.stringify(values, null, 2));
    },
  },
};
</script>
```

添加验证。

此外，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" :rules="validations" />
    <span>{{ errors.field }}</span>
  </Form>
</template><script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "@vee-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  data() {
    return {
      validations: { length: 5 },
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

做同样的事情。

# 结论

我们可以使用 Vee-Validate 4 在 Vue 3 应用程序中验证各种输入值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)