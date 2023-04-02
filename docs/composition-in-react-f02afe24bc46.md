# 合成:React 中道具演练的替代方案

> 原文：<https://javascript.plainenglish.io/composition-in-react-f02afe24bc46?source=collection_archive---------4----------------------->

## 在接触上下文或库之前，考虑一下组成。

![](img/df2247a7bbf83a5ecbf8d459fda50273.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/blocks?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

React 为构建组件的数据流实现了单向模式。模式本身并不是唯一的反应，而是被严格遵循的。

> 单向数据流简单地说就是数据只能单向流动**。**

根据定义——如果有 React 的经验——您会注意到子组件不能将数据传递给父组件；因此，数据只能单向流动，“从父节点**到**子节点

**如果我们需要修改影响父组件或在两个子组件之间共享状态的子组件，我们使用 props。**

**我们来看一个小例子。**

**在上面的例子中，我们做了一些假设，比如 App 函数负责处理登录，它将" *loggedIn* "状态和" *handleSetLoggedIn* "函数传递给 Header。**

**让我们研究一下 Header 组件，看看它是如何利用这些属性的。**

**上面，我们可以看到 Header 组件没有使用 props，而是将它们传递给使用它们的 Profile 组件。这种情况被称为道具演练。**

## **道具钻探**

**Props drilling 是将道具传递给一个不需要这些道具的子组件，但帮助将其传递给自己的子组件，子组件可能会将其传递给自己的子组件，因为在到达真正需要这些道具的子组件之前，它也不需要这些道具。**

**道具训练的问题是事情变得混乱，调试可能很快变得困难。**

**一个好的解决方案可能是使用上下文 API 或 Redux，但这并不是解决这个问题所必需的。**

**我们可以利用组合(组件组合)来为自己谋利。事实上，React 团队说:**

> **[**如果只是想避免一些道具经过很多关卡，组件组合往往是比上下文更简单的解决方案。**](https://reactjs.org/docs/context.html#before-you-use-context)**
> 
> ****—反应小组****

## **什么是作文？**

**组合是将组件或元素组装成一个整体的行为。**

**React 提供了一个帮助构图的强大工具，这就是儿童道具。**

**我们可以像这样轻松地重构我们的 Header 组件。**

**孩子的道具在每个部件上都有。它包含组件的开始和结束标记之间的内容。**

**现在，我们的 Header 组件是我们选择在其中呈现的子组件的包装器。**

**这使我们能够在" *App.js* "中重构我们的应用组件 render**

**我们利用构图解决了道具演练的问题。**

**这种模式也给了我们构建更具可伸缩性的可重用组件的能力，尤其是当构建一个工具、一个库或由大量不同需求的人使用的组件时。**

**下一篇文章将构建一个卡片组件，并看看构图是如何成为一个令人兴奋的模式来思考和经常使用。**

**谢谢你的阅读。**

## **进一步阅读**

**[](https://bit.cloud/blog/design-tokens-in-components-with-react-and-bit-l28qlxq6) [## 具有反应和比特的组件中的设计令牌

### 现场演示更好。在深入讨论细节之前，让我们看看使用 Bit 的设计令牌如何帮助我们构建……

bit.cloud](https://bit.cloud/blog/design-tokens-in-components-with-react-and-bit-l28qlxq6) 

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在* [***推特***](https://twitter.com/inPlainEngHQ)[***领英***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)***和******T48 不和**T52 *对成长黑客感兴趣？查看* [***电路***](https://circuit.ooo/) ***。*******