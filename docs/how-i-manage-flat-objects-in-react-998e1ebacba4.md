# 我如何在 React 中管理平面对象

> 原文：<https://javascript.plainenglish.io/how-i-manage-flat-objects-in-react-998e1ebacba4?source=collection_archive---------6----------------------->

![](img/c30b1a88bd4327298108feb3c5b5c994.png)

我想分享一个我喜欢在 React 应用程序状态下更新平面对象时使用的设计模式。这是我发现的用一个函数更新一个对象中多个字段的好方法。

我的例子是一个 React+Typescript 应用程序，它使用 Redux Toolkit 来管理它的全局状态。我的状态有一个成员对象，它需要一个 UI 来允许用户更新它的属性。

我将提供下面的所有代码，并逐一检查每个部分。

## 类型

**IMember** :我们将在我的状态中更新的对象。

**动作**:这个接口在 Redux Toolkit 文档中提供。它允许你使你的减压器的动作有效载荷通用。

**IGenericUpdate** :这是我想出来的一个接口，允许我更新不同的平面对象。我使用 Typescript keyof 特性来动态更新对象键。

## 还原剂

这是更新我的成员对象的缩减器。我在这里使用一个 spread 操作符来进行更新。因为我的 key 属性是 IMember 的 key，所以我可以安全地将它用作动态属性键。您经常会在“如何在 React.useState()中更新对象”教程中找到这种设计模式。第 3 行是我的两个泛型接口被利用的地方。

## JSX

每个输入都有一个匹配 IMember 对象属性的名称值。我可以从 onChange 事件中提取名称，并使用类型断言，以便我的 reducer 接受它。我可以在这里使用类型断言，因为我的表单不是动态的。

这种技术非常适合简单类型的平面对象。我发现它特别有用，因为我的组件中只需要一个函数来更新任何字段。在我开始使用这种技术之前，我的组件中的每个输入字段都有 onChange 函数。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*