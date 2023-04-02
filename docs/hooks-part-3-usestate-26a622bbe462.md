# 理解钩子第 3 部分——使用状态

> 原文：<https://javascript.plainenglish.io/hooks-part-3-usestate-26a622bbe462?source=collection_archive---------12----------------------->

传说中的 React 钩子背后是什么？有时候，我会想。

![](img/8e42cee1f7d92219ceebab9b4725eb57.png)

在[第二部分](https://windmaomao.medium.com/hooks-part-2-useeffect-2fa1a377c124) , `useEffect`及其所有用法都被详细考察了。在第 3 部分中，我们将继续深入探讨`useState`。

```
function Component() {
  const [**value**, **setValue**] = useState(**initialValue**);
  ...
  return (<div />)
}
```

用初始值初始化`state`。需要时，通过调用`setState`通知`Element`新值。

## 价值

提供的`value`可以直接用于`Component`定义。并且它可以被进一步发送到子组件中。

```
function Component() {
  const [**value**, **setValue**] = **useState**(**initialValue**)
  const onChange = e => {
    **setValue**(e.target.value)
  }
  return (
    <>
      value: {value}
      <input value={**value**} onChange={onChange} />
      <ChildComponent value={**value**} />
    </>
  )
}
```

该值可以是简单的数字和字符串，也可以是复杂的对象，实际上可以是 Javascript 中的任何内容。

```
const [**value**] = useState({ **name**, **func**, ...**anything** })
```

## 设置值

用`setValue`替换该值。

```
setValue(name)
// replace property name
setValue({ ...value, name })
// append to array
setValue([ ...values, { name })
```

如果值需要在设置前解析，可以用函数代替。

```
const reducer = prev => prev + 1
**setValue**(reducer)
```

你可能想要使用一个函数的原因之一是它可能依赖于先前的值，就像一个`reducer`。或者以后再解决，作为一个懒值。

一旦设置了新值，它就会请求`Element`进行更新。在下一个周期，用户界面将反映这一变化。

## 更新

`setValue`请求主机元素更新的事实。为了让其他组件使用它，可以通过`props`传递给其他组件。

```
function Component() {
  const [, **setValue**] = **useState**(0)
  return <ChildComponent setValue={set**Value**} />
}
```

这个函数可以被传递，传递给一个父母，传递给一个孩子，传递给一个`context`，甚至被收集为`updates`。

```
const updates = [setValue1, setValue2, ...]
updates.forEach(set => { set(value) })
```

## *原始的*

`value`可以是*原语*类型，如 1 或“字符串”。如果您需要传递这个值，特别是在一些延迟的时间，请记住这个值不是未来的证据。

```
const [value, setValue] = useState(0)
const doSomethingAboutIt = v => { 
  setTimeout(() => { console.log(v) }, 10000) 
}
doSomethingAboutIt(**value**)
```

`v`并不总是指向当前的`value`，因为`Component`可能已经被渲染了多次，每次渲染都会分配一个新的`value.`副本

## 笔记

在每个渲染中都运行一个钩子。第一次运行时设置一次`useState`的初始值。在每次渲染过程中，会将该值与以前的版本进行比较。如果检测到变化，则接受新值。然而，这种情况不会发生在`setValue`功能上，该功能在第一次运行时被设置，此后被(重新)使用。

**该值可以是一个新的实例。**初始值和设定函数都不是。

## TL；速度三角形定位法(dead reckoning)

`useState`分配一个值，并允许设置该值以请求元素更新。它还允许在设置值时使用函数。该值可以是没有引用跟踪的原始值。

# 索引

*   [第一部分，元素](https://windmaomao.medium.com/hook-myth-from-react-9495aa8ad7af)
*   [第二部分，使用效果](https://windmaomao.medium.com/hooks-part-2-useeffect-2fa1a377c124)
*   第 3 部分，使用状态你在这里
*   [第四部分，挂钩](https://windmaomao.medium.com/understanding-hooks-part-4-hook-c7a8c7185f4e)
*   [第 5 部分，自定义挂钩](https://windmaomao.medium.com/understanding-hooks-part-5-custom-hook-985b83c8bfea)
*   [第 6 部分，使用上下文](https://windmaomao.medium.com/understanding-hooks-part-6-usecontext-7ece0c0818e3)
*   [第七部分，状态管理](https://windmaomao.medium.com/understanding-hooks-part-7-state-management-84ff636834a7)
*   [第八部，四体问题](https://windmaomao.medium.com/understanding-hooks-part-8-four-body-problem-8f70b212356d)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)