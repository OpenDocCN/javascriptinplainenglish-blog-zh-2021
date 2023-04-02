# 反应和打字稿:基础

> 原文：<https://javascript.plainenglish.io/react-and-typescript-the-basics-a7bb6625282c?source=collection_archive---------4----------------------->

*通过设置一个习惯跟踪应用程序，了解如何使用 React 实现脚本语言。*

![](img/1d06aad0a9dd6c87d39a4f699383c841.png)

Photo by [Prophsee Journals](https://unsplash.com/@prophsee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在了解到 2020 年第二大最受欢迎的编程语言是 TypeScript 之后，很自然地，对于像我一样发现 TypeScript 的许多早期 JavaScript 开发人员来说，这个问题本身就是*工程师是否以及*如何将它与第二大最受欢迎的[JavaScript 框架/库(又名 React)一起使用。](https://insights.stackoverflow.com/survey/2020#most-loved-dreaded-and-wanted)

社区中的许多人认为这两者可以很好地结合在一起；一个开发者给出了一个[解释](https://fettblog.eu/typescript-react/)为什么:

> JSX 是句法糖。你打开并传递属性的每个 JSX 元素，只不过是 React(或 Preact 或 Vue 或 Dojo…你能想到的)中的一个函数调用。这给了我们 TypeScript 一个很大的优势:JavaScript 可以被解析、理解和评估。这意味着您可以获得 TypeScript 提供的所有工具和编译优势。缺少必需的属性？TypeScript 会告诉你！在某处有一个错别字:你会发现。不知道您需要哪些属性？自动完成拯救！

为了得到一个更实用的方法，我决定制作一个迷你习惯跟踪器应用程序(Rails 在后端，React 在前端)来感受一下这种集成是如何进行的。

# 基础知识

我通常使用 Create React App 来启动并运行一个新的 React 项目，事实证明，CRA [文档](https://create-react-app.dev/docs/adding-typescript/)提供了对 TypeScript 的支持。

## **用类型脚本启动一个新的 react 应用:**

```
npx create-react-app my-app --template typescript# oryarn create react-app my-app --template typescript
```

确保将`my-app`替换为您的应用程序/前端文件夹的预期名称。

( [Gatsby](https://www.gatsbyjs.com/docs/how-to/custom-configuration/typescript/) 和 [NextJS](https://nextjs.org/learn/excel/typescript) 也为静态站点 app 提供了类型脚本的支持。)

一旦我的 React 应用程序编译完成，在我的`App`组件中，我开始使用一个`useEffect`钩子和一个获取 API 来加载我想要呈现到页面的数据(来自我后端的日常习惯)，并使用`useState`钩子将我的获取响应设置为等于`habits`的状态。

然后，我将这个状态作为一个名为`dailyHabits`的道具传递给我的`Main`子组件。

## 正确类型和功能组件

对于接受 props 的函数组件，创建一个 ***类型别名*** 或 ***接口*** ，描述子组件正在接收的属性的形状。

* *类型别名和接口之间的区别是微妙的，但是来自 TypeScript 和 React [cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example) 的这个片段提供了一个经验法则:

> 创作库或第三方环境类型定义时，始终使用`*interface*`作为公共 API 的定义，因为这允许消费者在缺少某些定义时通过 ***声明合并*** 来扩展它们。
> 
> 考虑使用`*type*`作为你的 React 组件属性和状态，为了一致性，因为它更受约束。

(接口允许声明合并，即稍后添加属性，而类型别名不允许)。

在我的`Main`子组件中，我首先如下定义属性:

因为`dailyHabits`是一个对象数组，注意我们在结尾`}`后使用`[]`来表示。

**** *常见的道具类型*** 在 React 和 TypeScript [cheatsheet](https://react-typescript-cheatsheet.netlify.app/docs/basic/getting-started/basic_type_example) 中列出，但是作为道具传递的 React/TypeScript 应用程序的其他常见类型包括函数(例如 onClick 或 onChange)，可以定义如下:

```
*// function that doesn't take or return anything (VERY COMMON)* onClick: () => *void*;*//function with named prop (VERY COMMON)*onChange: (id: number) => *void*;
```

声明函数组件最简单的方法是将 props 作为一个参数，并在后面加上一个冒号和已经定义的类型别名或接口，如下所示:

然后推断出返回类型。在这个阶段，`React.FunctionComponent`或`React.FC`经常出现在代码库中，但是一般[不鼓励](https://github.com/facebook/create-react-app/pull/8177)使用，应该避免使用。

对于类组件来说，这个过程有点不同 cheatsheet 再次为声明类型提供了清晰性。

## 通过道具映射

接下来，我想映射我的`dailyHabits`道具，并将每个对象元素向下传递给一个`Habit`子组件，但是需要先对数组中的每个子组件进行类型检查。由于每个子对象都是一个对象本身(而不是一个对象数组)，它的形状与`dailyHabits`不同，所以我们必须首先声明类型别名:

从那里，类似于声明一个函数组件，我们用类型别名隐式定义每个子元素:

`*{…h}*` *这里是分配道具的简写——类似于写* `*key=h.id*` `*name=h.habit.name*` *等等(每个属性都通过* `*props*` *传递和访问)。*

在我的`Habit`组件中，因为我接受了那个道具，所以我也需要在那里声明形状，首先分配一个类型别名，这将是用于在 map 函数中对每个孩子进行类型检查的同一个别名:

在两个组件中编写相同的类型别名有点重复——相反，一种选择是将其包含在一个单独的文件中，将其作为变量导入，并在父映射函数和子函数组件声明中引用该变量。

每个日常习惯现在都可以成功地呈现在屏幕上，然而，这个应用程序缺少一些基本的功能，比如检查一天的习惯或添加一个全新的习惯。

在我的下一篇博客中，我将(试图)为初学者演示如何处理这些类型的事件和类型检查。

## 更多资源:

*   [打字稿备忘单](https://react-typescript-cheatsheet.netlify.app/)
*   [打字稿和反应指南](https://fettblog.eu/typescript-react/)

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)