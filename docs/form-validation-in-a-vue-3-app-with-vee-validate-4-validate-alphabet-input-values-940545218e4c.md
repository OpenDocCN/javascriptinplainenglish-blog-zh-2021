# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—验证字母输入值

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-validate-alphabet-input-values-940545218e4c?source=collection_archive---------12----------------------->

![](img/64d8ccfb1922008d38199516fed85c1a.png)

Photo by [Tyler Nix](https://unsplash.com/@jtylernix?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 阿尔法破折号

`alpha_dash`规则验证输入的值可能包含字母字符、数字、破折号或下划线。

为了使用它，我们写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="field" rules="alpha_dash" />
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

添加规则。

此外，我们还可以这样写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
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
      validations: { alpha_dash: true },
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

# 阿尔法数字

`alpha_num`规则让我们验证输入的值是否包含字母字符或数字。

例如，我们可以写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="field" rules="alpha_num" />
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

此外，我们可以写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
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
      validations: { alpha_num: true },
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

将验证规则作为对象传递给`rules`道具。

# alpha_spaces

`alpha_spaces`规则验证输入的值是否包含字母字符或空格。

为了使用它，我们写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="field" rules="alpha_spaces" />
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

此外，我们可以向`rules`道具传递一个对象来添加规则:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
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
      validations: { alpha_spaces: true },
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

# 结论

我们可以通过 Vee-Validate 4 在 Vue 3 应用中轻松验证字母输入值。