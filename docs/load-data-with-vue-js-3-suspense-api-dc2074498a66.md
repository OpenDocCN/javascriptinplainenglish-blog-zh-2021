# 用 Vue.js 3 暂记 API 加载数据

> 原文：<https://javascript.plainenglish.io/load-data-with-vue-js-3-suspense-api-dc2074498a66?source=collection_archive---------10----------------------->

## 使用 Vue.js 3 暂记 API 处理异步承诺

![](img/18e99ce0b5e978ce3a8c647a1fe83c45.png)

Photo by [Blake Connally](https://unsplash.com/@blakeconnally?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue.js 3 捆绑了一些令人惊叹的功能。它附带的一个特性是悬念 API 组件边界。当您想要处理一些异步请求时，悬念 API 就派上了用场。

举个例子，我们从一个 API 端点获取一些数据，并希望在相关承诺得到解决时向客户端显示一些回退消息。我们可以利用悬念 API 来执行这样的任务。

悬念 API 使我们能够处理承诺，并在其他组件上显示后备内容，而不是在单个组件中本地显示。

## **为什么要悬疑 API**

*   加载时容易显示回退消息和内容。
*   可以帮助显示何时承诺已经解决并准备好呈现。
*   帮助控制各种视图部分。

## **在组件中设置暂记 API。**

创建一个组件，并将其命名为 movies.vue。在这个组件中，我们将有如下所示的代码片段。

movies.vue

此外，为了确保组件状态的反应性，我们必须导入 ***ref*** 。因此，从上面的代码片段来看，我们正在对端点进行异步 API 调用，以获取一些电影数据。

对于发出 HTTP 请求，您可以使用 ***fetch*** 或 ***Axios*** ，这取决于您的首选方法，但是对于我们的示例，我们将使用 fetch。

好了，我们现在得到了权力，现在我们希望悬念 API 显示应用程序内的回退消息。

在我们的 app.vue 文件中，我们将拥有如下面代码片段所示的代码。

app.vue

因此，我们正在导入我们的电影组件，并在它周围有一个悬念 API 组件边界。另外，记得从 vue 导入悬念 API，这样 vue 就不会抛出一些错误。

从上面的代码片段来看，我们必须在悬念 API 边界内创建模板。带有 ***#default*** 的初始模板组件是当承诺被解决并且一切都成功时将显示的组件。

带有 ***#fallback*** 的模板是当承诺尚未解决时将向用户显示的组件，并充当回退组件。现在，我们在 ***#fallback*** 模板中提供的消息将显示给用户，直到承诺得到解决。

当您希望在承诺完成时显示一条回退消息时，悬念 API 会很方便。

## **注**

悬疑 API 是 Vue.js 3 的一个新特性，还在实验中。强烈建议不要在生产环境中使用。

感谢您阅读本文，希望对您有所帮助。

## **资源**

Vue.js 文档

[https://v3.vuejs.org/guide/migration/suspense API . html #子更新](https://v3.vuejs.org/guide/migration/suspense.html#child-updates)

## **更读着**

[](/how-to-create-custom-error-pages-in-nuxt-js-3c8192bc0ae5) [## 如何在 Nuxt.js 中创建自定义错误页面

### 在 Nuxt.js 中创建自定义错误页面，用例子解释。

javascript.plainenglish.io](/how-to-create-custom-error-pages-in-nuxt-js-3c8192bc0ae5) [](/option-api-vs-composition-api-in-vue-js-a-definitive-guide-2a04a398b3ce) [## Vue.js 中的选项 API 与组合 API—权威指南

### 我们应该使用哪一个？逐步比较。

javascript.plainenglish.io](/option-api-vs-composition-api-in-vue-js-a-definitive-guide-2a04a398b3ce) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)