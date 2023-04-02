# 2022 年应该用 Vue 3 还是 Vue 2？

> 原文：<https://javascript.plainenglish.io/should-i-use-vue-3-or-vue-2-in-2022-ba09c8059233?source=collection_archive---------2----------------------->

![](img/d2d711ceb62274d9c15465bfd325cb3c.png)

Already installed Vue CLI? Don’t worry! The same CLI offers both Vue 2 as well as Vue 3 support :)

长话短说，这里有一个快速检查。

# 何时使用 Vue 3，何时不使用

1.  如果需要 IE11 支持:**不要用 Vue 3，支持还没到|** 开个玩笑——微软终于扔掉了 Internet Explorer，所以除非你有一些遗留客户端，否则不需要支持。
2.  如果您正在使用 Vue 2: **进行一个非常大且复杂的现有项目，您可能不希望迁移到 Vue 3** ，这取决于您的代码，迁移时间和性能收益可能不值得
3.  如果你有一些优化后的性能问题: **Vue 3 是从头开始写的，比 Vue 2 提供更好的性能**
4.  如果你需要更好的 TypeScript 支持:**用 Vue 3，比以前好多了！**
5.  如果你的依赖支持 Vue 3: **使用 Vue 3** | Vue 3 是新的，并不是所有的库都支持它。

**最后，我鼓励任何不需要 IE11 支持(也见上面第 1 点的笑话)和不需要使用不支持 Vue 3 的依赖项的新项目使用 Vue 3。**

![](img/998aa0df85fbfaf342515b9e323c6e0a.png)

如果你认为你得到了你想要的，**祝贺你！**但是你难道不想知道更多关于 Vue 3 的信息吗？

> 如果你有兴趣学习 Vue JS 或者在 Vue JS 中磨砺自己的技能，可以看看我新推出的课程 [Vue 3 要领](https://www.udemy.com/course/vue-3-essentials/?referralCode=E6D2FDE2B8B06C1991F1)和 [Vue JS 完整课程+指南](https://www.udemy.com/course/vuejs-complete-course-plus-guide/?referralCode=93BDA4A1FE3F73C37CD2)。

代号为“海贼王”的 Vue 3.0 于 2 年前公布，2020 年 9 月正式发布。Vue 3 完全重写了框架。它带来了更好的性能、更好的树抖动、更小的尺寸、改进的 TypeScript 支持，以及一些用于开发大型企业软件的革命性新特性。

# 2022 年该学 Vue 2 还是 Vue 3？

Vue 2 中的大部分语法和做法在 Vue 3 中保持不变，所以**如果你学习 Vue 2 或 Vue 3** 应该不会有太大的区别。大多数图书馆现在支持 Vue 3，我们也期待 Vue 3 的兼容版本很快推出。然而，并不是所有的库都与 Vue 3 兼容，所以**如果你想安全一点，并且能够承受没有 Vue 3 的性能和 API 改进，那么你最好学习并使用 Vue 2** 。

Vue 3 基本上是 Vue 2 的增压版本。Vue 3 甚至更快更轻，带有改进的 TypeScript 支持，并且有一些很棒的新功能。框架本身已经从头开始重新编写，但是 API(开发人员如何使用它)几乎保持不变。这有多棒？！

把升级到 Vue 3 想象成换成一部稍新的相同品牌的手机，比如从 iPhone X 换成 iPhone 11 Pro。感觉棒极了，你得到了很大的改进，但是用户界面保持不变。在这两种情况下，您都有一部出色的手机！同样的**在 Vue.js 中，当你转到 Vue 3 时，你将能够用你的新框架做更多的事情，但是你以前能做的一切都将继续发挥作用**。

为了实现这一转变，Vue 团队发布了深入的指南，并将发布一个迁移工具来解析您的应用程序并指导您完成升级。

所以不要害怕 Vue 3，不要犹豫学习和使用 Vue 2。事实上，Vue 3 与 Vue 2 共享大多数概念。

# Vue 3 中激动人心的新功能

正如您所料，除了出色的性能改进和更好的摇树功能外，Vue 3 还带来了许多令人兴奋的新功能。谢天谢地，Vue 团队主要引入了对当前 API 的补充和改进，而不是重大的改变，所以已经知道 Vue 2 的人应该很快对新语法感到满意。

以下是新功能的列表:

> 成分原料药
> 
> 全局安装/配置 API 更改
> 
> 碎片
> 
> 焦虑
> 
> 多个 v 型
> 
> 门户|传送
> 
> 新的自定义指令应用编程接口

让我们从大多数人可能听说过的 API 开始…

# 成分原料药

Composition API 是 Vue 下一个主要版本中最常讨论和使用的语法。这是一种完全**可选的**逻辑重用和代码组织方法。值得注意的是，您仍然可以使用所有可选的 Vue 2 Options APIs。

目前，我们使用所谓的选项 API 构建组件。为了给 Vue 组件添加逻辑，我们填充了(选项)属性，如`data`、`methods`、`computed`等。这种方法最大的缺点是它本身不是一个工作的 JavaScript 代码。您需要确切了解模板中哪些属性是可访问的，以及`this`关键字的行为。在幕后，Vue 编译器需要将这些属性转换成工作代码。

Composition API 旨在通过将当前可通过组件属性获得的机制公开为 JavaScript 函数来解决这个问题。Vue 核心团队将 Composition API 描述为*“一组允许灵活组合组件逻辑的基于函数的附加 API”。*用 Composition API 编写的代码可读性更强，幕后没有魔法，更容易阅读和学习。

让我们看一个非常简单的组件示例，它使用新的 Composition API 来理解它是如何工作的。

```
<template>
  <button @click="increment">
    Count is: {{ count }}, double is {{ double }}, click to increment.
  </button>
</template><script>
import { ref, computed, onMounted } from 'vue'export default {
  setup() {
    const count = ref(0)
    const double = computed(() => count.value * 2) function increment() {
      count.value++
    } onMounted(() => console.log('component mounted!')) return {
      count,
      double,
      increment
    }
  }
}
</script>
```

现在让我们把这段代码分解成几部分，以了解发生了什么

```
import { ref, computed, onMounted } from 'vue'
```

正如我之前提到的，Composition API 将组件属性公开为函数，所以第一步是导入我们需要的函数。在我们的例子中，我们需要用`ref`创建反应性引用，用`computed`计算属性，用`onMounted`访问安装的生命周期钩子。

现在你大概在想这个神秘的`setup`方法是什么吧？

```
export default {
  setup() {
```

简言之，它只是一个向模板返回属性和函数的函数。就这样。我们在这里声明所有的反应属性、计算属性、观察器和生命周期钩子，然后返回它们，以便它们可以在模板中使用。

我们没有从`setup`功能中返回的内容在模板中将不可用。

```
const count = ref(0)
```

根据以上所述，我们用`ref`功能来声明一个叫做`count`的反应性属性。它可以包装任何图元或对象，并返回其被动引用。传递的元素的值将保留在创建的引用的`value`属性中。例如，如果您想访问`count`引用的值，您需要显式地请求`count.value`。

```
const double = computed(() => count.value * 2)function increment() {
  count.value++
}
```

……这正是我们在声明计算属性`double`和`increment`函数时所做的。

```
onMounted(() => console.log('component mounted!'))
```

有了`onMounted`钩子，当组件被安装时，我们会记录一些消息，只是为了告诉你你可以。

```
return {
  count,
  double,
  increment
}
```

最后，我们用`increment`方法返回`count`和`double`属性，使它们在模板中可用。

```
<template>
  <button @click="increment">
    Count is: {{ count }}, double is {{ double }}. Click to increment.
  </button>
</template>
```

瞧。现在我们可以像通过旧的 Options API 声明属性和函数一样，在模板中访问`setup`方法返回的属性和函数。

这是一个简单的例子，用 Options API 也很容易实现。新的组合 API 的真正好处不仅仅是以不同的方式编码，当涉及到重用我们的代码/逻辑时，这些好处就会显现出来。

**代码复用与组合 API**

新的组合 API 有更多的优点。考虑代码重用。目前，如果我们想在其他组件之间共享一些代码，有两种选择——混合和作用域插槽。两者都有缺点。

假设我们想要提取`counter`功能并在其他组件中重用它。下面您可以看到它如何与可用的 API 和新的组合 API 一起使用:

让我们从 mixins 开始:

```
import CounterMixin from './mixins/counter'export default {
  mixins: [CounterMixin]
}
```

mixins 最大的缺点是我们不知道它实际上给我们的组件添加了什么。这不仅使推理变得困难，还会导致与现有属性和函数的名称冲突。

是时候使用作用域插槽了。

```
<template>
  <Counter v-slot="{ count, increment }">
     {{ count }}
    <button @click="increment">Increment</button> 
  </Counter> 
</template>
```

有了作用域插槽，我们确切地知道我们可以通过`v-slot`属性访问什么属性，所以理解代码要容易得多。这种方法的缺点是我们只能在模板中访问它，并且它只能在`Counter`组件范围内使用。

现在是组合 API 的时候了:

```
function useCounter() {
  const count = ref(0)
  function increment () { count.value++ }return {
    count,
    incrememt
  }
}export default {
  setup () {
    const { count, increment } = useCounter()
    return {
      count,
      increment
    }
  }
}
```

优雅多了，不是吗？我们不受模板或组件范围的限制，并且确切地知道我们可以访问计数器中的哪些属性。此外，我们可以从编辑器中可用的代码完成中受益，因为`useCounter`只是一个返回一些属性的函数。幕后没有魔法，所以编辑器可以帮助我们进行类型检查和建议。

这也是使用第三方库的一种更优雅的方式。比如我们要用 Vuex，可以显式使用`useStore`函数，而不是污染 Vue 原型(`this.$store`)。这种方法也消除了 Vue 插件的幕后魔力。

```
const { commit, dispatch } = useStore()
```

如果你想了解更多关于 Composition API 及其用例的知识，我强烈推荐你阅读来自 Vue 团队的文档[,它解释了新 API 背后的原因并推荐了它的最佳用例。还有一个](https://vue-composition-api-rfc.netlify.com/)[很棒的资源库](https://github.com/LinusBorg/composition-api-demos)，里面有 Vue 核心团队的 Thorsten Lünborg 使用组合 API 的例子。

# 全球安装/配置 API 变更

我们可以在实例化和配置应用程序的方式中找到另一个主要变化。让我们看看它现在是如何工作的:

```
import Vue from 'vue'
import App from './App.vue'Vue.config.ignoredElements = [/^app-/]
Vue.use(/* ... */)
Vue.mixin(/* ... */)
Vue.component(/* ... */)
Vue.directive(/* ... */)new Vue({
  render: h => h(App)
}).$mount('#app')
```

目前，我们使用全局`Vue`对象来提供任何配置和创建新的 Vue 实例。对`Vue`对象的任何更改都会影响到每个 Vue 实例和组件。

现在让我们看看它在 Vue 3 中是如何工作的:

```
import { createApp } from 'vue'
import App from './App.vue'const app = createApp(App)app.config.ignoredElements = [/^app-/]
app.use(/* ... */)
app.mixin(/* ... */)
app.component(/* ... */)
app.directive(/* ... */)app.mount('#app')
```

正如你可能注意到的，现在每个配置的范围都是用`createApp`定义的某个 Vue 应用。

它可以使您的代码更容易理解，并且不容易出现由第三方附加组件引起的意外问题。目前，如果某个第三方解决方案正在修改 Vue 对象，它会以意想不到的方式影响你的应用程序(特别是使用全局混合),这在 Vue 3 中是不可能的。

这一 API 变化目前正在 [this](https://github.com/vuejs/rfcs/pull/29) RFC 中讨论，这意味着它可能会在未来发生变化。

# 碎片

在 Vue 3 中，我们可以期待的另一个令人兴奋的增加是片段。

你可能会问什么是片段？如果你创建一个 Vue 组件，它只能有一个根节点。

这意味着无法创建这样的组件:

```
<template>
  <div>Hello</div>
  <div>World</div>
</template>
```

原因是代表任何 Vue 组件的 Vue 实例都需要绑定到单个 DOM 元素中。创建具有多个 DOM 节点的组件的唯一方法是创建一个没有底层 Vue 实例的功能组件。

原来 React 社区也有同样的问题。他们提出的解决方案是一个名为 Fragment 的虚拟元素。看起来或多或少是这样的；

```
class Columns extends React.Component {
  render() {
    return (
      <React.Fragment>
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
```

尽管 Fragment 看起来像普通的 DOM 元素，但它是虚拟的，根本不会在 DOM 树中呈现。这样，我们可以将组件功能绑定到单个元素中，而无需创建冗余的 DOM 节点。

目前，你可以通过 [vue-fragments](https://vuejsdevelopers.com/2018/09/11/vue-multiple-root-fragments/) 库在 Vue 2 中使用片段，而在 Vue 3 中，你可以开箱即用！

# 焦虑

另一个将在 Vue 3 中采用的来自 React 生态系统的伟大想法是悬念组件。

暂停挂起组件呈现，并呈现回退组件，直到满足某个条件。在伦敦 Vue 期间，尤雨溪简要地谈到了这个话题，并展示了我们或多或少可以期待的 API。事实证明，悬念只是一个带槽的组件:

```
<Suspense>
  <template >
    <Suspended-component />
  </template>
  <template #fallback>
    Loading...
  </template>
</Suspense>
```

回退内容将一直显示，直到`Suspended-component`完全呈现。如果是异步组件，暂停可以等到组件被下载，或者在`setup`函数中执行一些异步操作。

# 多个虚拟模型

V-model 是一个指令，我们可以用它来实现给定组件的双向绑定。我们可以传递一个反应性属性，并从组件内部修改它。

我们从形式元素中很好地了解`v-model`:

```
<input v-model="property" />
```

但是您知道您可以对每个组件使用`v-model`吗？在引擎盖下`v-model`只是路过`value`酒店和聆听`input`事件的捷径。将上面的示例重写为下面的语法将会产生完全相同的效果:

```
<input 
  v-bind:value="property"
  v-on:input="property = $event.target.value"
/>
```

我们甚至可以用组件`model`属性更改默认属性和事件的名称:

```
model: {
  prop: 'checked',
  event: 'change'
}
```

正如您所看到的，如果我们想要在我们的组件中有双向绑定，那么`v-model`指令可以是一个非常有用的语法糖。不幸的是，每个组件只能有一个`v-model`。

幸运的是，这在 Vue 3 中不会成为问题！您可以给`v-model`房产命名，并且可以有任意多个。下面，您可以找到表单组件中两个`v-model`的示例:

```
<InviteeForm
  v-model:name="inviteeName"
  v-model:email="inviteeEmail"
/>
```

本 RFC 的[部分目前正在讨论 API 的这种变化，这意味着将来可能会发生变化。](https://github.com/vuejs/rfcs/pull/31)

# 门户网站

门户是用于呈现当前组件之外的某些内容的特殊组件。这也是 React 中本机实现的特性[之一。以下是 React 文档对门户网站的描述:](https://pl.reactjs.org/docs/portals.html)

*门户提供了一种一流的方式来将子节点呈现到存在于父组件的 DOM 层次结构之外的 DOM 节点中。*”

这是处理模态、弹出窗口和通常出现在页面顶部的组件的一种非常好的方式。通过使用门户，您可以确定没有任何宿主组件 CSS 规则会影响您想要显示的组件，并减轻您对`z-index`的恶意攻击。

对于每个门户，我们需要指定它的目标目的地，在那里门户内容将被呈现。下面您可以看到[门户-vue](https://github.com/LinusBorg/portal-vue) 库的实现，它为 Vue 2 增加了这个功能:

```
<portal to="destination">
  <p>This slot content will be rendered wherever thportal-target with name 'destination'
    is  located.</p>
</portal><portal-target name="destination">
  <!--
  This component can be located anywhere in your App.
  The slot content of the above portal component wilbe rendered here.
  -->
</portal-target>
```

Vue 3 将附带对门户的现成支持！

# 新的自定义指令应用编程接口

定制指令 API 将在 Vue 3 中稍微改变，以便更好地与组件生命周期保持一致。这种变化应该会让新来的人更容易理解和学习应用编程接口，因为它现在更直观了。

这是一个当前的自定义指令 API:

```
const MyDirective = {
  bind(el, binding, vnode, prevVnode) {},
  inserted() {},
  update() {},
  componentUpdated() {},
  unbind() {}
}
```

…这就是它在 Vue 3 中的样子。

```
const MyDirective = {
  beforeMount(el, binding, vnode, prevVnode) {},
  mounted() {},
  beforeUpdate() {},
  updated() {},
  beforeUnmount() {}, // new
  unmounted() {}
}
```

尽管这是一个突破性的变化，但它应该很容易被 Vue 兼容性构建所覆盖。

这一 API 变化目前正在 [this](https://github.com/vuejs/rfcs/pull/32/files) RFC 中讨论，这意味着它可能会在未来发生变化。

嘶！你可以在我们的课程中学习如何掌握自定义指令[。](https://vueschool.io/courses/custom-vuejs-directives)

# 摘要

除了 Vue 3 中最大的新 API Composition API，我们还可以找到很多小的改进。我们可以看到 Vue 正在向更好的开发者体验和更简单、更直观的 API 发展。很高兴看到 Vue 团队决定采用许多目前只能通过第三方库获得的想法作为框架的核心。

2022 年用 Vue 3 肯定是可取的。唯一的例外是当你已经有一个大的代码库或者你的依赖项还不支持 Vue 3 的时候。然而，在大多数情况下，即使是为了让您的大型代码库与 Vue 3 兼容，您也需要做最小的改动。如果你需要任何帮助或者通过 [Upwork](https://www.upwork.com/workwith/mayankkumarchaudhari) 联系我，请在评论区告诉我。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)