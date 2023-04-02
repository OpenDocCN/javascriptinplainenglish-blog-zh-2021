# 理解钩子第 2 部分——使用效果

> 原文：<https://javascript.plainenglish.io/hooks-part-2-useeffect-2fa1a377c124?source=collection_archive---------25----------------------->

React 里传说中的钩子背后有什么？有时候，我会想。

![](img/8e42cee1f7d92219ceebab9b4725eb57.png)

在第 1 部分的[中，我们通过`Element`解释了钩子的一般概念。在第 2 部分中，我们想深入了解一下`useEffect`，看看它是如何支持回调、拆卸和依赖的。](https://windmaomao.medium.com/hook-myth-from-react-9495aa8ad7af)

为了连接到`element`，需要注册`callback`。

```
function Component() {
  **useEffect**(() => { window.title = "ABC" })
}
```

## 永远在线

默认情况下，`effects`总是打开的，并且在每次更新时被调用。

```
**useEffect**(() => {
  ...
  **return** () => {
    ...
  }
})
```

通常情况下，`callback`不需要`return`，但是如果`teardown`功能由`return`提供，它可以用于每次运行前的清洁工作，包括拆卸。

## 具有依赖性

为每个`update`运行`effect`，这可能有点贵。为了避免这种情况，我们可以将依赖关系`values`作为第二个输入。

```
**useEffect**(() => {
  ...
}, [**var1**, **var2**, ...])
```

只有当`var`内部发生变化时，`effects`才会被触发。因此对于空数组，挂载后会跳过`effect`。

## 笔记

钩子在每个渲染中都运行，对于`useEffect`也不例外。在每次渲染过程中，依赖关系会与以前的版本进行比较。如果检测到变化，新的依赖关系`array`以及`callback`功能将被替换。

**依赖数组和回调可以是新的实例。如果 dependencies 数组为空，则设置回调并调用一次。**

## TL；速度三角形定位法(dead reckoning)

`useEffect`主要有三种用法。

*   始终开启，为安装和每次更新运行。
*   空依赖项，仅为装载运行。
*   对于依赖项，为装载运行，每次更改都会更新。

**如果给出了 teardown，它将在每次运行和卸载之前调用。**

# 索引

*   [第 1 部分，要素](https://windmaomao.medium.com/hook-myth-from-react-9495aa8ad7af)
*   第二部分，使用效果你在这里
*   [第 3 部分，使用状态](https://windmaomao.medium.com/hooks-part-3-usestate-26a622bbe462)
*   [第四部分，挂钩](https://windmaomao.medium.com/understanding-hooks-part-4-hook-c7a8c7185f4e)
*   [第 5 部分，自定义挂钩](https://windmaomao.medium.com/understanding-hooks-part-5-custom-hook-985b83c8bfea)
*   [第六部分，使用上下文](https://windmaomao.medium.com/understanding-hooks-part-6-usecontext-7ece0c0818e3)
*   [第七部，国家管理](https://windmaomao.medium.com/understanding-hooks-part-7-state-management-84ff636834a7)
*   [第八部，四体问题](https://windmaomao.medium.com/understanding-hooks-part-8-four-body-problem-8f70b212356d)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)