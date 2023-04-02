# 在 React 中开始使用可选的链接和无效合并

> 原文：<https://javascript.plainenglish.io/start-using-optional-chaining-and-nullish-coalescing-in-react-322bdf24b78c?source=collection_archive---------4----------------------->

## 在 React 中使用 nullish 合并和可选链接并使您的代码库更上一层楼所需要知道的一切。

![](img/1c84569711dd5c85036f236d0b701cfb.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

自从我开始在 React 中开发以来，我注意到大多数在线代码片段和教程是如何避免可选的链接操作符以及 nullish 合并操作符的。虽然它们是相当新的创新，但已经有一年多的历史了。

所以，我认为这背后的原因是缺乏关于它们是什么，如何开始使用它们，如何使用，为什么使用以及何时使用的教育。让我们试着解决所有这些问题。

# 它们是什么

让我们根据 [MDN Web 文档](https://en.wikipedia.org/wiki/MDN_Web_Docs)来看看可选的链接操作符和 nullish 合并操作符的定义。

## [可选链接](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

> 可选的链接操作符(`**?.**`)使您能够读取一个位于连接对象链深处的属性值，而不必检查链中的每个引用是否有效。
> 
> `?.`操作符类似于`.`链接操作符，除了当引用为 [nullish](https://developer.mozilla.org/en-US/docs/Glossary/Nullish) ( `[null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)`或`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`)时，表达式不会导致错误，而是用返回值`undefined`短路。当用于函数调用时，如果给定的函数不存在，则返回`undefined`。— [MDN 网络文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

## [无效合并](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Nullish_coalescing_operator)

> **无效合并运算符(** `**??**` **)** 是一个逻辑运算符，当其左侧操作数为`[null](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/null)`或`[undefined](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/undefined)`时，返回其右侧操作数，否则返回其左侧操作数。— [MDN 网络文档](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

# 如何启用它们

这两个操作符都正式发布了 [ECMA-262 第 11 版](https://262.ecma-international.org/11.0/) JavaScript 语言规范。因为这些都是相当新的特性，所以只有 React 的某些版本支持它们。

为了使用它们，必须满足以下要求:

*   [巴别塔≥ 7.8.0](https://babeljs.io/blog/2020/01/11/7.8.0)
*   [创建 React App ≥ 3.3.0](https://github.com/facebook/create-react-app/blob/main/CHANGELOG-3.x.md#330-2019-12-04)

另外，TypeScript 开发者要求 [TypeScript ≥ 3.7](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html) 。

# 如何使用它们

让我们看看使用这两个操作符所需的语法。

## 可选链接

```
obj.val?.prop // default use
obj.val?.[expr] // [optional chaining with expressions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining#optional_chaining_with_expressions)
obj.arr?.[index] // [array item access with optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining#array_item_access_with_optional_chaining)
obj.func?.(args) // [optional chaining with function calls](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining#optional_chaining_with_function_calls)
```

## 无效合并

```
leftExpr ?? rightExpr // default use
```

# 为什么以及何时使用它们

让我们看看为什么 JavaScript 引入了这两个操作符，以及何时应该使用它们来利用它们的优势。

## 可选链接

在用 JavaScript 开发时，您经常需要从树状结构中访问深度嵌套的属性。常见的解决方案是编写一个长长的属性访问链。问题是，如果链中的任何中间引用是`null`或`undefined`，JavaScript 将抛出一个`*TypeError: Cannot read property ‘name’ of undefined*`错误。

因此，您可能最终会编写自定义逻辑来避免这种情况发生。这段代码不仅难看，还会降低代码库的可读性。这就是引入可选链接操作符的原因。

在可选链接之前，您必须编写如下代码:

```
if (obj && object.property1 && object.property1.property2)
   object.property1.property2.toLowerCase();
```

通过可选的链接，您可以用一行更简洁、可读性更好的代码实现相同的结果:

```
obj.property1?.property2.toLowerCase()
```

这只是一个简单的例子，但是你可以在这里找到更深入的指南。

另外，记住可选的链接操作符只对声明的变量有效。如果没有`obj`变量，那么就会抛出一个`ReferenceError`错误。

此外，您应该只对可选属性和变量使用`?.`。这意味着如果根据你的编码逻辑`obj`变量必须存在，但是`property1`属性是可选的，你应该写`obj.property1?.property2`。

## 无效合并

当您需要一个变量有一个默认值时，您可以考虑使用 OR 运算符(`[||](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_OR)`)，如下所示:

```
let value;
let defaultValue = value || 'Hello World!';
```

这可能会变成一个很难发现的错误。实际上，`||`是一个布尔逻辑运算符。因此，在求值期间，左边的操作数会自动转换为布尔值。这意味着，如果左侧操作数是任何 JavaScript *falsy* 值(`0`、`''`、`NaN`、`null`、`undefined`)，则不会返回默认值。

引入 nullish 合并运算符是为了解决这个问题。事实上，它通过仅在第一个操作数计算为`null`或`undefined`时返回第二个操作数(但没有其他 *falsy* 值)来避免这个缺陷:

```
const nullValue = null;
const emptyText = ""; // falsy
const aNumber = 42;

const val1 = nullValue ?? "Default Value 1";
const val2 = emptyText ?? "Default Value 2";
const val3 = aNumber ?? 0;

console.log(val1); // "Default Value 1"
console.log(val2); // "" (as the empty string is not null or undefined)
console.log(val3); // 42
```

这只是一个简单的例子，但是你可以在这里找到更深入的指南。

# 奖金

您可能还对以下内容感兴趣:

[](/avoid-the-fear-of-refactoring-with-absolute-imports-in-react-804bce61dc31) [## 避免对 React 中绝对导入的重构的恐惧

### 在 React 中使用绝对路径别名使导入易于重构

javascript.plainenglish.io](/avoid-the-fear-of-refactoring-with-absolute-imports-in-react-804bce61dc31) [](https://betterprogramming.pub/how-to-avoid-bottlenecks-in-node-js-applications-8085d86b6b2e) [## 如何避免 Node.js 应用程序中的瓶颈

### 配置 Sequelize 和 Mongoose 来处理并发的数据密集型请求

better 编程. pub](https://betterprogramming.pub/how-to-avoid-bottlenecks-in-node-js-applications-8085d86b6b2e) [](https://codeburst.io/avoiding-code-duplication-by-adding-an-api-requests-definition-layer-in-javascript-6e5d7b409896) [## 通过在 JavaScript 中添加 API 层来避免代码重复

### 使用基于 Promise 的 HTTP 客户端构建 API 层

codeburst.io](https://codeburst.io/avoiding-code-duplication-by-adding-an-api-requests-definition-layer-in-javascript-6e5d7b409896) 

# 结论

今天我们看了什么是可选的链接和无效合并操作符，如何使用它们，为什么和在哪里使用。尽管它们在一年前就在 JavaScript 中引入了，但许多开发人员仍然没有尝试过它们。这是因为它们仍然是一个相当新奇的事物，需要通过教育来了解开始采用它们所需的一切，而这正是本文的目的。

感谢阅读！我希望这篇文章对你有所帮助。请随意留下任何问题、评论或建议。

*更多内容看*[***plain English . io***](http://plainenglish.io/)