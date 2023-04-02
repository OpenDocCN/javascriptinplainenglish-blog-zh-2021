# 我最喜欢的查克拉界面部分

> 原文：<https://javascript.plainenglish.io/my-favourite-part-from-chakraui-4e1158126b0c?source=collection_archive---------6----------------------->

![](img/cbd5bb73b247ea704cd80e52ec9ed953.png)

Photo by [Ricardo Resende](https://unsplash.com/@rresenden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我一开始就没打算在我最新的 React 项目中使用任何像 Bootstrap 或其他的 UI 库。但是在工作中，现在仍在进行中(你可以在这里看到😝)，我想起了 Chakra UI 并决定尝试一下，因为我的项目变得越来越复杂，我需要快速准备好一个简单的组件。

原来我真的很喜欢查克拉，因为他们有某种“速记”的组成部分，甚至更短的道具。我们以后会谈到这件事。我也喜欢我们为组件设计风格的方式，因为它是通过 props 实现的，这比使用一个长类名更好。但实际上，这真的取决于谁在基于他们的偏好来工作，当然，做响应性的东西的便利性——使它工作有时需要一段时间。

# 成分

我想说的第一件事是“速记”部分。例如，我发现自己像这样使用 flex 重复居中的风格。

```
<div style={{display:'flex',alignItems:'center',justifyContent:'center'}}> {/* content */}</div>
```

但是他们提供了一个名为“中心”的组件，可以将组件中的任何内容居中，就像下面这样简单。

```
<Center> {/* content */}</Center>
```

你只需要一些像它的宽度或高度的配置。为了与所有脉轮组件保持一致，在他们的[文件](https://chakra-ui.com/docs/layout/box)中,‘div’组件被定义为‘Box’组件。或者，如果你已经习惯了 flex 样式，他们的“flex”组件已经将其显示定义为 Flex，或者它只是带有`display:flex;`的“盒子”。

它是这样定义的:

```
<Flex justify="center" align="center"> {/* content */}</Flex>
```

# 较短的道具

' Flex '组件有速记道具如 *justify-content* 变成 *justify* ， *align-items* 变成 only *align* ，不仅如此，常见的样式道具如 *width* ， *height* ， *margin* ， *padding* ， *background color* ，其他的如 *w，h，m，p，p*

当你有很多小道具要写的时候，这是非常有用的，用这样的小道具会让它更快，我真的很喜欢它。

# 应答的

我喜欢用 Chakra 做有反应的事情，因为它很容易设置。请记住，Chakra 使用`@media(min-width)`来确保接口采用移动优先。通常，我们会在 CSS 中使用媒体查询来响应某些组件。但是在 Chakra 里，你只能把它写在一个数组里。例如，您有一个“Box”组件，并希望它的宽度能够响应，可以这样做。

```
<Box w={["100%","90%","80%","70%"]}> {/* content */}</Box>
```

第一个值(100%)表示组件在最小屏幕尺寸下的宽度，第二个值表示组件在较大屏幕尺寸下的宽度，依此类推。它会将数组中的值解释为[ *base，sm，md，lg]* ，并根据屏幕大小表示组件大小。

基于上面的简单性，我可以在组件之间混合和匹配数组中的值，以保持它良好的响应。

# 结论

Chakra UI 提供了很多有用的特性，我相信还有更多需要发现的，我很乐意在我的下一个项目中使用它。

这是我最喜欢的关于 Chakra UI 的部分，我希望这篇文章能帮助和引起你对开始使用 Chakra 的兴趣。再见！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)