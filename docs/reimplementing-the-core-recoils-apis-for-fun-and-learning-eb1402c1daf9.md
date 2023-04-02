# 为了娱乐和学习，重新实现反冲的核心 API

> 原文：<https://javascript.plainenglish.io/reimplementing-the-core-recoils-apis-for-fun-and-learning-eb1402c1daf9?source=collection_archive---------13----------------------->

我总是渴望探索学习途径(你可以在我的[选择不学习什么和一次专注于一件事](https://medium.com/@NoriSte/choose-what-not-to-study-and-focus-on-one-thing-at-a-time-b7304ac2a125)文章中读到更多)，但是我仍然缺少重新实现 API。肯特·c·多兹(Kent C. Dodds)的一篇文章启发了我，于是我们就有了这篇文章。

![](img/e6ee3e8801c095b3e9f204a350ccc66e.png)

Photo by [Shane Aldendorff](https://unsplash.com/@pluyar?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

我们在工作中使用[反冲](https://recoiljs.org/)；这是 [WorkWave RouteManager 的](https://www.workwave.com/route-manager/)下一个架构的核心元素。反冲具有很好的易用性，它消除了本地和全局状态管理之间的所有区别。它还不完美，但相对稳定。

***请注意:*** *这篇文章八个月未发表。我应该重写它，因为我意识到代码和设计决策通过视觉更容易理解，把代码留在最后。但是既然* ***做得不如做得完美，*** *我决定照原样发表这篇文章。作为对自己的一个提醒，我认为* [*Maty Perry 的《布局投影:以 60fps 制作浏览器布局动画的方法》*](https://mattperry.is/writing-code/layout-projection-animate-browser-layout-60fps) *是如何写一篇技术文章的绝佳范例。*

# 要求

目标是重新实现`atom`和`selector`API，只是同步版本。这意味着

*   实现`atom` API 来创建新的原子
*   实现`selector` API 来创建依赖原子和其他选择器的新选择器
*   实现`useRecoilValue` API 来获取一个原子/选择器值，并订阅(也称为重新呈现)它们的更新
*   实现`useRecoilState` API 以获得所有`useRecoilValue`特性并设置原子/选择器
*   实现`RecoilRoot` API 以避免在不同的组件树之间共享状态(我需要它只是为了测试)

在深入研究代码之前，我们需要的是:

1.  **存储原子的值**:原子本身只是普通的物体，反冲存储器必须保持它们当前的状态
2.  **更新订阅的组件**当一个 Atom 更新时，强制它们重新渲染
3.  通过 React 挂钩公开 API
4.  用 id 区分每个商店，因为每个反冲根都是独立的
5.  保持一个反冲根的 ID 私有，我们不想暴露内部实现细节

## 可能的解决方案:

*   存储值(#1)将是普通对象
*   对于#2，我们需要为每个用户注册一个回调
*   #3 我们可以强制组件重新呈现的唯一方法是保持一个内部状态并更新它。其他州立图书馆是怎么做的？看看它的内部，反冲是通过`useState`实现的:

```
const [_, setValue] = useState({});
forceUpdate = () => setValue({});
```

而 Redux 在内部通过`useReducer`完成

```
const [, forceRender] = useReducer(s => s + 1, 0)
```

*   如今，我认为第四点是理所当然的😉
*   #5 要求我们使用 React 上下文，由反冲根组件拥有
*   我们将用一些包装核心函数的高阶函数来管理# 6(稍后，我将解释如何做到这一点)

## 选择器呢？

1.  选择器是无状态的。它们的`get`是从其他原子和选择器中获取值的纯函数
2.  **当选择器依赖的原子/选择器之一更新时，选择器必须更新**
3.  选择器也可以写其他原子和选择器的值

因此:

*   对于#1，我们需要一些糖围绕原子的核心功能
*   #2 迫使我们找出选择器依赖的原子和选择器，并订阅它们
*   #3 利用现有的 Atom setters，仅此而已

要点:在项目的核心，**商店必须收集价值和订户**；订户可以是使用所提供的挂钩或选择器的组件。

你可以[在 CodeSandbox](https://codesandbox.io/s/recoil-apis-gl2cb?file=/README.md) 上玩这个项目，或者在 GitHub 上把它分叉[。下面，我将指导您通过上下文分解相关代码:核心/公共类型、核心/公共 API 和钩子。](https://github.com/NoriSte/recoil-apis-codesandbox)

## 类型

*如果想跳过解释:直接进入*[*GitHub*](https://github.com/NoriSte/recoil-apis/blob/master/src/recoil/typings.ts)*上的 typings.ts 文件。*

我们将在后面描述公开的 API/类型。让我们先集中讨论需要在内部存储哪些数据。我将区分内部函数和前缀为`core`的公共函数。

## 核心反冲值

内部反冲值。每个原子都应该:

*   有识别键
*   有默认值
*   有当前值
*   有一个更新时要通知的订阅者列表

虽然每个选择器应该:

*   有识别键
*   有一个更新时要通知的订阅者列表

所以`CoreRecoilValue`的签名如下:

The CoreRecoilValue signature. [Check it out on Gist](https://gist.github.com/NoriSte/00a1aed85faccb8c635cc0d42869ee80).

请注意:

*   我们不需要在创建 Atom 时传递`T`,因为 TypeScript 可以从默认值中推断出它
*   有多种方法来设计这种类型，但是我认为有区别的联合非常简洁明了

## 反冲储备

每个`RecoilRoot`必须有一个专门的商店和一个唯一的 id。一个`RecoilStore`是一个`Record`,通过它们的键识别反冲值，而`RecoilStores`是一个记录，通过它们的反冲 id 存储每个`RecoilStore`。更容易看到代码😊

The RecoilStores signature. [Check it out on Gist](https://gist.github.com/NoriSte/8c5366fef7209a936d7a7aa1969368f9).

## 公共类型

关于公共类型没什么好说的，因为我是在复制反冲的类型定义😊

The public types brought directly from Recoil. [Check it out on Gist](https://gist.github.com/NoriSte/85520178804b9a1392d8521f42f81f8d).

你可以在 GitHub 上看一下[完整的 typings.ts 文件。](https://github.com/NoriSte/recoil-apis/blob/master/src/recoil/typings.ts)

# 核心 API

*如果想跳过解释:直接去 GitHub* *上的*[*core . ts 文件。*](https://github.com/NoriSte/recoil-apis/blob/master/src/recoil/core.ts)

内部 API 和实用程序的混合，最终用户不会知道它们。

## 吸气剂

最容易的函数是 getters。他们应该:

*   从`RecoilStore`中检索原子的当前值或调用`selector.get`函数
*   公开一个泛型`coreGetRecoilValue`,它使用上面提到的专用 getters
*   高阶函数(`createPublicGetRecoilValue`)，允许在不知道反冲 id 的情况下利用`coreGetRecoilValue`

The getters implementation. [Check it out on Gist](https://gist.github.com/NoriSte/8ec8bf8e4487edaee0a1914f56c25070).

请注意:

*   核心函数被标记为`@private`是为了强调最终用户不能导入它们。
*   `registerRecoilValue`是主动反冲存储器(组件所在的存储器)和原子本身的第一个接触点

如果您不熟悉高阶函数模式，这是一种预先配置您稍后需要调用的函数的方法。此外，所有的核心函数都需要知道反冲 id，但是，与此同时，它们的公共对应函数需要隐藏 id。

这里有一个超级简洁(没有箭头函数)的要点来说明这个想法。看看`logId`和`logIdWithoutKnowingIt`函数，它们做同样的事情，但是后者不需要 id。

A super-simple example of higher-order-functions. [Check it out on Gist](https://gist.github.com/NoriSte/5d9ca4abdbffb7bc194be159898a7314).

## 安装员

基本器械包功能包括:

*   设置原子的新值
*   调用所有订户
*   在选择器的情况下，调用它们的`set`函数(如果已定义)
*   暴露了通常的反冲无 id 功能

代码如下:

The setters implementation. [Check it out on Gist](https://gist.github.com/NoriSte/96647da462a42172c838bfdd7bcef31e).

## 注册和订阅

到目前为止，一切都是普通的 JS，让我们进入 React 的领域:注册和订阅。

注册必须是幂等的(调用一次或多次的效果必须是一样的)。为什么？因为我们必须在需要时注册反冲值(因为反冲 Id 存储在 React 上下文中，我们无法提前知道)，可能的选项有:

*   在尝试注册反冲值之前，检查反冲值是否已经注册
*   调用`registerRecoilValue`而不关心之前的注册，它会检查自己

我选择了后者，使得`registerRecoilValue`幂等。

`subscribeToRecoilValueUpdates`必须只返回退订者，这里是注册和订阅的代码:

Registration and subscription implementation. [Check it out on Gist](https://gist.github.com/NoriSte/c30f3ac1bf73fc46c78d60e6b0db712c).

你可以在 GitHub 上看一下整个 [core.ts 文件。](https://github.com/NoriSte/recoil-apis/blob/master/src/recoil/core.ts)

# 反应 API

*如果想跳过解释:直接去 GitHub* *上的 api.ts 文件。*

## useRecoilValue 和 useRecoilState

这里是基本的 API。`useRecoilValue`必须:

*   从由反冲根组件创建的 React 上下文中检索当前反冲 Id
*   记录反冲值
*   为组件订阅每一次 Atom/Selector 更新(就像官方那样)
*   获取当前的后坐力值(像官方的一样)

`useRecoilState`利用`useRecoilValue`检索当前值，然后它必须

*   为原子提供一个设置器
*   为选择器提供一个 setter，这意味着调用选择器'`set`(如果定义了的话)，向它传递一个反冲值 getter 和一个 setter

这是我们之前定义的高阶函数的第一次使用。请记住，我们需要让消费者访问一些隐藏反冲 Id 的核心功能(如设置原子)，这就是我们创建`createPublicGetRecoilValue`和`createPublicSetRecoilValue`的原因。

这是代码

UseRecoilValue and useRecoilState implementation. [Check it out on Gist](https://gist.github.com/NoriSte/e914c58d37ab6b34c5b962c169392ca4).

## 签署

最后缺少的一点是组件如何订阅反冲值更新以及如何取消订阅。这个必要的行为是免费的。棘手的部分是从选择器中获取依赖关系树，并订阅每个反冲值更新:`createDependenciesSpy`会这样做。

The subscription implementation. [Check it out on Gist](https://gist.github.com/NoriSte/bd57eebfb13ac859702c04803c09cd7c).

你可以在 GitHub 上看看完整的 [api.ts 文件。](https://github.com/NoriSte/recoil-apis/blob/master/src/recoil/api.ts)

## 反冲根

每个反冲树的父树。它的唯一任务是在消耗反冲值的孩子周围创建反冲上下文。代码很简单。

The RecoilRoot implementation. [Check it out on Gist](https://gist.github.com/NoriSte/f1c2b23730a13380feec25bc2d5f533e).

## 有用！

我们到了！你可以[在 CodeSandbox](https://codesandbox.io/s/recoil-apis-gl2cb?file=/README.md) 上玩这个项目，或者在 GitHub 上将它分叉[。](https://github.com/NoriSte/recoil-apis-codesandbox) [App.tsx](https://github.com/NoriSte/recoil-apis/blob/master/src/App.tsx) 代码强调上述内容:

*   注册一些原子和选择器，就像你注册反冲一样
*   注册依赖于原子和选择器的选择器
*   提供选择器组
*   记录组件的每一次重新渲染，因为在使用应用程序时，您可以用眼睛检查所有内容是否都按预期更新，但您无法检查组件被重新渲染了多少次，所以看一下控制台

## 试验

为了这个项目的缘故，我不想只检查一切是否如预期的那样工作，但我想确保组件不会比预期的更多地重新渲染。在项目开发过程中，我经常需要这样做，所以我编写了一些测试来自动化我的手工检查。

## 常见问题

*上述代码中是否存在一些未经测试的场景？*

是的，我手动测试了一切正常

*   元件会动态更改其订阅的反冲值
*   一个选择器设置另一个选择器

*为什么要用双引号和分号？*

我不在乎定制默认的 CodeSandbox 的漂亮配置😉

还有其他方法吗？

当然，看看贝内特·哈德威克的《[重写脸书的《反冲](https://bennetthardwick.com/blog/recoil-js-clone-from-scratch-in-100-lines/)》一文《从零开始反应库 100 行》。他使用一种更基于班级的方法。请检查一下！

# 结论

我喜欢重新实现反冲 API，因为

*   它迫使我看一看反冲内部
*   这让我接触到了不同的问题，因此我开始思考更广泛的解决方案
*   这让我开始创作一种新型的博客，在那里我试图解释一些设计决策，我以前的文章大多是关于问题和解决方案，讲述我的经历，或者试图启发人们

我不喜欢那样做，因为

*   我知道做兼职项目对我来说并不理想，我有时是个完美主义者😁

## **我的更多文章，你可能会喜欢:**

*   我与赛普拉斯的旅程:[选择不学什么，一次专注一件事](https://medium.com/@NoriSte/choose-what-not-to-study-and-focus-on-one-thing-at-a-time-b7304ac2a125)
*   为什么测试是讲述你的代码故事的完美方式:[作为文档工具的软件测试](https://medium.com/@NoriSte/software-tests-as-a-documentation-tool-e1c463bad1be)
*   从前端测试世界获得即时结果(和满意度)的更简单的方法:[刚接触前端测试？从金字塔的顶端开始！](https://medium.com/@NoriSte/new-to-front-end-testing-start-from-the-top-of-the-pyramid-a0039615353c)

别忘了看看我在 GitHub 上的 [UI 测试最佳实践](https://github.com/NoriSte/ui-testing-best-practices)的书。

## 关于我

你好👋我是斯特凡诺·马尼，我是一个充满激情的**前端工程师**，一个**柏树大使**，一个**导师**。我是 WorkWave 的高级前端工程师。

我喜欢创造高质量的产品，测试和自动化一切，学习和分享我的知识，帮助别人，在会议上发言，面对新的挑战。

你可以在 [Twitter](https://twitter.com/NoriSte?source=post_page---------------------------) 、 [GitHub](https://github.com/NoriSte?source=post_page---------------------------) 、 [LinkedIn](https://www.linkedin.com/in/noriste/?source=post_page---------------------------) 上找到我。你可以找到我最近所有的投稿/演讲等。关于[我的 GitHub 总结](https://github.com/NoriSte/all-my-contributions)。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)