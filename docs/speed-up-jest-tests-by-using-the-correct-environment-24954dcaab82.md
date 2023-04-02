# 通过使用正确的环境加速 Jest 测试

> 原文：<https://javascript.plainenglish.io/speed-up-jest-tests-by-using-the-correct-environment-24954dcaab82?source=collection_archive---------5----------------------->

## DOM 很贵。只在需要的时候使用。

![](img/3c39672367483aff7168e8ef08c548e3.png)

Photo by [Stephanie LeBlanc](https://unsplash.com/@sleblanc01?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近在 [Parallax](https://www.getparallax.com/) ，我们注意到我们的 UI 测试套件花了越来越长的时间才完成。这是几分钟的事，所以不是什么大问题。至少现在还没有。然而，这是一个影响开发和延长反馈周期的问题。这是我们希望尽快解决的问题。

我们决定调查一下，看看能否加快速度。

# 问题

在撰写本文时，我们的 UI 应用程序有大约 1600 个单元测试。我们使用[Jest](https://jestjs.io/)TypeScript 和 [React 测试库](https://testing-library.com/docs/react-testing-library/intro/)。我们大约一半的测试是针对需要一个 [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction) 的 [React](https://reactjs.org/) 组件。另一半是纯函数或者[类型脚本类](https://www.typescriptlang.org/docs/handbook/classes.html)。这些不需要 DOM 来测试，只需要一个[节点](https://nodejs.org/en/)环境。

Jest 使用节点通过 CLI 运行。Node 里不存在`window`、`document`之类的东西。因此，我们必须向 Node 提供一个假的 DOM。可以想象，需要 DOM 的测试增加了对某种 DOM 库的依赖。

Jest 测试的 Jest 文档指出 [jsdom](https://github.com/jsdom/jsdom) 是这项工作的推荐工具。您可以通过两种方式设置 Jest 环境；通过 Jest 配置，或者通过在单独的测试文件中使用一个特殊的 doc 块。

我应该提到，在我们的配置中，默认的全局环境被设置为`jsdom`。

![](img/1d5ff0603ae279496bf719c5b7282fda.png)

Photo by [AbsolutVision](https://unsplash.com/@freegraphictoday?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 解决办法

对我们如何让事情变得更好有什么猜测吗？我已经暗示过了。我给你一分钟考虑一下。

从高层次来看，我们的解决方案是将默认 Jest 环境设置为`node`。然后，在需要 DOM 的测试中，我们添加了一个 [docblock](https://en.wikipedia.org/wiki/Docblock) 来告诉 Jest 使用`jsdom`环境而不是`node`。

我想承认，我们并不仅仅是靠自己解决了这个问题。像任何优秀的工程师一样，我们首先在互联网上找到了答案。

[](https://itnext.io/how-to-make-your-sluggish-jest-v23-tests-go-faster-1d4f3388bcdd) [## 如何让你缓慢的 Jest v23 测试进行得更快

### 让单元测试再次变得伟大

itnext.io](https://itnext.io/how-to-make-your-sluggish-jest-v23-tests-go-faster-1d4f3388bcdd) 

为了在我们的项目中实施这个修复，我们通过三个简单的步骤来完成:

## 将`node`设置为默认测试环境

这对速度产生了直接的积极影响。但也导致我们一半的测试失败。我们预料到了这一点，因为 node 没有 DOM。因此，需要 DOM 的测试现在都有点麻烦了。

## 将 jsdom Docblock 添加到组件测试文件中

一旦我们转移到`node`作为默认测试环境，我们突然有了一个失败测试的集合。我们的目录结构使得找到大多数组件测试变得非常容易。一旦定位了组件测试，就需要在文件的顶部添加一个具有正确环境的 doc 块。

```
*/***
 ** @jest-environment jsdom*
 **/*
```

然后，我们重新运行测试，并验证事情再次通过。很简单！

## 更新组件生成器以包含 jsdom Docblock

最后一步同样重要:更新我们的生成器，使其包含文档块。这样，就可以用正确的文档块创建新的组件测试。

多年来， [Robert S (codeBelt)](https://medium.com/u/32c8aef7a385?source=post_page-----24954dcaab82--------------------------------) 已经建立了一个健康的[生成器集合](https://medium.com/@robertsavian/generate-template-files-with-ease-19b320615359)，我们在我们的项目中使用它。这些生成器使得在我们的项目中创建新文件变得非常简单。

# 结论

这实际上产生了多大的影响？我们的测试现在运行得更快了。这是有意义的，考虑到我们只有在需要的时候才旋转 DOM(大约一半的时间)。

在我们做了这个改变之后，我们从每次运行大约 120 秒下降到大约 80 秒。这不是一个巨大的变化，但确实有所不同。

## 参考

*   [https://www.getparallax.com/](https://www.getparallax.com/)
*   [https://jestjs.io/](https://jestjs.io/)
*   [https://www.typescriptlang.org/](https://www.typescriptlang.org/)
*   [https://testing-library . com/docs/react-testing-library/intro/](https://testing-library.com/docs/react-testing-library/intro/)
*   【https://reactjs.org/ 号
*   [https://developer . Mozilla . org/en-US/docs/Web/API/Document _ Object _ Model/简介](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
*   [https://www.typescriptlang.org/docs/handbook/classes.html](https://www.typescriptlang.org/docs/handbook/classes.html)
*   [https://nodejs.org/en/](https://nodejs.org/en/)
*   [https://jestjs.io/docs/configuration#testenvironment-string](https://jestjs.io/docs/configuration#testenvironment-string)
*   [https://github.com/jsdom/jsdom](https://github.com/jsdom/jsdom)
*   [https://en.wikipedia.org/wiki/Docblock](https://en.wikipedia.org/wiki/Docblock)
*   [https://it next . io/how-to-make-your-sleep-jest-v 23-tests-go-faster-1d4f 3388 bcdd](https://itnext.io/how-to-make-your-sluggish-jest-v23-tests-go-faster-1d4f3388bcdd)
*   [https://medium . com/@ Roberts avian/generate-template-files-with-ease-19b 320615359](https://medium.com/@robertsavian/generate-template-files-with-ease-19b320615359)

*更多内容看* [*说白了就是*](http://plainenglish.io/) *。报名参加我们的* [*免费每周简讯*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和谐*](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。*