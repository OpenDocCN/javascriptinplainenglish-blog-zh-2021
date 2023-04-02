# 在 Vue 中生成 API 驱动的表单

> 原文：<https://javascript.plainenglish.io/generate-api-driven-forms-in-vue-a2a9cb263bd2?source=collection_archive---------6----------------------->

![](img/267458e6ba82b0613da31ba50f004613.png)

cover image

我最近参与了一个项目，该项目要求 SuperAdmin 用户检查客户在入职过程中出现的注册错误。受影响的字段由内部系统标记，并作为 JSON 有效载荷返回给前端应用程序。我们有 100 多个表单输入字段可能会受到影响。

考虑到这一点，我从一开始就知道生成表单的典型方法不足以解决这个问题。

在本文中，我将向您展示从 JSON 有效负载动态生成表单输入的方法。

你可以在这里 查看 React.js 版本[](/generating-api-driven-form-in-reactjs-d07ed54ca3f2)

## **沙箱**

**我们在一个 [Codesandbox](https://codesandbox.io/s/dynamic-form-vuejs-ilsn9?file=/src/App.vue:0-1004) 中完成了这个项目，你可以派生它来运行代码。**

# **Vue 中的表单处理**

**在开始之前，我们必须了解 Vue 中当前是如何处理表单的。**

**Vue.js 目前使用`v-model`指令在表单元素上创建双向数据绑定，并根据输入类型和用户输入事件自动更新数据。**

**Handling form in Vue**

# **动态生成表单**

**现在我们完全理解了 Vue.js 是如何处理表单的。我们可以直接修改`App.vue`来动态地从 JSON 响应中生成表单输入元素。**

## ****第一步****

**在`src`目录中创建一个`data.json`来模拟我们从一个端点得到的响应。**

**JSON response mock data**

## ****第二步****

**记住 JSON 文件的结构，我们可以编辑`App.vue`,如下所示:**

**Dynamic Form**

**上述代码执行这些任务:**

*   **从 JSON 文件导入`response`。**
*   **传递`response`并将`formData`初始化为组件的数据选项中的空对象。**
*   **通过将**字段名**和**值**映射为 ***键值对*** ，使用 Vue.js `created`生命周期实例动态填充`formData`空对象。这样，如果端点带有初始值，它将被填充到输入字段中。**
*   **通过 form 元素映射显示**表单标签**、**输入类型**、 **v-model** 指令，以及对应的值。**

**现在，我们可以测试我们的表单并相应地提交它。**

**您可以在这个沙盒上查看完整的代码。**

**Dynamic Form**

# **结论**

**这篇文章讨论了如何动态地生成表单，而不会因为外部库而使应用程序膨胀。它也是可扩展的(以适应其他表单元素)，可维护的，并且是一种更简洁的方法。**

****参考:****

*   **[vue . js 入门](https://vuejs.org/v2/guide/)**
*   **[处理 Vue.js 中的表单](https://vuejs.org/v2/guide/forms.html)**
*   **[vue . js 中的生命周期实例](https://vuejs.org/v2/guide/instance.html)**

***更多内容请看*[***plain English . io***](https://plainenglish.io/)**