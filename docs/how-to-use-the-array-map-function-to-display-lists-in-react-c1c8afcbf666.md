# 如何使用数组映射函数在 React 中显示列表

> 原文：<https://javascript.plainenglish.io/how-to-use-the-array-map-function-to-display-lists-in-react-c1c8afcbf666?source=collection_archive---------6----------------------->

让我们了解一下使用数组映射函数在 React 中动态生成列表有多简单。

![](img/3315cc53555e6980e830639511438dc1.png)

对于那些不知道的人来说，使用 map 函数并不是特定于 React 的语法。这完全是普通的 JavaScript。map 函数用更容易理解的语言接受一个项目数组(通常来自服务器),并返回一个经过转换以呈现不同外观的数组。我们将在 React 中利用这一点，获取一个数据列表，并将其转换为 React 组件列表，然后在屏幕上呈现。

# 让我们开始编码吧

让我们看一些例子来了解如何在 React 中使用它。我将把这些嵌入到一个名为 CodeSandbox 的在线代码编辑器中。对于那些以前没有尝试过的人来说，它使原型制作和共享项目变得非常容易。如果你想尝试一下，下面是一个链接。

[](https://codesandbox.io/) [## CodeSandbox:用于快速 Web 开发的在线代码编辑器和 IDE

### 无需设置超快速多人游戏更新实时共享沙盒无需设置-使用模板启动新项目…

codesandbox.io](https://codesandbox.io/) 

## 示例 Return 语句中项目的静态数组

这通常是 React 项目中最常见的地图使用方式。大多数情况下，如果组件以一种清晰易读的方式分解，我认为将这些代码直接放在 return 语句中没有问题。

## 示例 2:函数中项目的静态数组

JSX 也可以从 React 组件中的函数返回。如果做得正确，这可以清理代码，使其更具可读性，尤其是在较大的 React 组件中。

## 示例 3:来自 API 的一组项目

就此而言，处理 API 只是你进一步深入 React 和任何其他前端框架的保证。虽然地图的使用方式与例 1 中的**相同，但我想提供一个更真实的场景。**

# 结论

网站上经常需要处理数据列表，幸运的是，处理数据列表非常简单，因为 JavaScript 中内置了 map 函数。

*更多内容尽在*[***plain English . io***](https://plainenglish.io/)