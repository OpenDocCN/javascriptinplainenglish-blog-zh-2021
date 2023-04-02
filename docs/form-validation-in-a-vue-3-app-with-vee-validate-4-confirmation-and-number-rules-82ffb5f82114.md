# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—确认和编号规则

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-confirmation-and-number-rules-82ffb5f82114?source=collection_archive---------17----------------------->

![](img/c034e81eb0d345db312a7ce06ee8541e.png)

Photo by [Ines Štandeker](https://unsplash.com/@inesseni?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 在...之间

`between`规则让我们验证输入的数字是否在给定的范围内。

要使用它，我们可以写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="field" rules="between:1,10" />
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

我们将一个字符串传入到`rules`属性中，将规则添加到`Field`组件中。

同样，我们可以将一个对象传递到`rules` prop 中来添加规则:

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
      validations: { between: [1, 10] },
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

该范围的最小值和最大值在数组中。

最小值和最大值都是必需的。

# 确认的

`confirmed`规则验证接受验证的字段必须与另一个字段具有相同的值。

要使用它，我们可以写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="password" type="password" /> <Field name="confirmation" type="password" rules="confirmed:@password" />
    <span>{{ errors.confirmation }}</span>
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

将`rules`属性设置为`confirmed:@password`，以便 Vee-Validate 检查`confirmation`字段是否与`password`字段具有相同的值。

`Field`组件必须都在`Form`组件内。

# 数字

`digits`规则检查输入的值必须是数字并且具有指定的位数。

例如，我们可以写:

```
<template>
  <Form @submit="submit" v-slot="{ errors }">
    <Field name="field" rules="digits:3" />
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

我们验证输入值必须正好有 3 位数字和`'digits:3'`字符串。

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
      validations: { digits: 3 },
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

我们可以使用 Vee-Validate 4 在我们的 Vue 3 应用程序中添加各种表单验证规则。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)