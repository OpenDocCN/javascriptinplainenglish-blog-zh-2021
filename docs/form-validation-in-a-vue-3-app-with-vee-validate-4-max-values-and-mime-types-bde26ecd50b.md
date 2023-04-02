# 使用 Vee-Validate 4 在 Vue 3 应用程序中进行表单验证—最大值和 MIME 类型

> 原文：<https://javascript.plainenglish.io/form-validation-in-a-vue-3-app-with-vee-validate-4-max-values-and-mime-types-bde26ecd50b?source=collection_archive---------18----------------------->

![](img/d6b9a33b22073c8a052d0403649e02bf.png)

Photo by [Eka Bima Sitorus](https://unsplash.com/@ebsitorus?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

表单验证是任何应用程序的重要组成部分。

在本文中，我们将了解如何在我们的 Vue 3 应用程序中使用 Vee-Validate 4 进行表单验证。

# 最大

我们可以使用`max`规则来确保输入的值不超过指定的长度。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="max:10" />
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

我们在冒号后面加上最大长度。

因此，如果我们输入的内容超过 10 个字符，就会显示错误。

此外，我们可以将一个对象传递到`rules`属性中来添加相同的规则:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" :rules="validations" />
    <span>{{ errors.field }}</span>
  </Form>
</template>
<script>
import { Form, Field, defineRule } from "vee-validate";
import * as rules from "[@vee](http://twitter.com/vee)-validate/rules";Object.keys(rules).forEach((rule) => {
  defineRule(rule, rules[rule]);
});export default {
  components: {
    Form,
    Field,
  },
  data() {
    return {
      validations: { max: 10 },
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

# 最大值

`max_value`道具让我们确保输入的值不超过给定的数字。

例如，我们可以这样使用它:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" rules="max_value:10" />
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

我们在冒号后添加要检查的最大数量。

如果我们输入一个大于 10 的数字，我们会看到一个错误显示。

同样，我们可以使用一个对象来添加规则:

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
      validations: { max_value: 10 },
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

# 哑剧

我们可以使用`mimes`规则来检查所选文件是否具有给定的 MIME 类型。

例如，我们可以写:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" type="file" rules="mimes:image/jpeg" />
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

将规则添加到文件输入中。

我们还可以添加带有对象的规则:

```
<template>
  <Form @submit="onSubmit" v-slot="{ errors }">
    <Field name="field" type="file" :rules="validations" />
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
      validations: { mimes: ["image/jpeg"] },
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

我们将允许的 MIME 类型放在`mimes`数组属性中。

# 结论

我们可以使用 Vee-Validate 4 在 Vue 3 应用程序中验证文件的 MIME 类型、输入的最大长度和输入的最大值。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)