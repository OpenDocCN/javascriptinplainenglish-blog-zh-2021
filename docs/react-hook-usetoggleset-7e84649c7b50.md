# useToggleSet:用于切换元素的自定义 React 挂钩

> 原文：<https://javascript.plainenglish.io/react-hook-usetoggleset-7e84649c7b50?source=collection_archive---------16----------------------->

![](img/c02ecc63f61a7153e5e7284fb27a13c0.png)

Photo by [Mukund Nair](https://unsplash.com/@m_k_nd?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

打开和关闭一组元素是现代 web 服务的常见部分。一个用例是在搜索时选择要过滤的属性，另一个用例是选择应该包含在请求中的项目。

为此编写逻辑通常很简单，但是反复编写有点麻烦。最近我在一个项目中遇到了这个问题，我想分享一下如何使用一个可重用的钩子来一劳永逸地解决这个问题。

注意，这篇文章是 React 独有的，因为它需要 hook API。

## 冰淇淋店示例

![](img/e3918aae0e69eb72b318d8a583d0856d.png)

Photo by [Lama Roscu](https://unsplash.com/@lamaroscu?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们将用一家冰淇淋店作为例子来说明我们所写的逻辑。我们假设用户可以选择任意数量的口味来制作一个冰淇淋。

我们用一组薯片来表示，每一片都有“香草”、“巧克力”和其他熟悉的冰淇淋口味的名字。

然后，用户可以随心所欲地选择和取消选择每种口味。在底部，我们将向用户展示一整套活跃的味道。

我已经用完成的钩子实现了这一点。继续看一看，测试一下逻辑，然后让我们看看实现的细节。

## hooks/useToggleSet.ts

我们将创建一个钩子，它使用 React 默认的`useState`钩子，因为我们知道这在跟踪状态和用新数据更新状态方面已经很健壮了。

**TypeScript:** 我们希望跟踪类型，所以我们将它作为类型`T`的通用函数，这将是我们的钩子将要处理的元素的类型。

我们将接受类型为`T`的`initialSet`，这是我们的初始活动集。请注意，我们不接受代表整个可能元素集的任何参数。我们也可以这样做，但是特别是如果使用 TypeScript，泛型类型`T`的限制对于大多数用例应该是足够的。

使用`useState`，我们定义了`activeSet`，代表当前选择的元素，以及函数`setActiveSet`，将这个选择更改为任何其他的任意集合。

接下来，我们将方法`toggleElement`定义为一种打开和关闭类型`T`的任何给定元素的方式。方法相当简单:如果元素已经在我们的活动元素列表中，我们就删除它。如果没有，我们包括它。

最后，我们将`activeSet`和`toggleElement`函数作为双元素长度数组返回，以努力与 React hooks 语法保持一致。我们返回数组`as const`来表明我们的钩子初始化将只返回这两个变量，按照特定的顺序。这使得 TypeScript 能够正确识别`activeSet`和`toggleElement`的类型，而不管它们在使用我们的钩子的组件中的命名。

## 源代码:

```
import { useState } from "react";function useToggleSet<T>(initSet?: T[]) { const [activeSet, setActiveSet] = useState(initSet || ([] as T[])); const toggleElement = (element: T) => { if (activeSet.includes(element)) { setActiveSet(activeSet.filter(el => el !== element)); } else { setActiveSet(activeSet.concat(element)); } }; return [activeSet, toggleElement] as const;}export default useToggleSet;
```

## 考虑

非常简单，嗯？

以目前的形式，这应该可以完美地用于原语；对象不太好。允许对象的最好方法可能是采用第二个参数来确定相等性。另一种方式可以是在所有传入元素上运行的序列化函数。在我目前的用例中，我不需要这样做，所以我没有费心去实现它，尽管如果有人要求，我可能会去做。

也就这样了！一个实现自定义 React 钩子的超级简单的方法，允许我们轻松地打开和关闭一组元素。因为这实际上只是 useState 的更新功能的包装，所以没什么大不了的！尽情享受，自由使用！

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)