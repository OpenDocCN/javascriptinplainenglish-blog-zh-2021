# React 测试库概述

> 原文：<https://javascript.plainenglish.io/react-testing-library-overview-1065082563d2?source=collection_archive---------9----------------------->

一种简单易用的酶替代品

![](img/83133be85f7e28de098bd3fbd73eac15.png)

photo credit: [academy.hsoub.com](https://academy.hsoub.com/programming/javascript/react/%D8%A7%D8%AE%D8%AA%D8%A8%D8%A7%D8%B1-%D8%AA%D8%B7%D8%A8%D9%8A%D9%82%D8%A7%D8%AA-react-%D8%A8%D8%A7%D8%B3%D8%AA%D8%B9%D9%85%D8%A7%D9%84-jest-%D9%88%D9%85%D9%83%D8%AA%D8%A8%D8%A9-react-testing-library-r1138/)

## RTL 介绍

React 测试库是由软件测试大师 Kent C. Dodds 创建的。目标是为流行的 JavaScript 测试库 Enzyme 提供一个更轻量级的替代品，并消除“破坏测试库”的可能性。

肯特是良好测试实践的倡导者。他已经写了许多关于这个主题的博客文章，这些文章是公开的，也是强烈推荐的。他解释了编写可维护的测试的重要性，这意味着如果被测试的代码被重构，它们仍然会通过。我们应该测试的是功能，而不是实现。

## 设置

明确地说，React 测试库并没有消除开玩笑的必要。它不是一个测试运行程序，所以你仍然想使用 Jest，就像使用 Enzyme 一样。利用酶没有错。只是个人喜好。正如我之前提到的，RTL 给了我们同样的能力来测试我们的 React 组件，同时去掉了一些不常用的方法。如果您是 React 测试的新手，请随意查看我的[React 组件测试简介](/intro-to-react-component-testing-cd42853c06d3)，它涵盖了酶和 Jest 用法的基础知识。

如果您使用 create-react-app 构建应用程序的框架，那么 react 测试库(和 Jest)已经包含在您的依赖项中了。否则，您可以从命令行添加它。

```
npm i --save-dev @testing-library/react
```

测试文件必须以. test.js 结尾命名，以便在运行“npm 测试”时被识别为测试。这条命令将运行所有可用的测试套件。

测试本身仍然利用典型的“描述”、“测试”和“预期”块，但是 RTL 中有一些内置函数可以帮助我们模拟应用程序的预期用途和用户交互。

## 渲染、筛选和调试

渲染、屏幕和调试是常用的，可以通过在文件顶部导入它们来访问，如下所示:

```
import {render, screen, debug}
```

Render 模仿作为参数传入的组件的呈现。这必须在我们测试该组件中的任何东西之前完成。在它被渲染之后，我们可以在 screen 关键字上添加一些查询方法，这将在当前渲染的元素上执行搜索。

我们还可以对 screen 关键字使用 debug 方法。这将在您的终端中显示所有当前呈现的 HTML 元素，这样当我们执行模拟呈现时，您可以确切地看到页面在测试过程中的样子。最佳实践是在编写测试时将 screen.debug()添加到测试的末尾，以确保您知道可以从屏幕上选择什么和不可以选择什么。

## 选择/查询元素

在测试特定元素是否被正确呈现之前，我们需要找到这些元素。通过 RTL 内置的 getBy、queryBy 和 findBy 方法，查询变得很容易。使用 render 方法后，我们可以使用 screen.debug()代码片段来查看 HTML 显示的内容，并确定选择所需内容的最佳方法。

getBy 方法适用于我们希望使用传递给 render 方法的组件呈现的内容。例如，如果您希望应用程序组件立即有一个下拉菜单，您可以运行如下测试:

```
describe('App', () => { test('renders drop down menu options', () => { render(<App />); const dropdown = screen.getByRole('combobox'); expect(dropdown).toBeInTheDocument(); });})
```

通过代码编辑器中的自动完成功能，getBy 有许多变体。一些最常用的变体是 getByText 和 getByRole。如果您不确定您正在寻找的元素的角色，只需传入一个空字符串作为参数，您将看到当前呈现的 HTML 中所有可用角色的列表。

如果您需要测试某个元素不在屏幕上，您会希望使用 queryBy 方法，它包含许多相同的变体，并添加。toBeNull()位于 expect 块的末尾。以 React 测试库中的这个测试为例。

```
describe('App', () => {test('renders App component', async () => {render(<App />);expect(screen.queryByText(/Signed in as/)).toBeNull();screen.debug();expect(await screen.findByText(/Signed in as/)).toBeInTheDocument();screen.debug();});});
```

您可以看到使用了 async 和 await 关键字，因为我们正在测试用户登录后是否会显示“登录身份”文本。findByText 方法用于在异步函数执行完毕后检查所选元素是否在文档中。

## 事件模拟

当你想要假装一个动作发生时，使用 fireEvent 函数。它可以用来改变表单域的值或点击按钮。但是，在模仿用户交互时，建议使用 userEvent 函数。

这里有一个测试的例子，当点击“重新开始”按钮时，检查订单是否被清除。

```
describe('App', () => { test('clears the current order when start over is clicked', () => { render(<App />); fireEvent.change(screen.getByRole('combobox'), { target: {value: 'dinner'} }) const addButtons = screen.getAllByRole('button') fireEvent.click(addButtons[0]) const startOverButton = screen.getByText(/Start Over/) expect(startOverButton).toBeInTheDocument() fireEvent.click(startOverButton) expect(screen.queryByText(/current order/)).toBeNull() });})
```

我们首先呈现应用程序组件，将下拉菜单中的选定值更改为“晚餐”以显示菜单选项。然后我们检查“重新开始”按钮是否被呈现。最后，我们在按钮上假装一个点击动作，并测试当前订单是否被清除。

## 最后…

我希望这篇文章已经让您对最佳测试实践有了更好的理解，并介绍了一些您可以在将来的项目中使用的附加工具。有大量关于 React 测试库用例的文档、教程和博客。如果您通常使用 Enzyme，我鼓励您查看下面的资源，尝试一些不同的东西。你会很高兴你做了！

[RTL 官方文件](https://testing-library.com/docs/)

[RTL 小抄](https://testing-library.com/docs/react-testing-library/cheatsheet/)

[肯特·多德初级教程](https://www.robinwieruch.de/react-testing-library)

[RTL 博文简介](https://kentcdodds.com/blog/introducing-the-react-testing-library)

[FreeCodeCamp RTL 教程](https://www.freecodecamp.org/news/react-testing-library-tutorial-javascript-example-code/)

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)