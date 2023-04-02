# 关于 CSS 位置属性，您只需要知道

> 原文：<https://javascript.plainenglish.io/all-you-need-to-know-about-the-css-position-property-c329b2882613?source=collection_archive---------25----------------------->

## CSS 位置属性。

![](img/61a57eaba8e52e30a9b1cf0d111bdd39.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

使用 CSS 总是一件痛苦的事，有时会让你怀疑自己是否做对了每一件事。CSS 位置属性总是很难去神秘化，并且很难理解它是如何在幕后工作的。在这篇文章中，我们将学习一些很酷的 CSS 位置属性。

CSS position 属性设置元素在文档流中的位置。元素可以用以下任一方式定位:静态、相对、绝对、固定或粘滞。

所有主流浏览器都支持 CSS 位置，包括 Firefox、Chrome、Safari、Internet Explorer 等。

## 相对位置

具有相对位置的元素相对于其原始位置进行定位。该属性将元素保留在文档流中。

通过设置元素的相对位置，可以使用 offset 属性将其定位在顶部、底部、左侧或右侧。

## 绝对位置

将元素设置为绝对位置会将该元素从文档流中移除。

该属性将元素放置在文档流中，就好像它不存在一样。通过从文档流中移除元素，我们可以使用 top、bottom、left 或 right 来设置它的位置。

绝对位置设置位于其父(相对)元素旁边的元素。应用此位置允许使用顶部、左侧、右侧或底部在页面上定位元素。

## 位置粘性

粘性定位可以被认为是相对定位和固定定位的混合。

粘性定位的元素被视为相对定位的，直到它越过指定的阈值。根据 Mozilla 的说法，在这一点上，它被视为固定的，直到它到达其父节点的边界。

它相对定位，直到在文档流中满足给定的偏移量。位置设置为 sticky 的元素基于用户滚动行为进行定位。它在相对和粘性之间转换。

## 位置固定

“位置固定”属性将元素固定设置为文档流中的一个点。

它通常用在页脚部分，总是意味着在一个固定的位置查看。

如果设置，元素将在文档流中保持固定位置。

## 在你走之前

感谢您阅读本文到目前为止；如果你发现它有帮助，请不要犹豫分享。

## 更多阅读:

[](/why-you-should-be-part-of-a-developer-community-f3e28bc13c88) [## 为什么你应该成为开发者社区的一员

### 开发者社区组织者的故事。

javascript.plainenglish.io](/why-you-should-be-part-of-a-developer-community-f3e28bc13c88) [](/soft-skills-every-programmer-needs-to-have-32d321e4a15e) [## 每个程序员都需要具备的软技能

### 作为程序员，你需要这些软技能来提高。

javascript.plainenglish.io](/soft-skills-every-programmer-needs-to-have-32d321e4a15e) 

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)