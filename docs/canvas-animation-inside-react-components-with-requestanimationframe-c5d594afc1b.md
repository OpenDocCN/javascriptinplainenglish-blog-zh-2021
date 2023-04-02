# 带有 requestAnimationFrame 的 React 组件内的画布动画

> 原文：<https://javascript.plainenglish.io/canvas-animation-inside-react-components-with-requestanimationframe-c5d594afc1b?source=collection_archive---------0----------------------->

![](img/8927c012d4da23a483bae636ce7b8d09.png)

Photo by [Hans Eiskonen](https://unsplash.com/@eiskonen?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

本文的相关源代码可以在 [**GitLab**](https://gitlab.com/gvanderput/react-canvas-component) 上找到🙂

## 介绍

如果你熟悉 **HTML 画布元素**，你就会知道制作动画相对容易。我们向 DOM 添加一个 canvas 元素，并借助于[**requestAnimationFrame**](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame)递归调用一个渲染函数。render 函数操纵画布的上下文，可以添加形状、图像、文本等。

```
const ctx = canvas.getContext('2d');
```

根据你使用的浏览器和渲染函数的重量，它每秒执行 60 次。

**但是，如果您想在 React 组件中制作这样的动画，该怎么办呢？**

这带来了一些挑战。我们当然不想每秒 60 次重新渲染 React 组件。让我们来看看解决方案。

## 画布组件

我们将创建一个单独的(功能性的)React 组件，它使用三个 [useRef 钩子](https://reactjs.org/docs/hooks-reference.html#useref)来帮助我们实现目标。

让我们从基础开始:

在第 7 行，我们将 *canvasRef* 传递给画布元素。这是 **useRef** 的常见用例，但不是 *only* 用例，我们很快就会发现。

通过这样做，我们将能够在我们的 DOM 中访问对*canvas 元素的引用，以便我们稍后能够访问它的 2D 绘图上下文。*

但是什么是 useRef 钩子，它做什么？

如果你已经熟悉 useRef 钩子，可以跳过下一段。

## useRef

根据 reactjs.org 上的文档:

> useRef 返回一个可变的 Ref 对象。当前属性被初始化为传递的参数(initialValue)。返回的对象将在组件的整个生存期内保持不变。

因此对 useRef 的调用将返回一个*可变对象*。这意味着我们可以改变。没有意外行为或副作用的当前属性。事实上，我们可以**改变那个值**，它将**不会导致我们组件的重新提交**。文件中的另一段引文:

> 请记住，useRef 不会在内容发生变化时通知您。变异了。当前属性不会导致重新呈现。

在某种程度上，这就像一个**规则*让*变量**。但是 T4 有一个很大的不同。每当我们的组件*由于其他外部因素*重新呈现时，useRef 调用返回的值总是对同一个对象的引用(因此是值):

> useRef()和自己创建一个{current: …}对象的唯一区别是 useRef 会在每次渲染时给你相同的 Ref 对象。

好吧。因此，通过使用 useRef，我们可以:

*   将值存储在对象中
*   我们可以在任何时候操作该值，而不会导致组件的重新呈现
*   在每个重新呈现器上访问相同值

说到画布动画，听起来对我很有用🙂让我们找出答案。

## 开始播放动画

让我们通过开始动画循环来更新我们的组件:

在第 17 行，我们调用 useEffect，通过传递一个空数组作为第二个参数，它将表现得像一个老式的***componentdidmount***方法。作为第一个参数传递的函数将只执行一次:在我们的 Canvas 组件被 React 添加到 DOM 之后。

这就是我们开始制作动画的时间:

```
requestAnimationFrame(tick);
```

每当浏览器准备就绪时，这将简单地调用第 11 行定义的 tick 函数(关于 requestAnimationFrame 的具体行为的更多信息可以在 [MDN](https://developer.mozilla.org/en-US/docs/Web/API/window/requestAnimationFrame) 找到)。实际上，它会立即调用 tick 函数。

> *“滴答”是在动画*的一帧中执行的逻辑的常用术语。

在 *tick* 中，我们渲染我们的帧(第 13 行),并再次递归调用 tick 函数(第 14 行)。现在忽略第 12 行的突破检查。

## 渲染框架

renderFrame 的内容是隐藏的(故意的)。关于**渲染细节**，我请参考 GitLab 上的[库](https://gitlab.com/gvanderput/react-canvas-component)，因为我相信它与本文无关。简而言之，它所做的就是更新我在演示中制作的球的某些属性，然后在画布上绘制这个球。

虽然有一件事很重要。我制作的球是有属性的(比如它的位置和速度)。这些属性存储在一个名为“球”的对象中。因为我们希望在重新呈现器之间保持这些属性，*并且因为我们希望能够在不导致 React 组件*重新呈现的情况下操作这些值，所以我们将球对象存储在我们之前描述的 **ref 容器**中:

```
const ballRef = useRef({ x: 50, y: 50, vx: 3.9, ... });
```

稍后，我们再次访问球值:

```
const ball = ballRef.current;
// ball.x === 50
```

如果你感兴趣的话，可以看看 Canvas.jsx 里面的函数 *updateBall* 和文件 *frameRenderer.js* 。

## 碎片帐集

我们的动画正在运行，并且表现良好。但是，如果我们的 React 组件(Canvas 组件)从 DOM 中移除了，会怎么样呢？如果是 ***卸装*** 呢？动画逻辑(tick 函数的执行)将继续运行。

我们必须自己清理。

实际上，我前面提到的 tick 函数中第 12 行的中断已经阻止了动画在组件卸载后继续运行:

```
if (!canvasRef.current) return;
```

这样做的原因是，当组件被卸载时，我们将丢失画布引用(它的值将变成 ***null*** )。

但是我们**无论如何都应该进行一次适当的专门清理**,原因有二:

*   这是个好习惯。默认情况下，垃圾收集和**防止内存泄漏**应该是开发人员必备技能的一部分。
*   当使用 CRA 和捆绑的*热重新加载*(例如，执行“纱线运行启动”时启动的开发环境)时，无论何时组件被“热重新加载”，都会启动一个新的动画循环，这将导致我们的动画以 n 倍的速度运行…

我们更新我们的组件(删除不相关的代码):

我们启动了一个名为 **requestIdRef** 的新 ref 对象(第 5 行)。每当我们调用 requestAnimationFrame 时，我们都将返回值传递给这个 ref 对象。返回值是所谓的请求 ID，这意味着它是通过调用它而启动的帧的标识符。

我们可以随时使用这个 ID 来取消我们的动画。正如我们提到的，我们希望在从 DOM 中卸载组件时这样做。

使用钩子，在函数式 React 组件内部，我们可以通过在函数内部返回一个回调来实现这一点，该回调作为第一个参数传递给我们的 useEffect 钩子:

```
return () => {
  cancelAnimationFrame(requestIdRef.current);
};
```

参见上面要点中的第 14 行。

## 结论

暂时就这样吧！通过采取这些简单的步骤，您可以在 React 组件中启动一个动画，并确保它不会出现意外的行为，是高性能的，并在完成后进行清理。

我喜欢 HTML 画布，并希望通过写这篇小文章来传播这份爱。

> 如果你已经分享了那份爱:请留意全新的 [***CSS 胡迪尼***](https://developer.mozilla.org/en-US/docs/Web/Houdini) *。它将允许你把你的画布知识转移到 CSS 的世界，并创建你自己的“CSS 渲染函数”。极其强大的 API，也是 web 开发未来的一部分，但这是另一天的主题😉*

杰拉德·范德普特