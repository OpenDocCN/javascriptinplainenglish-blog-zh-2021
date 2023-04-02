# 如何在下一个 React 应用中使用道具类型

> 原文：<https://javascript.plainenglish.io/how-to-use-prop-types-in-your-next-react-app-894d55767ec3?source=collection_archive---------16----------------------->

今天，我们将看看在 React 应用程序中使用道具类型是多么容易。

![](img/b5eb0fd7aa11080e4530fbe9c8e6e27f.png)

Prop-Types 是一个有用的包，可以添加到任何不使用 TypeScript 的普通 React 应用程序中。他们将为代码库提供的价值将有益于项目，尤其是那些将增长和扩展的项目。像更容易的测试和自动完成这样的事情将会是这个包提供的巨大好处。

# 我们开始吧

我们将通过几个不同的例子来说明如何在 React 项目中使用 Prop-type。首先，我想说我将展示的只是道具类型的皮毛。关于使用道具类型的不同方法的更多细节，你可以查看下面的链接。

[](https://www.npmjs.com/package/prop-types) [## 道具类型

### React props 和类似对象的运行时类型检查。您可以使用 prop-types 来记录预期的…类型

www.npmjs.com](https://www.npmjs.com/package/prop-types) 

*关于所有这些例子，请注意:Prop-Types 是一个在运行时检查 React 组件的属性类型的库，这意味着 Prop-Types 不会阻止代码编译，并且当您检查页面时，错误消息不会显示在您的代码编辑器(例如 VS 代码)中，而是显示在浏览器的控制台中。*

所以，事不宜迟，让我们来看看几个常见的用例。

## 示例 1:一个组件有两个道具(一个可选，一个必需)

这可能是你会遇到的最常见的用例。您需要将一些简单的数据(原始类型)传递给 React 组件。在下面的代码中，我们将在道具类型中定义几个道具。其中一个将是可选的*布尔*道具，而另一个将是必需的*字符串*道具。

上面的代码中有一些需要注意的地方。首先，你会注意到我将`isVisible`设置为 false，这是因为它是可选的，这意味着我们需要考虑什么时候没有东西被传递。在这种情况下，当没有传递任何内容时，我们只是将值设置为 false。其次，您会注意到为 React 组件定义 Prop-type 是多么简单。我们需要做的就是在 PropType1 对象上定义一个名为`propTypes`的新属性。

## 示例 2:采用特定结构的 JavaScript 对象的组件

在这个用例中，我们将有一个将对象作为道具的组件。在本例中，该对象将是一个 Todo 项。

当我们为这个组件定义 Prop-Types 时，您会注意到我使用了 Prop-Types 附带的一个方法。这个方法叫做`exact`，它允许我们通过将一个对象作为参数传递给`exact`方法来定义对象的形状。我们做的和以前非常相似，除了现在 PropTypes 检查嵌套在我们对象的 exact 方法中。

## 示例 3:一个将 JavaScript 函数作为道具的组件

设置 Prop-Types 来期望一个函数作为 Prop 与任何其他 JavaScript 原始类型没有什么不同。

到目前为止，这与我们对 Prop-type 所做的任何事情的语法是相同的，但是我认为这很重要，因为在 React 中将函数向下传递给组件是非常常见的。

# 代码

所有这些例子的完整代码可以在下面的 CodeSandbox 中找到。

# 附加内容

查看下面的文章，它解释了如何使用 TypeScript 创建类型安全的 React 组件。

[](/how-to-make-your-react-components-type-safe-with-typescript-63d648d361ef) [## 如何使用 TypeScript 使 React 组件类型安全

### 您将了解到在 React 中制作类型安全的组件有多简单，以及这将对编写有多大的帮助…

javascript.plainenglish.io](/how-to-make-your-react-components-type-safe-with-typescript-63d648d361ef) 

# 包扎

prop-type 使 React 中的可测试组件编写得更健壮、更简单。它们可能会增加最初的工作量，但从长远来看是值得的，因为它们有助于制造不容易出错的组件。

和往常一样，如果你有任何关于道具类型的问题或顾虑，欢迎留下评论。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)