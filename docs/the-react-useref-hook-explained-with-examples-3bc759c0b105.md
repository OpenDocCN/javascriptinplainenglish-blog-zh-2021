# React UseRef 钩子举例说明

> 原文：<https://javascript.plainenglish.io/the-react-useref-hook-explained-with-examples-3bc759c0b105?source=collection_archive---------6----------------------->

## 通过实例了解 React 中的 UseRef 挂钩。

![](img/2e00032c05965cdc7a8004a3afe9604d.png)

Image created with ❤️️ By [author](https://mehdiouss315.medium.com/).

# 介绍

React 提供了一系列挂钩，允许您向组件添加特性。这些钩子使得在功能组件中封装有状态行为和副作用变得更加容易，从而增加可读性并使用更少的代码。

在本文中，我们将通过一些实例来了解 React UseRef 钩子。让我们开始吧。

# 什么是 UseRef 钩子？

React 中的钩子`useRef()`返回一个具有属性`current`的对象，我们可以像访问对象一样访问该属性。该属性被初始化为函数`useRef()`中传递的参数。返回的对象将在组件的整个生存期内保持不变。

钩子`useRef()`接受一个参数，这个参数是初始化返回对象中属性`current`的值。

为了使用钩子`useRef`，你必须首先从 React 包中导入它。

这里有一个例子:

```
import React, **{ useRef }** from 'react';
```

现在，您可以毫无问题地使用挂钩了:

```
const myRef = **useRef(0)**;console.log(myRef);
// { current: 0 }
```

正如你在上面的例子中看到的，我们已经创建了一个名为`myRef`的 ref，并将其默认值设置为 0。在这种情况下，返回对象中的属性`current`的值将为 0。您可以通过在控制台中打印`myRef`来检查。

使`useRef`强大的是它在渲染之间持续存在的事实。它与`useState`非常相似，但它不会导致组件在更改时重新呈现。为了让事情更清楚，我们来看一些实际的例子。

假设您想要计算组件重新渲染的次数。在这种情况下，您可以使用`useState`挂钩或`useRef`挂钩。

*状态:*

```
function StateExample() {
  const [count, setCount] = **useState(0)**;

  useEffect(() => {
    **setCount**(prevCount => prevCount + 1);
  });

  return <div>{**count**}</div>;
}
```

*参考:*

```
function RefExample() {
  const count = **useRef(0)**;

  useEffect(() => {
    **count.current = count.current + 1;**
  });

  return <div>{**count.current**}</div>;
}
```

这两个例子都将显示组件重新渲染的次数。然而，在状态示例中，组件将无限地重新呈现自己，因为我们在这种情况下设置状态。另一方面，ref 示例将只运行一次，因为它不会导致组件在更改时重新呈现。

# UseRef 的使用案例

React 中钩子`useRef`最常见的用例之一是引用 DOM 元素。

由于每个 DOM 元素都有一个属性`ref`，我们可以使用钩子`useRef` 来设置对该元素的引用。

下面是一个例子，每当我们单击一个按钮时，它就关注一个输入元素:

```
const Reference = ()=> {
  const inputRef = **useRef(null)**

  const focusInput = () => {
    inputRef.current.focus()
  }

  return (
    <>
      <input **ref={inputRef}** />
      <button onClick={focusInput}>Focus on the Input</button>
    </>
  )
}
```

refs 的另一个用例是跨组件呈现持久化的存储。例如，使用 refs，我们可以存储状态变量的前一个值。

下面是一个例子:

```
const Reference = ()=> {
  const [name, setName] = useState('Mehdi')
  const previousName = useRef(null)

  useEffect(() => {
    previousName.current = **name;**
  }, **[name]**)

  return (
    <>
      <input value={name} onChange={e => setName(e.target.value)} />
      <div>{previousName.current} => {name}</div>
    </>
  )
}
```

以上示例将在每次名称更改时更新`previousName` ref，以便它始终存储名称变量的上一个值。

# 结论

钩子`useRef`是你需要知道的重要且有用的反作用钩子之一。它允许您直接访问 DOM 元素，并在渲染之间保存数据，而不会导致组件在变化时无限地重新渲染。

谢谢你阅读这篇文章，我希望你觉得它有用。

# 更多阅读

*如果你对 JavaScript 和 web 开发相关的更有用的内容感兴趣，你也可以* [*订阅*](https://mehdiouss.ck.page/) *我的时事通讯。*

*以下链接中还有一篇有用的文章可以查看:*

[](https://medium.com/javascript-in-plain-english/fetching-data-with-useeffect-in-react-604ed53edffe) [## 在反应中使用 UseEffect 获取数据

### 通过真实世界的例子了解反应使用效果。

medium.com](https://medium.com/javascript-in-plain-english/fetching-data-with-useeffect-in-react-604ed53edffe)