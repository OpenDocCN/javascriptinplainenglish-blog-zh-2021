# 如何对 TypeScript 和 React 使用可选的链接和 Nullish 合并

> 原文：<https://javascript.plainenglish.io/how-to-use-optional-chaining-and-nullish-coalescing-with-typescript-and-react-1d43d0cf9c34?source=collection_archive---------11----------------------->

## 如何在 TypeScript 和 React 中正确使用可选的链接和 Nullish 合并

![](img/d52ba4b13b671b2a192f91cf08a9abaa.png)

Photo by [Guillaume de Germain](https://unsplash.com/@guillaumedegermain?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

我们试图解决的问题是:你是否曾经在一个对象中有一个深度嵌套的属性，当你任何时候引用它的时候都会返回 null，因为它在你的代码运行之前没有足够快地被定义？通常使用 API 调用，但不限于。根据属性的深度，你必须写一些难看的 if 语句来防止错误？这就是我们今天要用可选链接解决的问题。

# 可选链接

正如简介中简要讨论的，可选链接中的明星是新的**(?。)**操作符，它使您能够捕获位于连接对象链深处的属性值，而无需检查链中的每个属性是否有效。

在可选的链接访问一个深度嵌套的属性之前，你必须这样做。

```
if(object && object.property && object.property.nextProperty) {setProperty(object.property.nextProperty.finalProperty)}
```

通过可选的链接，您现在可以通过这个简单的加法去掉所有的代码。

```
setPropert(object.property.nextProperty?.finalProperty)
```

**(？。)**符类似于常用的**(。)**运算符如果嵌套属性的值或引用为 nullish (null 或 undefined ),则表达式不会创建错误，而是返回 undefined 值。

如果给定的函数不存在，也可以在函数中使用可选链接来返回 undefined。

当在链式属性中访问引用时，引用可能会丢失，这会导致表达式变得更短、更简单。

当你在探索一个对象，而他们不能保证需要什么属性时，这也是有帮助的。

最后但同样重要的是，如果需要，可以使用多个可选的链接操作符。

```
object.property?.nextProperty?.finalProperty
```

# 无效合并

该节目的下一个明星是 nullish 合并运算符**(?？)**。当左边的操作数为空或未定义时，该逻辑运算符返回右边的值。你和我想的一样吗？这将与可选链接完美配合。

```
object.person?.details?.car ?? "Person Has No Car"
```

与更常用的运算符相比，如果操作数是任何假值，而不仅仅是 null 或 undefined，则逻辑 OR **(||)** 返回右边的值。为了更清楚地说明这一点，如果您使用逻辑 OR 操作符来提供一个默认值，那么如果您认为某些 falsy 值是可用的(例如:“or 0”)，您可能会遇到意外的行为。

我们来做一个例子，右边的值等于 0。

```
let count = 0;let orOperand = count || 42;let nullishOperand = count ?? 42; console.log(orOperand)console.log(nullishOperand);result-
logical OR: 42
nullish coalescing: O
```

你可以在这个例子中看到 nullish 合并操作符，因为计数不是未定义的或者空的，它返回左边的值。其中使用逻辑或 see 的 0 作为 falsy 值，并返回右边的值。

现在让我们做一个例子，右边的值是未定义的。

```
let count = *undefined*;let orOperand = count || 42;let nullishOperand = count ?? 42;console.log(orOperand)console.log(nullishOperand);result-
logical OR: 42
nullish coalescing: 42
```

这提供了一个清晰的例子，说明零化合并是多么有益。

# React 和 TypeScript 示例

在 Reactjs 和 TypeScript 的世界中，这在很多方面都是有帮助的，我想提供一个类型化接口对象的例子，我们有时希望它为空。

然后用这些类型创建一个对象，并将值作为 null 传递。

在 console.log()中，您可以期望它返回默认值“主浴室未知”。

我希望这有助于您了解如何使用这两个惊人的 JavaScript 特性，使您的代码与任何空值或未定义值的默认值相似但更健壮。

## **重要提示**

还需要注意的是，由于这些是较新的 JavaScript 特性，所以只有 React 和 TypeScript 的某些版本支持它们。

最新的 [ECMAScript (ECMA-262)](https://tc39.es/ecma262/#prod-OptionalExpression) 是这些特性被引入的时候。

支持范围:

*   **打字稿 3.7**
*   **巴别塔 7.8.0**
*   **创建 React App** **3.3.0**

## 结论

再次感谢阅读！我喜欢提供这样的文章和指南来帮助社区。如果他们有你想看的主题或话题，请随意联系！

看看我其他一些受欢迎的文章:

[](/how-to-create-an-animated-countdown-timer-with-framer-motion-and-react-75035d13309c) [## 创建一个动画倒计时定时器与帧运动和反应

### 一个指南，建立自己的动画倒计时定时器与帧运动，反应，并使用倒计时钩。

javascript.plainenglish.io](/how-to-create-an-animated-countdown-timer-with-framer-motion-and-react-75035d13309c) [](/password-validation-using-react-and-typescript-5230079dff89) [## 使用 React 和 TypeScript 进行密码验证

### 了解如何使用 React 挂钩和 TypeScript 验证密码

javascript.plainenglish.io](/password-validation-using-react-and-typescript-5230079dff89) [](https://medium.com/@steven_creates/how-to-use-react-hooks-usecontext-and-usereducer-with-typescript-f616067248dd) [## 如何将 React 挂钩 useContext 和 useReducer 与 TypeScript 一起使用

### 在这篇指南+文章中，我们将通过 reactions use context hook 来设置 typescript 的用法…

medium.com](https://medium.com/@steven_creates/how-to-use-react-hooks-usecontext-and-usereducer-with-typescript-f616067248dd) 

*更多内容请看*[***plain English . io***](https://plainenglish.io/)