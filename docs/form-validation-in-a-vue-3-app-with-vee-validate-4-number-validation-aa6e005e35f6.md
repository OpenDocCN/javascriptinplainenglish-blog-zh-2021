# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—数字验证

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-number-validation-aa6e005e35f6?source=collection_archive---------20----------------------->

![](img/16bbc13f8af0d52f19e9199df425ffbd.png)

Photo by [Trnava University](https://unsplash.com/@trnavskauni?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 部

`min`规则规定输入值的长度不能小于指定长度。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="min:3" />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
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

我们将`min`值设置为 3，以设置我们允许输入值的最小长度。

此外，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" :rules="validations" />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
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
      validations: { min: 3 },
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

添加相同的规则。

# 最小值

`min_value`规则让我们指定我们允许作为输入值的最小值。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="min_value:5" />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
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

如果我们输入一个小于 5 的数字，我们会看到一个错误。

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
      validations: { min_value: 5 },
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

添加相同的规则。

# 数字的

`numeric`规则让我们验证输入的值是一个数字。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="numeric" />
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
      validations: { numeric: true },
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

添加相同的规则。

# 结论

我们可以使用 Vee-Validate 4 来验证 Vue 3 应用程序中的数字输入。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)