# 理解挂钩第 1 部分-元素

> 原文：<https://javascript.plainenglish.io/hook-myth-from-react-9495aa8ad7af?source=collection_archive---------21----------------------->

React 里传说中的钩子背后有什么？有时候，我会想。

![](img/8e42cee1f7d92219ceebab9b4725eb57.png)

Captain Hooks. Find me if you can.

给定一个`Component`，将它传递给一个助手函数`component`，在那里它生成一个新的`Element`类供 UI 系统使用。在这个类中，额外的`Hook`属性，如`states`和`effects`，被分配并为`Hooks`做好准备。

```
*/* Implementation */* function component(**renderer**) {
  class Element {
    constructor() {
      this.**renderer** = **renderer**
      this.**states** = {}
      this.**effects** = {}
      this.**queued** = false
    }
    ...
  }
  return Element
}*/* Usage */* const Component = () => <div />
component(**Component**)  // can be transparent to us
```

## 钩

将`useEffect`实现与用法放在一起。注意`useEffect`通过将`callback`添加到注册列表`effects`来注册它。

```
*/* Implementation */* function useEffect(**callback**) {
  *const id = notify()*
  if (!element.**effects**[id]) 
    element.**effects**[id] = **callback**
}*/* Usage */* function **Component**() {
  useEffect(() => { window.title = "ABC" })
}
```

> 钩子`id`根据其在`Component`内部出现的位置唯一生成。由于这种缓存，它不会在多次渲染中注册两次。

```
/* Implementation */
function useState(initialState) {
 *const id = notify()*  **element**.**states**[id] = initialState const setState = (newState) => {
    **element**.**states**[id] = newState
    **element**.**_update**()
  } return [**state**, **setState**]
}*/* Usage */* function **Component**() {
  const [**count**, **setCount**] = useState(0);
}
```

同样，`useState`将`state`和`setState`与挂钩`id`对齐。注意调用`setState`会触发更新。

## 更新

当进入元素更新周期时，它检查元素是否已经排队等待更新。如果还没有，它将请求渲染它并将结果提交给`DOM`。

```
function _update() {
  if (this.**queued**) return
  schedule(() => {
    let result = this.**_render**(element)
    schedule(() => {
      this.**_commit**(result)
      for (let e of this.**effects**) e.call(this)
    })
    this.**queued** = false
  })
  this.**queued** = true
}
```

渲染函数调用`Component`从而返回`DOM`元素。这和定义`Hooks`的函数是一样的。

```
function _render() {
  let result = element.**apply**(null, this.args)
  return result;
}
```

因此，在更新期间，**不会在**更新之前或之后，`Hooks`得到注册。此外，更新后，所有注册的`effects`都有机会被调用。

## **TL；博士**

**一个钩子**，通过一个`Element`类，在第一次更新时被注册，并且可以:

*   渲染后触发`effect`(`useEffect`)
*   通过`state`变化(`useState`)触发渲染

# 索引

*   第 1 部分，元素你在这里
*   [第二部分，使用效果](https://windmaomao.medium.com/hooks-part-2-useeffect-2fa1a377c124)
*   [第 3 部分，使用状态](https://windmaomao.medium.com/hooks-part-3-usestate-26a622bbe462)
*   [第四部，钩子](https://windmaomao.medium.com/understanding-hooks-part-4-hook-c7a8c7185f4e)
*   [第五部分，定制挂钩](https://windmaomao.medium.com/understanding-hooks-part-5-custom-hook-985b83c8bfea)
*   [第 6 部分，使用上下文](https://windmaomao.medium.com/understanding-hooks-part-6-usecontext-7ece0c0818e3)
*   [第七部分，状态管理](https://medium.com/codex/understanding-hooks-part-7-state-management-84ff636834a7)
*   [第八部，四体问题](https://windmaomao.medium.com/understanding-hooks-part-8-four-body-problem-8f70b212356d)

*使用的代码片段大量借鉴并简化自* [*回购*](https://github.com/matthewp/haunted) `*Haunted*` *为* `*lit-element*` *的早期草案。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)