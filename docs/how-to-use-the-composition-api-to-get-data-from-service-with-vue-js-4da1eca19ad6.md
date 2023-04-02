# 如何使用组合 API 通过 Vue.js 从服务中获取数据

> 原文：<https://javascript.plainenglish.io/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6?source=collection_archive---------8----------------------->

## 通过使用组合 API 而不是选项 API，可以使服务结构更加可用。

![](img/dba0e5a893f45d46fc6d1d18cf78a461.png)

Photo by [Jan Antonin Kolar](https://unsplash.com/@jankolar?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

今天我感兴趣的是 Vue.js 2 和 Vue.js 3 的一个最美的区别。在 Vue.js 2 中，曾经使用过，甚至还在使用 Options API，现在在 Vue.js 3 中，我们面对的是 Composition API 的概念。

简要解释为什么做出这样的改变；

*   Vue.js 2 让我们不得不在一个地方使用反应变量(数据)、方法和计算值(computed)。
*   没有简单的解决方案来解构组件之间的公共逻辑。

Mixin 被用来解决这个问题，但是它们相当复杂。随着 mixin 使用的增加，我们在组件中做出的定义也是混杂的。

由于这些原因，在 Vue.js 3 中提出了一个不同的概念。当然，它也有缺点。但是它使我们的代码可重用，它的可理解性更简单。

让我们从慢到组合 API 概念。

首先，`setup()`这个方法是为我们使用组合 API 而创建的。

> 一旦它们`props`被解析，在组件被创建之前执行的组件选项。它充当组合 API 的入口点。

其中重要的一点是，你不应该在`setup()`中使用关键词`this`。因为`setup`是在数据、计算或方法被解析之前被调用的。

让我告诉你我举的例子。我正在从 Vue 自己网站上的服务中提取数据。他使用的数据是用 Options API 编写的。我想把它和复合 API 一起使用。

正如你在我准备的例子中看到的，我在`data()`中创建了`isStatus`属性。稍后我会用它来显示数据。

当你设置你正在使用的 IDE 时，它会给你一个`setup()`建议，它会按照它应该的那样设置。

我想解释一下我用的第一个概念`setup()`和类似的概念。

我用`ref([])`创建了我使用的数据

在使用`ref`之前，我们需要导入包。

`import {ref} from "vue"`

*   **ref:** 我们用它来使一个特征反应。
*   **反应性:**将稳定对象转化为反应性对象。
*   **isRef:** 我们用它来检查一个特性是否是反应性的。
*   **toRefs:** 允许我们把一个反应性对象的属性作为反应性属性。

首先，我必须使用`axios`从服务中获取数据。Axios 是一个 javascript 库，允许在客户端应用程序中轻松进行 HTTP 调用。我们用 NPM 安装`axios`包。

`npm install vue-axios`

`npm i vue-axios`

之后，我们需要在`.vue`导入文件。

`import axios from "axios"`

这是我获取数据的地方。

`axios.get("url")`

我处理数据的地方；

`.then((res)=>{ data.value = res.data.bpi})`

我可以通过调用`data.value`来使用我创建的`data`。

`res.data.bpi`这部分是关于我获取数据的 JSON 格式。JSON 中使用了`bpi`，我调用`data.bpi`是因为我想访问那里的数据。

在`setup()`里面我们需要使用`return.`作为回报，我添加了`data.`

在这些阶段之后，我将数据从服务获取到数据中。

在`methods:{}`中，我创建了`control()`一个函数。我将使用它来获取或关闭数据。

第一个`isStatus`值为真，为真时数据不显示。如果值为假，数据显示。

我使用 for 循环来使用模板中的数据。

`v-for="datas in data" :key="datas.description"`

我已经准备好这样使用数据了。我们需要确定密钥。

您可以根据传入的 JSON 格式对将要使用的数据进行格式化。

我的 **HelloWorld.vue** 、 **package.json** 和 **StackBlitz** 文件；

[](/how-to-use-angulars-attribute-directives-in-your-class-hierarchy-d3a1d0adac32) [## 如何在类层次结构中使用 Angular 的属性指令

### 使用 Angular CLI 构建属性指令

javascript.plainenglish.io](/how-to-use-angulars-attribute-directives-in-your-class-hierarchy-d3a1d0adac32) [](/chart-and-calendar-design-in-flip-card-using-angular-nebular-db0ffd434d5b) [## 使用角状星云在翻转卡中设计图表和日历

### 在活动卡片上创建一个快速、友好的图表和日历。

javascript.plainenglish.io](/chart-and-calendar-design-in-flip-card-using-angular-nebular-db0ffd434d5b) [](/how-to-create-marker-and-marker-cluster-with-leaflet-map-95e92216c391) [## 如何使用传单地图创建标记和标记簇

### 在活页地图架构中创建标记和图层，然后对标记进行聚类的方法。

javascript.plainenglish.io](/how-to-create-marker-and-marker-cluster-with-leaflet-map-95e92216c391) [](https://bestte.medium.com/today-im-going-to-share-the-home-screen-i-designed-with-flutter-bf95029c76e4) [## 颤振登录和主页设计

### 学习使用导航器传送另一页。按下并使用圆形按钮，输入说明

bestte.medium.com](https://bestte.medium.com/today-im-going-to-share-the-home-screen-i-designed-with-flutter-bf95029c76e4) [](/create-a-card-design-with-the-free-vue-js-template-now-ui-kit-5676a738e518) [## 使用免费的 Vue.js 模板创建卡片设计

### 使用免费主题可能是开发设计和学习的最佳方式之一。

javascript.plainenglish.io](/create-a-card-design-with-the-free-vue-js-template-now-ui-kit-5676a738e518) [](/how-to-use-angular-component-styles-with-special-selectors-dc877514372c) [## 如何将角度组件样式与特殊选择器一起使用

### 在具有独立样式文件的组件的基础上，将样式添加到您的 Angular 应用程序有助于您创建一个更…

javascript.plainenglish.io](/how-to-use-angular-component-styles-with-special-selectors-dc877514372c) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)