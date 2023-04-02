# 使用 Vue.js 和 VeeValidate 进行表单验证

> 原文：<https://javascript.plainenglish.io/form-validation-using-vue-js-veevalidate-31a2f56b8d3f?source=collection_archive---------6----------------------->

![](img/9d18148a90f327f659d342de35fffd14.png)

Photo by [Nick Morrison](https://unsplash.com/@nickmorrison?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 框架有很多插件，可以用来实现前端表单验证。其中一个就是 **VeeValidate** 。VeeValidate 可用于构建高级验证。这是因为它为不同类型的字段提供了内置的验证规则。本文将向您展示如何使用VeeValidate 和 **Vue** 来实现表单验证。

**步骤 1:** 创建一个名为 RegisterApp 的新 Vue 项目。点击阅读 Vue 项目设置[。](https://cli.vuejs.org/guide/creating-a-project.html)

```
vue create RegisterApp
```

**步骤 2:** 将 *VeeValidate* 安装到 *RegisterApp 中。* [阅读此处了解 VeeValidate 设置](https://vee-validate.logaretm.com/v3/overview.html#installation)

```
cd RegisterApp
npm install vee-validate --save
```

**第三步:**在 *main.js* 文件中使用***vue . component()***函数全局注册 *ValidationProvider* 。

```
import { ValidationProvider } from 'vee-validate';
import { ValidationObserver } from 'vee-validate';Vue.component('ValidationProvider', ValidationProvider);
```

第四步:接下来安装所有可用的规则。[阅读此处查找可用角色](https://vee-validate.logaretm.com/v3/guide/rules.html#installing-all-rules)

```
import { ValidationProvider } from 'vee-validate/dist/vee-validate.full.esm';
```

最终的 *main.js* 文件必须是这样的。

```
import Vue from 'vue'
import App from './App.vue'
import { ValidationObserver } from 'vee-validate'
import { ValidationProvider } from 'vee-validate/dist/vee-validate.full.esm';Vue.component('ValidationProvider', ValidationProvider);
Vue.config.productionTip = falsenew Vue({
  render: *h* => h(App),
}).$mount('#app')
```

**第五步:**在 *components/* 文件夹下创建一个名为***register form . vue .***的组件

```
<template>
 <div>
 <h2>VeeValidate Form</h2>

</div></template><script>
  export default {
   data: () => (),
  methods: {

  }
}}
</script> 
```

**第六步: *<脚本></脚本>* 部分中的**创建*名*、*姓*、*邮箱*和*密码*作为数据属性。

```
<script>
  export default {
   data: () => ({

       name: '',
       email: '',
       password: '',

  }),
  methods: {

  }
}}
</script>
```

**步骤 7:** 在 *<模板></模板>* 部分创建一个表单，并将其包装在 *ValidationObserver 中。*

```
<template>
 <div>
 <h2>VeeValidate Form</h2>
 <ValidationObserver *v-slot*="{ handleSubmit }">
    <form @*submit*.*prevent*="handleSubmit(onSubmit)"> </form>
</ValidationObserver></div></template>
```

**步骤 8:** 为*名字*、*姓氏*、*电子邮件*和*密码创建输入。*用***validation provider***组件包装每个输入，该组件充当您的字段 ***的验证器。***

```
<template>
 <div>
 <h2>VeeValidate Form</h2>
 <ValidationObserver *v-slot*="{ handleSubmit }">
 <form @*submit*.*prevent*="handleSubmit(onSubmit)"><ValidateProvider *name*="firstname" *rules*="required|alpha" *v-slot*="{ errors }">
<div>
  <label>Firstname</label>
  <input *type*="text" *v-model*="firstname">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="lastname" *rules*="required|alpha" *v-slot*="{ errors }">
<div>
  <label>Lastname</label>
  <input *type*="text" *v-model*="lastname">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="email" *rules*="required|email" *v-slot*="{ errors }">
<div>
  <label>Email</label>
  <input *type*="email" *v-model*="email">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="password" *rules*="required" *v-slot*="{ errors }">
<div>
  <label>Password</label>
  <input *type*="password" *v-model*="password">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><input *type*="submit" *text*="Submit"></form></ValidationObserver>
</div></template>
```

最终的***register form . vue***应该是这样的。

```
<template>
 <div>
 <h2>VeeValidate Form</h2>
 <ValidationObserver *v-slot*="{ handleSubmit }">
 <form @*submit*.*prevent*="handleSubmit(onSubmit)"><ValidateProvider *name*="firstname" *rules*="required|alpha" *v-slot*="{ errors }">
<div>
  <label>Firstname</label>
  <input *type*="text" *v-model*="formData.firstname">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="lastname" *rules*="required|alpha" *v-slot*="{ errors }">
<div>
  <label>Lastname</label>
  <input *type*="text" *v-model*="formData.lastname">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="email" *rules*="required|email" *v-slot*="{ errors }">
<div>
  <label>Email</label>
  <input *type*="text" *v-model*="formData.email">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><ValidateProvider *name*="password" *rules*="required|alpha" *v-slot*="{ errors }">
<div>
  <label>Password</label>
  <input *type*="text" *v-model*="formData.password">
  <span>{{ errors[0] }}</span>
</div>
</ValidationProvider><input *type*="submit" *text*="Submit"></form></ValidationObserver>
</div></template><script>
  export default {
   data: () => ({

       name: '',
       email: '',
       password: '',

  }),
  methods: {
    onSubmit(){
      console.log(*this*.formData);
  }
}}
</script>
```

**第九步:**将 *RegisterForm.vue* 导入到 *App.vue* 中。

```
<template>
  <div *id*="app">
  <RegisterForm />
  </div>
</template><script>
import RegisterForm from "./components/RegisterForm";export default {
  name: "App",
  components: {
     RegisterForm
  }
}
</script><style></style>
```

运行应用程序

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容看*[***plain English . io***](http://plainenglish.io/)