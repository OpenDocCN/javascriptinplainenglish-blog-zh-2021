# StackOverflow 上关于 Vue.js 3 的 4 个排名最高的查询

> 原文：<https://javascript.plainenglish.io/4-top-rated-queries-about-vue-js-3-on-stackoverflow-90beaff3b285?source=collection_archive---------5----------------------->

## 回答 Vue.js 3 上排名最高的 4 个问题。

![](img/38d7582ba18cde36dac42ed6ed4e914f.png)

Photo by [Nick Fewings](https://unsplash.com/@jannerboy62?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

StackOverflow 作为程序员使用的平台为大多数公众所知。但是今天它不仅仅包括软件世界。我的意思是，我们可以说它存在于我们生活的每一部分。

在软件世界里，它每天被很多人点击很多次。使用区域；有时创建一个项目，有时解决语法错误，有时获取一段代码并退出，等等。

今天和大家分享一下 Vue.js 上投票最多的问题。

开始吧！

# 问题 1

## [**参考 vs Vue 3 中的无功？**](https://stackoverflow.com/questions/61452458/ref-vs-reactive-in-vue-3)

投票 8426 万次。

我们可以这样解释这个问题的答案。

`ref`用于反应变量如原始值(布尔值、数字、字符串、符号、空值等。).

我们定义为`reactive`的变量必须定义为对象类型。对于`reactive`附加信息，我们可以通过在已定义对象的属性中添加`toRefs`将其转换为`ref`类型。

堆栈溢出中这个问题的最佳答案是:

> ***要点***
> 
> `*reactive()*` *只取对象，* ***不取*** *JS 原语(String，Boolean，Number，BigInt，Symbol，null，undefined)*
> 
> `*ref()*` *正在幕后调用*`*reactive()*`
> 
> **由于* `*reactive()*` *对对象有效而* `*ref()*` *调用* `*reactive()*` *，对象对两者都有效**
> 
> **但是，* `*ref()*` *有一个* `*.value*` *属性用于重新分配，* `*reactive()*` *没有这个属性，因此不能重新分配**
> 
> *`***ref()***` ***当……****
> 
> **这是一个原语(例如*`*'string'*`*`*true*`*`*23*`*等)****
> 
> ***是一个你需要稍后重新分配的对象(比如一个数组—* [*更多信息请点击*](https://github.com/vuejs/docs-next/issues/801#issuecomment-757587022) *)***
> 
> **`*reactive()*` *当……***
> 
> ***是一个你不需要重新分配的对象，你想避免* `*ref()*`的开销**
> 
> *****总结*****
> 
> **`*ref()*` *看起来不错，因为它支持所有的对象类型，并允许用* `*.value*` *重新分配。* `*ref()*` *是一个很好的起点，但是随着你习惯了这个 API，知道* `*reactive()*` *开销更少，你可能会发现它更符合你的需求。***

**`reactive()`**

```
**const person = reactive({
  name: 'Albert',
  isNinja: true,
});**
```

**`ref()`**

```
**const name = ref('Albert');
const isNinja = ref(true);**
```

# **问题 2**

## **[**承诺和可观察到的区别？**](https://stackoverflow.com/questions/37364973/what-is-the-difference-between-promises-and-observables)**

**有 57，168，000 次投票。**

***我想把 Bootstrap 5 和 Vue 3 一起用。由于 Bootstrap 5 使用 vanilla JS(没有 JQuery)，我可以在 Vue 3 项目中直接使用 Bootstrap 5 吗(不使用 Bootstrap-Vue)？有人能指导我如何使用 Bootstrap 5 和 Vue 3 吗？***

**堆栈溢出中这个问题的最佳答案是:**

****Bootstrap 5 不再需要 jQuery，因此它更容易与 Vue** 一起使用，并且不再需要像`bootstrap-vue`这样的库。**

**使用 npm install 或将其添加到`package.json`中，像安装 Vue 项目中的任何其他 JS 模块一样安装 bootstrap。**

```
**npm install --save bootstrap**
```

**接下来，将引导 CSS 和 JS 组件添加到 Vue 项目入口点(即:`src/main.js`):**

```
**import "bootstrap/dist/css/bootstrap.min.css"
import "bootstrap"**
```

**然后，使用引导组件最简单的方法是通过`data-bs-`属性。例如，以下是引导折叠组件:**

```
**<button 
  class="btn btn-primary" 
  data-bs-target="#collapseTarget" 
  data-bs-toggle="collapse">
  Bootstrap collapse
</button>
<div class="collapse py-2" id="collapseTarget">
  This is the toggle-able content!
</div>**
```

# **问题 3**

## **[**Vue.js 3 事件总线**](https://stackoverflow.com/questions/63471824/vue-js-3-event-bus)**

**投票 4126000 次**

> **如何在 Vue 3 中创建事件总线？**
> 
> **在 Vue 2 中，它是:**

```
**export const bus = new Vue();bus.$on(...)
bus.$emit(...)**
```

> **在 Vue 3 中，`Vue`不再是构造函数，`Vue.createApp({});`返回一个没有`$on`和`$emit`方法的对象。**

**堆栈溢出中这个问题的最佳答案是:**

**正如官方[文档](https://v3.vuejs.org/guide/migration/events-api.html#migration-strategy)中所建议的，你可以使用 [mitt](https://github.com/developit/mitt) 库在组件之间分派事件，假设我们有一个侧边栏和`header`，其中包含一个关闭/打开侧边栏的按钮，我们需要这个按钮来切换侧边栏组件中的一些属性:**

**在 main.js 中导入该库，创建该发射器的一个实例，并将其定义为一个全局属性:**

## ****安装:****

```
**npm install --save mitt**
```

## ****用法:****

```
**import { createApp } from 'vue'
import App from './App.vue'
import mitt from 'mitt';
const emitter = mitt();
const app = createApp(App);
app.config.globalProperties.emitter = emitter;
app.mount('#app');**
```

**在头中发出带有一些有效负载的`toggle-sidebar`事件。**

**对于那些使用组合 API 的人，他们可以如下使用`emitter`:**

**创建一个文件 src/composables/useEmitter.js，如下所示:**

```
**import { getCurrentInstance } from 'vue'export default function useEmitter() {
    const internalInstance = getCurrentInstance(); 
    const emitter = internalInstance.appContext.config.globalProperties.emitter; return emitter;
}**
```

**从那以后，你可以像使用`useRouter`一样使用`useEmitter`:**

```
**import useEmitter from '@/composables/useEmitter'export default {
  setup() {
    const emitter = useEmitter()
    ...
  }
  ...
}**
```

# **问题 4**

## **[**Vue 3 Composition API——如何获取挂载组件的组件元素($ El)**](https://stackoverflow.com/questions/61600078/vue-3-composition-api-how-to-get-the-component-element-el-on-which-componen)？**

**投票数是 22，24k 次**

> **想用`onMounted`发起第三方库。为此，我需要组件元素作为其上下文。在 Vue 2 中，我会用`this.$el`得到它，但不确定如何用复合函数来得到它。`setup`有两个参数，但它们都不包含元素。**

```
**setup(props, context) {
    onMounted(() => {
        interact($el)
            .resizable();
    })
}**
```

**StackOverflow 中这个问题的最佳答案:**

**在 Vue 3 中，组件不再仅限于一个根元素。含蓄地说，这意味着您不再拥有`$el`。你必须使用`ref`来与你的模板中的任何元素交互。**

**正如@AndrewSee 在评论中指出的，当使用渲染函数(不是模板)时，可以在`createElement`选项中指定所需的`ref`:**

```
**render: function (createElement) {
  return createElement('div', { ref: 'root' })
}
// or, in short form:
render: h => h('div', { ref: 'root' })** 
```

**阅读问题和检查答案会给你很多信息。因此，要经常阅读和复习。**

**感谢您的更多访问 [StackOverflow。](https://stackoverflow.com/questions/tagged/vuejs3?sort=MostVotes&edited=true)**

**[](https://bestte.medium.com/membership) [## 通过我的推荐链接加入 Medium—Beste

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

bestte.medium.com](https://bestte.medium.com/membership) [](/5-top-rated-q-a-for-angular-on-stack-overflow-bed610bf1c50) [## 5 堆栈上角溢出的顶级问答

### “这个项目从堆栈溢出开始”是开发人员如何开始她的故事。

javascript.plainenglish.io](/5-top-rated-q-a-for-angular-on-stack-overflow-bed610bf1c50) [](/how-to-work-with-the-angular-nebular-ui-library-and-use-a-simple-splash-screen-3dd0d1790478) [## 如何使用 Angular Nebular UI 库并使用简单的闪屏

### 闪屏在某些情况下是必要的，所以我想用一种非常简单的方式来展示它，我将谈谈…

javascript.plainenglish.io](/how-to-work-with-the-angular-nebular-ui-library-and-use-a-simple-splash-screen-3dd0d1790478) [](/how-to-use-sass-and-enjoy-css-with-dynamic-structure-900ea2adddf7) [## 如何使用 Sass，享受动态结构的 CSS

### 由于 CSS 是一个静态结构，我们必须不断重复代码。我们给 CSS 代码带来了动态结构…

javascript.plainenglish.io](/how-to-use-sass-and-enjoy-css-with-dynamic-structure-900ea2adddf7) [](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) [## 如何使用组合 API 通过 Vue.js 从服务中获取数据

### 通过使用组合 API 而不是选项 API，可以使服务结构更加可用。

javascript.plainenglish.io](/how-to-use-the-composition-api-to-get-data-from-service-with-vue-js-4da1eca19ad6) 

*更多内容看* [*说白了。在这里注册我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。***