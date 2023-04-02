# 你必须知道闭包是一个(好的)反应开发者

> 原文：<https://javascript.plainenglish.io/you-have-to-know-closures-to-be-a-good-react-developer-104fc2f6cd70?source=collection_archive---------0----------------------->

## 为什么你需要知道闭包才能成为一个比普通的 React 开发者

![](img/15bcd8c8113f166c3ba3c9b1ae3f990d.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我经常听到这样的误解:作为一名 React 开发者并不意味着你必须对 JavaScript 的工作原理有深刻的理解。毕竟，这是有意义的——一般的 React 开发者在大多数时间里只使用三进制表达式和一些数组函数(map、filter 等)。)，对吗？

好吧，事实证明，如果你想成为一个比普通的 React 开发人员更优秀的开发人员，你需要对 JavaScript 在幕后是如何工作的有一个扎实的掌握——闭包、原型和引用/基元值类型，这些只是你必须掌握的一些概念。

在本文中，我将向您展示，理解闭包如何提高您的反应技能。本文不是要解释闭包是如何工作的。我将展示一个简单的例子，但是如果你想理解闭包，我建议你搜索另一个资源[(像这样)](https://dmitripavlutin.com/simple-explanation-of-javascript-closures/)。兴奋吗？我们走吧！

# 什么是结束？

让我们看看 [MDN 对](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)闭包有什么看法:

> 闭包是捆绑在一起的函数与对其周围状态(词汇环境)的引用的组合。换句话说，闭包让您可以从内部函数访问外部函数的范围。在 JavaScript 中，每次创建函数时都会在函数创建时创建闭包。

好的，这是官方定义。听起来有点吓人？简单地说:Closure 意味着，当 JavaScript 运行您的代码时，它会查找您的函数中的所有变量，如果它看到一个函数中没有声明(- let，const)的变量，但是在一个外部作用域(函数嵌套在其中)中，它会“锁定”给定函数中该变量的值。

你还困惑吗？考虑以下代码片段:

```
const myOuterFunction = () => {
  let variableInOuterFunction = 'Hello World';
 const myNestedFunction = () => {
    console.log(variableInOuterFunction);
  }; myNestedFunction();
}; myOuterFunction();
```

请注意，我们如何在“myNestedFunction”中使用“variableInOuterFunction”(在 myOuterFunction 中声明)。结束了。值“Hello World”现在在嵌套函数中被“关闭”(锁定)。听起来很简单，对吧？让我们看看理解它如何帮助我们做出反应。

# 反应中的闭包

所以，让我们看看闭包在 reactor 中是如何工作的。

考虑以下代码片段:

```
import React, { useEffect, useState } from 'react';const ClosuresInReact = () => {
  const [count, setCount] = useState('1');
 const incrementCount = () => {
    setCount(prevCount => +prevCount + 1);
  }; useEffect(() => {
    const timer = setTimeout(() => {
      incrementCount();
    }, 1000);
    return () => {
      clearTimeout(timer);
    };
  }, [incrementCount]);
  return <div>{`Timer started: ${count}`}</div>;
}; export default ClosuresInReact;
```

那么，我们这里有什么？

它是一个简单的反应组件，在屏幕上打印一个计时器，每秒钟递增一次。我们使用 useState 钩子来跟踪计数变量的变化，然后使用 setCount 函数来增加计数变量的增量计数函数，最后，我们使用 useEffect 钩子来负责使用内置的 JavaScript 函数 setTimeout 每秒触发增量计数函数。

有经验的 React 开发人员可能已经注意到，在 useEffect 钩子的依赖数组中有 incrementCount 函数。实际上，可能没有必要在这里包含它，但是总是用 useEffect 钩子中使用的所有变量(和函数)填充依赖数组被认为是一个好的实践。

现在我们有另一个问题。使用 incrementCount 函数作为 useEffect hook 中的依赖项，我的 IDE 横向对我大喊:

添加替代文本

![](img/31d4f3b79c2074662e347c0439eb91f1.png)

我们不会深究为什么现在会发生这种情况，我只会说这与函数是引用类型这一事实有关，如果我们不将它移动到 useEffect 钩子内或用 useCallback 钩子包装它，我们会导致无限循环。无论如何，对我们来说，现在重要的是 IDE 的建议——要么将 incrementCount 移到 useEffect 内部，要么用 useCallback 钩子将它包装起来。让我们选择第二个选项。

```
import React, { useCallback, useEffect, useState } from 'react';const ClosuresInReact = () => {
  const [count, setCount] = useState('1');
 const incrementCount = useCallback(() => {
    setCount(prevCount => +prevCount + 1);
  }, []); useEffect(() => {
    const timer = setTimeout(() => {
      incrementCount();
    }, 1000);
    return () => {
      clearTimeout(timer);
    };
  }, [incrementCount]);
  return <div>{`Timer started: ${count}`}</div>;
}; export default ClosuresInReact;
```

太好了！现在一切都正常了，对吗？我的意思是，甚至我的 IDE 现在也平静下来了，让我们运行代码吧！

我们看到计时器开始计时:1，2，然后…发生了什么？计时器刚刚停在 2？为什么会这样呢？

添加替代文本

![](img/2cd27f9424cc8d2898a76b418af38782.png)

原因是——你猜对了——闭包！如果我们仔细观察，我们会发现在 incrementCount 函数中实际上有一个闭包。这一点很难注意到，但是当我们使用 setCount 函数时，我们也依赖于 Count 变量，我们也可以这样写:

```
setCount(+count + 1)
```

编写更长版本的原因是，当我们依赖以前的状态时，我们应该采用最新的状态，这样做是一个好的做法(尽管在我们的示例中不一定需要)。

无论如何，回到闭包——正如我们在例子中看到的，在外部函数 ClosuresInReact 中声明的变量 count 的值现在被“锁定”在函数 incrementCount 中。更准确地说，我们在 setCount 函数中所做的增量被锁定在 incrementCount 函数中，这就是为什么我们在屏幕上看到 1、2 和… stop。

# 如何修复 React 中的关闭问题

因此，让我们简化这里发生的过程:

React:我有一个将 incrementCount 作为依赖项的 useEffect 钩子。这意味着我应该只在 incrementCount 改变时重新渲染。

React:我用 useCallback 钩子包装了 incrementCount。这意味着我应该记住它的第一个闭包(当它第一次运行时)，即使发生了重新呈现，我也不应该在刷新的环境中运行函数(当 count 现在是 2 时)，而是使用我捕获的它的良好的旧的第一个闭包(当 count 是 1 时)。

React: useEffect 告诉我 incrementCount 没有变化，所以我不应该触发新的渲染。

你明白了。那么我们该怎么办呢？解决办法很简单。我们需要将 count 变量作为依赖项传递给 useCallback 钩子。这样，我们告诉 React，即使我们希望保留 incrementCount 函数的第一个闭包，React 也应该跟踪并用 Count 变量的最新值更新闭包。通过这样做，我们还导致了 useEffect 钩子调用屏幕上的重新呈现，因为 incrementCount 每秒都在变化。

```
import React, { useCallback, useEffect, useState } from 'react'; const ClosuresInReact = () => {
  const [count, setCount] = useState('1');
 const incrementCount = useCallback(() => {
    setCount(prevCount => +prevCount + 1);
  }, [count]); useEffect(() => {
    console.log('useEffect');
    const timer = setTimeout(() => {
      incrementCount();
    }, 1000);
    return () => {
      clearTimeout(timer);
    };
  }, [incrementCount]);
  return <div>{`Timer started: ${count}`}</div>;
}; export default ClosuresInReact;
```

现在一切都在按预期运行。有趣的是，我的 IDE 现在仍然对我大喊:

添加替代文本

![](img/870c546ce9849df47b23fc8f22f404d7.png)

它告诉我从依赖数组中移除计数。这当然是一个错误，发生这种情况是因为我们实际上并没有在 setCount 函数中使用 count 变量，但这只是再次向我们展示了理解闭包对于一个好的 React 开发人员来说是多么重要，因为没有它我们无法解决问题。

# 结论

JavaScript 中的闭包是一个至关重要的概念，当涉及到反应时，理解幕后发生的事情可能变得更加重要。React 本身，尤其是 React 钩子，在很多地方都使用了闭包。

掌握闭包的概念，以及 JavaScript 的其他核心概念(原型、引用和原始类型，等等)会使您成为更好的 React 开发人员，并帮助您以更高效、更优雅的方式解决问题。

# 用组件构建微前端

微前端是加速和扩展应用程序开发的好方法，具有独立的部署、解耦的代码库和自治的团队。

位为构建组件驱动的微前端提供了很好的开发体验。构建组件、协作和组合可扩展的应用程序。[我们的 GitHub 有超过 14.5k 颗星星！](https://github.com/teambit/bit)

[**试一试→**](https://bit.dev)

![](img/974fac3b1ac310e3d805735bbe3a102d.png)

An independently source-controlled and shared “card” component (on the right, its dependency graph, auto-generated by Bit)

## 了解更多信息

[](https://blog.bitsrc.io/building-a-react-component-library-d92a2da8eab9) [## 构建 React 组件库——正确的方法

### 创建一个超级模块化的 React 组件库:可伸缩、可维护、安装速度极快。

blog.bitsrc.io](https://blog.bitsrc.io/building-a-react-component-library-d92a2da8eab9) [](https://blog.bitsrc.io/microservices-are-dead-long-live-miniservices-40e4ccf4741) [## 微服务已死——微服务万岁

### 你真的在为你的应用使用微服务吗？再想想。

blog.bitsrc.io](https://blog.bitsrc.io/microservices-are-dead-long-live-miniservices-40e4ccf4741) [](https://blog.bitsrc.io/7-tools-for-faster-frontend-development-in-2022-43b6f663c607) [## 2022 年加快前端开发的 7 种工具

### 您应该知道的工具，可以更快地构建现代前端应用程序，并获得更多乐趣。

blog.bitsrc.io](https://blog.bitsrc.io/7-tools-for-faster-frontend-development-in-2022-43b6f663c607)