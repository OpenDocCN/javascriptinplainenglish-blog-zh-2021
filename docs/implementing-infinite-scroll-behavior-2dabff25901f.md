# 如何实现无限滚动行为

> 原文：<https://javascript.plainenglish.io/implementing-infinite-scroll-behavior-2dabff25901f?source=collection_archive---------9----------------------->

## 学习反应 JS

## 利用 MDN 的交叉观察器

![](img/025d30270f7c5f34f3fdab3537a419ca.png)

Photo by [Dan Freeman](https://unsplash.com/@danfreemanphoto?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/spiral?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在过去的一周里，我决定在我当前的项目中加入一个无限滚动的特性。任何在互联网上呆过哪怕是很短时间的人都可能熟悉这种行为。给定提要、新闻页面、列表等。，当用户滚动时，内容将持续加载，提供无缝的提要，直到用户查看了所有可用的数据或达到其他限制。

我知道*想要做什么*，但我不确定*如何*着手实现这个功能。我很高兴地发现 MDN 提供了一个名为`IntersectionObserver`的 API，这在这方面非常有帮助。学习这项技术已经在我的“待办事项”清单上有一段时间了，我很高兴现在已经把它添加到我的工具箱中。

# 可交付成果

*   当用户第一次访问页面时，会加载一定数量的内容
*   当用户向下滚动时，向服务器发出一个异步请求，返回下一批内容。
*   附加内容被附加到页面的底部，允许用户无限地连续向下滚动(或者直到所有可用的内容都被显示)。

# 相关阅读

本演练要求对 React refs 有基本的了解。如果您不熟悉 React 中的引用，我建议您先阅读以下文章:

*   [***到底什么是裁判？***](/whats-a-ref-anyway-2a6979ad173f)
*   [***理解回调引用***](/understanding-callback-refs-107a21d831d7)

它们都是快速阅读，肯定会加深你对无限滚动的理解，并做出总体反应。阅读它们？好吧，酷。我们继续。

# 用另一个名称分页

当你开始使用它时，无限滚动只是显示分页数据的另一种方式。分页将数据集合分解成不同的可管理的块，并按顺序向用户显示这些块。无限滚动的工作方式类似，但不是将块分成不同的页面，而是在用户滚动时异步加载内容，从而导致内容的无休止输入。

这意味着您对服务器的调用看起来像任何其他涉及分页的请求。

Standard Redux GET action to retrieve paginated data from an API back end.

# 观察十字路口

因此，我们有从后端请求数据的逻辑，但是我们如何知道何时发出这些请求呢？这就是 MDN 的`IntersectionObserver`发挥作用的地方:

> [交集观察器 API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) 提供了一种异步观察目标元素与祖先元素或顶层文档的[视口](https://developer.mozilla.org/en-US/docs/Glossary/Viewport)交集变化的方法。

`IntersectionObserver`构造函数接受一个回调函数，默认情况下，每当目标元素进入用户的视窗时，这个函数就会被执行。目标元素作为参数传递给一个`entries`数组中的回调函数，以便根据需要记录或操作。

*(* ***先不说:*** *初始化观察者时，通过传递一个附加的* `*options*` *对象，可以微调交叉点事件触发的时间。查看* [*MDN 的文档*](https://developer.mozilla.org/en-US/docs/Web/API/IntersectionObserver/IntersectionObserver) *了解更多信息)*

当元素作为一个参数单独传递给观察者的`.observe()`方法时，观察者会跟踪这些元素。

# 将它并入 React

在本教程的帮助下，我将`IntersectionObserver`合并到我的项目中。利用 [**回调引用**](/understanding-callback-refs-107a21d831d7) ，我们可以将观察者与它可能正在观察的任何元素断开连接，然后创建一个新的`IntersectionObserver`对象来观察页面上最后呈现的元素。`observer`使用自己的回调函数，该函数递增本地状态中存储的`pageNum`。结合前面显示的调度`GET`请求的`useEffect`钩子，你瞧，无限滚动！

你在自己的一个项目中实现过无限滚动吗？如果是，您是否利用了上面显示的方法，或者实施了不同的策略？

*更多内容请看*[*plain English . io*](http://plainenglish.io/)