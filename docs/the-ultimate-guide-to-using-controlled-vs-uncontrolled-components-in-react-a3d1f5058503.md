# React 中使用受控和非受控组件的终极指南

> 原文：<https://javascript.plainenglish.io/the-ultimate-guide-to-using-controlled-vs-uncontrolled-components-in-react-a3d1f5058503?source=collection_archive---------7----------------------->

在这篇文章中，我们将从理论和实践两个方面来看看在 React 中使用受控或不受控组件的区别。我们将尝试看看使用其中一种来对抗另一种的好处，以及一些初学者可能陷入的陷阱。如果你不熟悉 React 组件，我建议你看一下 React 官方文档和教程。

![](img/b4b79289d7df237ce948d04daaea3560.png)

Not all uncontrolled things are cute

关于 React 中受控和不受控输入的争论可以在新 web 开发人员的旅程中很早就开始。您可能会遇到很多文章说一种方法比另一种方法更好，这可能是真的，取决于用例。看起来受控组件在 React 社区得到了广泛的推荐，而且理由很充分。甚至在[非受控部件的官方文件](https://reactjs.org/docs/uncontrolled-components.html#:~:text=In%20a%20controlled%20component%2C%20form,form%20values%20from%20the%20DOM.)中，第一句话就是:

> 在大多数情况下，我们建议使用[控制组件](https://reactjs.org/docs/forms.html#controlled-components)来实现表单。

因此，让我们深入这个主题，了解这两种方法之间的区别。为了能够做到这一点，我们需要回忆一下 DOM 是什么。

## **好的 DOM，坏的 DOM 和丑陋的 DOM**

DOM 是处理 HTML 和 XML 文档的接口。它表示一个树状结构的文档。它是浏览器用来组织如何在网页上向用户显示元素的主要工具。您可以通过检查页面来访问任何网页的 DOM。你会看到 HTML 元素，如 div、文本字段、按钮和图像，它们以树形结构组织:它们有父元素、子元素和兄弟元素。实际上，DOM 中的这些家族关系转化为网页上的位置关系。

DOM 与 HTML 非常相似，但与网页的 HTML 源文档并不完全相同。您可以自己检查一下:检查页面 DOM 和查看页面源代码可能会有很大的不同。您可能会在 DOM 中找到在源代码中找不到的元素，反之亦然。这是因为 HTML 元素可以由 Javascript 创建、删除和修改。例如，单击页面中的按钮可以使 HTML 源文件中不存在的图像出现。但是，您会在 DOM 中找到这个图像。

简而言之，你在网页上找到的所有元素都存在于 DOM 中。网页上的 Javascript 动态修改 DOM，修改会立即反映在屏幕上。

Javascript 控制 DOM 的能力给了我们在受控组件和非受控组件之间进行选择的机会。

受控组件或输入是其值依赖于组件的反应状态的组件，而非受控组件是其值被直接控制或存储在 DOM 中并且只能从 DOM 访问的组件。

为了更好地理解这种差异，让我们来看看以受控和非受控方式实现的同一个表单。

## **非受控输入示例**

这是一个不受控制的文本输入的例子。它是不受控制的，因为第 10 行输入包含的值不受 Javascript 控制。这意味着没有代码告诉 DOM 给这个 input 元素一个特定的值。

因此，当用户在这个输入中书写时，文本被存储在 DOM 中。为了能够在 React 应用程序中使用它，开发人员需要从 DOM 中提取它。这可以使用`ref`属性来完成。

## **受控输入示例**

在这个受控实现的例子中，您可以看到我们的输入元素的`value`被 React 设置为总是等于状态变量`name`。实际上，当用户在文本输入中输入时，处理程序`onChange`被触发，并将调用函数`handleNameChange`，变量`event`包含输入的文本。该函数将文本存储在状态变量`name`中。由于`name`与输入的`value`属性相关联，因此这些更改将反映在页面的输入框中。

## **只需选择一个并在您的应用中采用它**

那么应该用哪一个呢？嗯，如果你真的明白你在做什么，这两者都很好。只要有可能，你可以尝试使用受控组件，因为它给你的表单提供了更多的灵活性。这两种方法都允许您至少检索一次输入，并在提交时验证它。除此之外，受控组件还能够:

*   即时现场验证
*   有条件地禁用提交按钮
*   强制输入格式
*   一条数据的多个输入

## **运行时在受控和非受控之间切换**

即使您以受控的方式编写输入表单，React 实际上也可以自动切换到不受控的行为，将输入值存储在 DOM 中。您将在 web 控制台中看到以下错误:

```
**Warning**: A component is changing a controlled input of type text to be uncontrolled. Input elements should not switch from controlled to uncontrolled (or vice versa). Decide between using a controlled or uncontrolled input element for the lifetime of the component.
```

例如，当控制输入属性的状态变量变为`undefined`时，就会发生这种情况。这通常是由于开发错误。原则上，绑定到输入值的变量永远不应该是未定义的。如果状态变量在逻辑上不包含任何内容，用空字符串`''`替换`undefined`。

受控组件和非受控组件之间没有优先选择。初学者可能会发现不受控制的组件更容易处理，因为它们的实现类似于 HTML。但是一旦你对 React 有了更多的经验，我建议你转向受控组件。

如果您有兴趣将 React 应用程序迁移到生产环境中，请查看以下指南:

[](https://medium.com/swlh/react-and-node-js-build-a-full-stack-app-from-development-to-production-in-5-minutes-a03bc019df6b) [## React 和 Node.js:在 5 分钟内构建从开发到生产的全栈应用

### 在本文中，我将向您展示如何创建一个从开发到生产的全栈 Web 应用程序。我将展示…

medium.com](https://medium.com/swlh/react-and-node-js-build-a-full-stack-app-from-development-to-production-in-5-minutes-a03bc019df6b) 

要了解关于 Webpack 的更多信息，web pack 是现代 Javascript 技术的支柱，请看下面的教程:

[](https://levelup.gitconnected.com/the-ultimate-webpack-tutorial-understanding-the-wizard-behind-the-magic-of-modern-javascript-a0efd12a2cdc) [## 终极 Webpack 教程:理解现代 Javascript 魔力背后的向导

### 在本文中，我们将了解什么是 webpack，以及它的魔力如何革新了 Javascript 库和框架，如…

levelup.gitconnected.com](https://levelup.gitconnected.com/the-ultimate-webpack-tutorial-understanding-the-wizard-behind-the-magic-of-modern-javascript-a0efd12a2cdc) 

有关 Refs 和 DOM 的更多信息，您可以查看 React 官方文档中的[这篇文章](https://reactjs.org/docs/refs-and-the-dom.html)。