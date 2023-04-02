# 样式组件快速入门

> 原文：<https://javascript.plainenglish.io/a-quick-start-to-styled-components-5ac5f9349160?source=collection_archive---------14----------------------->

## 第 2 部分:向应用程序添加动态样式

![](img/b38291d9e26a51101bbf6931d4881f42.png)

Photo by [Rodrigo Santos](https://www.pexels.com/@rsantos1232?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/workplace-with-modern-laptop-with-program-code-on-screen-3888151/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

如果您刚刚开始在 React 应用程序中实现样式化组件，并且想知道为什么要花时间学习这个库，那么您来对地方了！

在应用程序中使用样式化组件将允许您添加更多的功能，并且更容易定制您选择添加的样式。

如果您对样式化组件完全陌生，或者希望开始使用这个库，我强烈建议您首先阅读"[样式化组件快速入门](https://medium.com/geekculture/a-quick-start-to-styled-components-3b6fd1f776eb)"在那篇文章中，我回顾了关于这个库的一些一般信息，以及如何开始在应用程序中使用样式化组件。

在本文中，我计划介绍一些更高级的(尽管是必要的)样式组件特性，这些特性将为您的应用程序提供更健壮的样式体验。我将把[传递道具](https://reactjs.org/docs/components-and-props.html)覆盖到你的样式化组件中，使用状态来动态呈现样式，并添加或样式化[伪类](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)。

为了演示这三个特性，我将使用一个非常简单的 React 应用程序，它由一个按钮组成。该按钮将在亮模式和暗模式之间切换应用程序。

# 将道具传递给样式化组件

正如在“[样式化组件快速入门](https://medium.com/geekculture/a-quick-start-to-styled-components-3b6fd1f776eb)中提到的，使用样式化组件的乐趣之一是能够将属性传递给组件，以便动态地将样式呈现到应用程序中。通过传入道具，您可以将组件作为模板重用，同时能够根据传入的任何道具来更改呈现的样式。更强大的是，由于您可以根据传入的属性来更改样式，因此您还可以根据组件和应用程序中不断变化的状态来更改应用程序的设计。稍后，您将在我们的亮模式与暗模式示例中更好地看到这一点。

为了通过 props 更新组件的样式，您需要使用 JavaScript 的字符串插值语法和回调函数。例如，如果您确定每个重要的标题都有一个蓝色的字体颜色，我们称之为原色，其他的标题颜色都是红色，那么您可以向样式化的标题传递一个名为 primary 的属性来动态地呈现它。我们将这样实现它:

```
**import** styled **from** "styled-components"**const** StyledTitle = styled.h1`
   font-color: ${(props.primary) => props.primary ? "blue" : "red"
`**export** **default** **function** App() {
   **return** (
      <div>
         *//This will display a Blue Title*
         <StyledTitle primary={true}> Important Title </StyledTitle>
         *//This will display a Red Title*
         <StyledTitle primary={false}> Other Title </StyledTitle>
      </div>
   );
}//Note: You could have made use of object destructuring in the 
//callback function like this: 
//font-color: ${({primary}) => primary ? "blue" : "red"
```

# 使用状态动态呈现样式

既然您已经知道了如何使用 Props 来控制样式化组件中呈现的样式，现在是讨论如何使用 State 来显示不同样式的好时机。这样做就像将状态作为道具传递给样式化组件一样简单。由于状态随着应用程序中数据的变化而变化，我们可以使组件中的样式依赖于变化的状态。

为了演示这一点，我将创建一个非常简单的 react 应用程序，它由一个标题和一个按钮组成。该按钮将在 true 和 false 之间切换我们的`lightMode`变量的状态。最初，`lightMode`将被设置为`true`，我们的应用程序将有一个黑色文本的白色背景。当你点击按钮时，`lightMode`将被设置为`false`，使我们的应用程序进入“黑暗模式”，这将改变应用程序的背景为灰色，蓝色文本。

请使用下面的 [CodeSandbox](https://codesandbox.io/) 来查看代码，并把状态传递给你的样式化组件。

# 向样式化组件添加伪类/元素

既然您已经了解了如何将动态样式添加到 React 应用程序中，您可能想知道样式化组件是否考虑了伪类或伪元素。请放心，您仍然可以使用样式化组件将伪类和元素添加到样式中。

如果你从未听说过伪类，这里有一个由 [MDN Web Docs:](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements) 给出的简要描述

> [“伪类是一个选择器，它选择处于特定状态的元素，例如，它们是其类型的第一个元素，或者它们正被鼠标指针悬停。它们往往表现得好像您已经将一个类应用到了文档的某个部分，通常帮助您减少标记中多余的类，并为您提供更加灵活、可维护的代码。](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)

在样式化组件中添加伪类与在 CSS 样式表中添加伪类相对相似。要添加伪类，您需要做的就是添加`&:`和伪类的名称，后跟包含您的样式的`{}`。继续上面的重要标题和不重要标题的例子，如果我想让“重要标题”在悬停时变成紫色，让“不重要标题”在悬停时变成黄色，我可以在代码中添加下面的伪类。

```
**import** styled **from** "styled-components"**const** StyledTitle = styled.h1`
   color: ${({primary}) => primary ? "blue" : "red"
   *//This will add the pseudo-hover class to your headers*
   &:hover {
     color: ${({primary}) => primary ? "purple" : "yellow"
   }
`**export** **default** **function** App() {
   **return** (
      <div>
         *//This will display a Blue Title that changes to purple*            
         //on hover
         <StyledTitle primary> Important Title </StyledTitle>
         *//This will display a Red Title that changes to yellow
         //on hover*
         <StyledTitle> Other Title </StyledTitle>
      </div>
   );
}
//Note: Passing in primary is the same as primary={true} and leaving
//primary out all together is the same as primary={false}
```

当然，我们也可以通过为我们的道具传入状态来做到这一点。请使用下面的 [CodeSandbox](https://codesandbox.io/) 来查看代码，并尝试将状态传递给你的样式化组件，以动态呈现伪类。

# 结论

现在你已经学会了如何给你的样式组件添加更多的功能，你已经准备好让你的 React 样式更上一层楼了！使用 props 和 state，您现在可以动态地改变 React 应用程序的外观和感觉。

尽管如此，我还没有介绍样式化组件的许多特性。我建议查看 CSS 函数以及 ThemeProvider 组件。我邀请您进一步探索这个宏伟的库，并在设计您的应用程序时尽可能多地尝试。

编码快乐！

# 有用的资源

*   https://styled-components.com/
*   [https://developer . Mozilla . org/en-US/docs/Learn/CSS/Building _ blocks/selector/Pseudo-classes _ and _ Pseudo-elements](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors/Pseudo-classes_and_pseudo-elements)
*   [https://github.com/styled-components/styled-components](https://github.com/styled-components/styled-components)
*   [https://www.youtube.com/watch?v=c5-Vex3ufFU&t = 4s](https://www.youtube.com/watch?v=c5-Vex3ufFU&t=4s)

*更多内容请看*[***plain English . io***](http://plainenglish.io/)