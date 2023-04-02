# 了解 useRef React 挂钩

> 原文：<https://javascript.plainenglish.io/understanding-the-useref-react-hook-6771e68fc537?source=collection_archive---------10----------------------->

## 继续我们的 React hooks 系列，我们将在这篇博文中了解 useRef react hook。

![](img/cad61082ca53d65acb12fe3843f74db6.png)

继续我们的 [React hooks](https://www.wisdomgeek.com/tag/react-hooks/) 系列，我们将在这篇博文中了解 useRef React hook。

useRef React 挂钩在以下两种情况下很有用:

1.  在 React 内部直接访问 DOM 元素
2.  存储不触发重新呈现并且在重新呈现之间保持的状态值

在看到这个钩子的这些优点之前，我们先来了解一下钩子是什么，它是做什么的。

# 什么是 useRef React hook？

useRef React 挂钩是一个返回可变 Ref 对象的函数。Refs 是 React 中访问 DOM 节点的一种方式。

```
const refContainer = useRef(initialValue);
```

的。useRef React 钩子返回的对象的 current 属性被初始化为我们在钩子中传递的初始值。返回的对象在组件的整个生存期内都保持不变。

换句话说，useRef 可以用作容器，我们可以在其中存储可变值。

要改变对象的值，我们可以将新值赋给当前属性:

```
const App = () => {
   const myRef = useRef("initial value")

   // updating ref 
   myRef.current = "updated value" 

  // myRef now will be {current: "updated value"} 
}
```

如果我们使用`<div ref={myRef} />`将 ref 对象传递给 DOM 节点，那么。引用的当前属性将被设置为该节点。每当节点改变时，返回的引用变量也会更新。

当分配给一个 DOM 节点时，我们通常在 JSX 这样做。因此，我们在声明期间提供给 useRef React 钩子的初始值将是 null。

或者，如果我们不使用 DOM 节点，而是使用任何其他 JavaScript 值，那么该值将在重新呈现时保持不变。因此，这是保存可变值的一种简便方法。当以这种方式使用时，它非常类似于类中的实例字段。

但是为什么不自己用. current 属性({current: … })创建一个对象呢？唯一的区别是，使用 useRef React 钩子创建的对象将在每次渲染时返回相同的对象。如果是我们自己创造的，情况就不一样了。

还需要注意的是，useRef 没有附加通知程序。当值改变时，什么也不会发生。如果我们想要这个功能，最好使用 useState 钩子。如果我们想在一个 DOM 节点上添加/移除一个 ref 时执行一些代码，我们可以使用回调 ref。

# 访问 DOM 节点或 React 元素

让我们开始进入 useRef React 钩子有用的场景。熟悉 React 的人应该已经知道我们使用 Refs 来访问 DOM 节点或 React 元素。正如我们上面讨论的，useRef 也允许我们这样做。

为了在单击按钮时聚焦于一个元素，我们可以创建一个组件:

```
const InputTextWithFocusButton= () => {
   const inputEl = useRef()

   const onButtonClick = () => {
      inputEl.current.focus()
   }

   return (
      <>
         <input ref={inputEl} type="text" />
         <button onClick={onButtonClick}>Focus on Input Text</button>
      </>
   )
}
```

因此，我们能够访问子 DOM 节点，并使用 useRef React 钩子来访问它。

**注意:**同样的功能也可以通过使用 createRef API 来实现:

```
const InputTextWithFocusButton= () => {
   const inputEl = createRef()

   const onButtonClick = () => {
      inputEl.current.focus()
   }

   return (
      <>
         <input ref={inputEl} type="text" />
         <button onClick={onButtonClick}>Focus on Input Text</button>
      </>
   )
}
```

那我们为什么需要 useRef React 钩子呢？

关键在于坚持。useRef 的返回对象在组件的整个生命周期中都是持久的，而 createRef 则不是。如果要重新呈现组件，useRef 创建的对象将被持久化。使用 createRef 创建的对象将指向一个新对象。

如果你想在一个实际的例子中查看另一个例子，你可以查看我们之前的帖子[使用 useRef 钩子](https://www.wisdomgeek.com/development/web-development/react/detecting-click-outside-component-using-react-hooks/)检测 React 组件外部的点击。

另一件要记住的事情是避免在任何需要与 DOM 节点交互的地方使用 useRef。仅仅因为我们能做并不意味着我们应该去做。除非需要，否则不鼓励使用 useRef。围绕州的最佳实践的存在是有原因的。

# 存储可变变量

因为 useRef React 钩子返回一个 JavaScript 对象，所以它不局限于存储 DOM 节点。我们可以用它来存储任何我们希望在重新渲染时持久化的变量。

让我们创建一个组件来显示它被重新渲染的次数。

这份声明有用吗？

```
const RerenderCounter = () => {
  let count = 0;
  count++;

  return (<span>{count}</span>);
}
```

因为我们在组件内部初始化计数，所以每次重新渲染时都会重新初始化。因此该组件将始终呈现 1 作为输出。

我们需要引用一个在重新渲染时保留的变量。因此，请参考:

```
const RerenderCounter = () => {
  const count = useRef(0);
  useEffect(() => {
    // Every time the component has been re-rendered,
    // the counter is incremented
    counter.current = counter.current + 1;
  }); 
  return (<span>{count}</span>);
}
```

该实现将在重新渲染时保留 count 变量。由于值被保留，我们将在每次渲染时获得对相同变量的引用。因此，我们将在每次重新渲染时增加计数。因此，我们将获得组件被重新渲染的实际次数。

我们可以更新函数内部的计数器，而不是使用 useEffect，但是 React 文档建议修改事件处理程序或效果中的引用。这是因为功能组件中的所有副作用都应该在生命周期的布局阶段或提交阶段完成，以避免意外。

关于这个功能的另一个实例，你可以查看我们的帖子，在那里我们[使用 useReducer](https://www.wisdomgeek.com/development/web-development/react/use-redux-like-middleware-for-usereducer-in-react/) 钩子创建了类似 redux 的中间件。我们使用 useRef 钩子存储组件的先前状态，并在每次使用 [useReducer 钩子](https://www.wisdomgeek.com/development/web-development/react/understanding-the-usereducer-hook-in-react/)更新状态时更新它。

我们希望这篇文章能帮助你对 useRef React hook 有更深的理解，现在你知道什么时候不应该使用它了。如果你有任何疑问，请在评论区告诉我们。

*原载于 2021 年 1 月 21 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/react/understanding-the-useref-react-hook/)*。*