# 如何在 React 中将道具从子组件传递到父组件

> 原文：<https://javascript.plainenglish.io/how-to-pass-props-from-child-to-parent-component-in-react-d90752ff4d01?source=collection_archive---------0----------------------->

学习这个简洁的小技巧，将大块的道具传递回组件树！

![](img/c56b48c135ca79a88128bb6edd504ee3.png)

Photo by [Sai Kiran Anagani](https://unsplash.com/@_imkiran?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 快速简单:

如果您使用过 React，显然您已经使用 props 将数据从父组件传递到子组件。**这被称为单向数据流**。

如果我向您展示一个小技巧，允许您将小块道具从**子**组件反向传递回**父**组件，会怎么样？

诀窍就在这里——非常简单。我们有 2 个组件:

*   **父** : `App.js`
*   **子** : `Child.js`

*使用以下步骤:*

*   在父组件中创建一个函数，给它传递一个参数，并使用`console.log`记录这个参数。
*   将函数名作为道具传递给子组件 render。
*   从子组件内部的 props 调用函数。
*   将您的数据作为参数传入调用中。
*   *堇菜。*

# 父组件:

# 子组件:

***就这么简单！***

另外，注意在`Child.js`里面，React 片段`<> ... </>`的使用。

这允许我们创建更少的 DOM 节点，给我们的应用程序一个小的性能提升。这也有助于调试(减少`div`的混乱)。

**感谢**的阅读——我希望这能提供一些有用的信息。

**到[PJCodes.com](http://www.pjcodes.com/)来找我**。

## 进一步阅读

[](/code-documentation-is-broken-but-i-think-swimm-may-have-fixed-it-daaa7547d834) [## 代码文档被破坏了——但是我认为 Swimm 可能已经修复了它

### 传统的文档管理系统让软件开发人员失望了，是时候来点新的了。游泳吗…

javascript.plainenglish.io](/code-documentation-is-broken-but-i-think-swimm-may-have-fixed-it-daaa7547d834) [](https://bit.cloud/blog/composable-link-component-that-works-in-any-react-meta-framework-l7i3qgmw) [## 可在任何 React 元框架中工作的可组合链接组件

### Bit 的链接组件是一个与运行环境无关的组件。您可以将此链接用于…

比特云](https://bit.cloud/blog/composable-link-component-that-works-in-any-react-meta-framework-l7i3qgmw) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*[***不和***](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [***电路***](https://circuit.ooo/) *。***