# 10 个初级前端开发人员技术面试问题

> 原文：<https://javascript.plainenglish.io/10-junior-frontend-developer-technical-interview-questions-4342da7c7fd0?source=collection_archive---------1----------------------->

## (和答案)

![](img/abce324dbba7fa843c05fb83d3d53737.png)

Photo by [Maranda Vandergriff](https://unsplash.com/@mkvandergriff?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/interview?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当我面试一个初级前端开发人员的职位时，我被问到了这 10 个连珠炮似的问题。尽情享受吧！

# 半铸钢ˌ钢性铸铁(Cast Semi-Steel)

## **1。当你做相对设计时，你有不同的相对单位，比如 em，%,等等。其中一个叫 em，另一个叫 rem。你能告诉我这两者的区别吗？**

EM 相对于直接父级，而 REM 仅相对于 html(根)字体大小。

## **2。你如何把一些东西放到页面的右下角？**

假设我们有这样一个代码:

那么我们的 CSS 需要看起来像这样:

其工作方式是绝对定位的元素总是相对于第一个相对定位的父元素或窗口定位。因为我们将盒子的位置设置为相对位置。文本框文本将其右边缘定位到的右边缘。框及其下边缘到. box 的下边缘。

# Java Script 语言

## **3。除了回调之外，JS 中处理异步编程的其他方法有哪些？**

使用承诺——标准方式。

## 4.说到承诺，你知道 async-await 是什么吗？
**async/await 和 Promises 有什么区别？**

没有！Async/await 是使用 promises 的不同 API。Async/Await 在更复杂的场景中提供了更好的语法。特别是，任何处理循环或某些其他结构的东西，比如`try` / `catch`。

## 5.最流行的两个 Ajax 库是什么？

Axios 和获取。

# 反应

## 6.React — **当你想进行 Ajax 调用时，你通常会使用什么钩子？**

使用效果挂钩。

## 7.React — **如果你正在渲染一个对象数组，你通常会用适当的键传递什么？用什么值最好？**

一些独特的身份。数据库中的 GUID 之类的。

## 8.React — **你知道 React 里的片段是什么吗？**

组件的多个部分需要用某种东西包装起来才能成为一个节点。Fragment 是多个组件的包装器，然后成为单个节点，但它不向 DOM 呈现任何内容——它是一个不可见的包装器。

## 9.React —说到碎片，你知道为什么碎片比 div 好用吗？

这有几个原因。通过不创建额外的 DOM 节点，片段速度更快，使用的内存更少。但是，这只对非常大和深的树有真正的好处。有些 CSS 机制像 *Flexbox* 和 *CSS Grid* 有特殊的父子关系，在中间添加 div 很难保持想要的布局。此外，DOM 检查器也不那么杂乱。

# 超文本传送协议

## 10.假设你正在做一个 API，你想修改一个资源，你会使用什么 HTTP 动词？

放置或修补。

# 结论

我们做到了！如果你要去参加初级前端开发人员的面试，准备 10 个问题是很有用的。还有其他我们漏掉的吗，或者你有什么建议吗？一定要把它们留在评论里。