# 反应上下文是一个全局变量

> 原文：<https://javascript.plainenglish.io/react-context-is-a-global-variable-b4b049812028?source=collection_archive---------4----------------------->

React 里没有 Redux 的对应词，最接近的一个叫 Context。我们中有相当多的人认为，与 Redux 相比，上下文是本地的，而 Redux 对站点来说是全局的，尤其是当涉及到数据存储的位置时。

然而，React context 并没有被设计成一个局部变量，就像纤程、钩子或者任何局限于一个工作单元的东西一样。恰恰相反，都不是。所以我们将在下面解释为什么。

## 创建一个上下文

![](img/27b1ac47356982faf198bc571628463f.png)

上下文由函数`createContext`创建，

```
const UserContext = createContext(defaultValue)
export default UserContext
```

上下文对象是保存值的元素，

```
{
  **_currentValue**: defaultValue,
  Provider: { ... },
  Consumer: { ... }
}
```

上下文，比如`UserContext`，被立即导出，因为它需要被每个提供者和消费者引用。把它们放在同一个文件里不会暴露它的本质。上下文需要与消费者和提供者共享！

## 上下文范围

在讨论上下文作用域之前，我们先来看看什么是函数作用域。

```
function provider1(value) {
  const provider2 = (value) => {
    const provider3 = (value) => {
      console.log(value)  
    }
    provider3(3)
  }
  provider2(2)
}
provider1(1)
```

猜猜上面代码的输出是什么。答案是`3`。因为我们都知道函数有一个范围。在函数范围内，输入参数中的局部变量优先。

上下文提供者以类似的方式设计，它使用一个堆栈在进入内部范围之前将旧值推入，然后在离开范围之后将旧值弹出。

```
const Branch = ({ theme1, theme2 }) => {
  return (
    <ThemeContext.Provider value={theme1}>
      // **A**. value = theme1
      <ThemeContext.Provider value={theme2}>
        // **B**. value = theme2
      </ThemeContext.Provider>
      // **C**. value = theme1
    </ThemeContext.Provider> 
    // **D.** value = defaultValue
  )
}
```

有没有想过，给定`theme1`和`theme2`，为什么位置 **A** 、 **B** 和 **C** 的上下文值不同？同一个`ThemeContext`下的单个变量`_currentValue`怎么可能保存一个动态值？这怎么可能？什么是`_currentValue`？不是`theme1`，不是`theme2`？

上面的代码似乎不能与代码中提到的任何本地值一起工作。

## 堆栈和光标

因此，原来有一个全局变量在幕后工作，称之为`cursor`。在我们用一个`value`进入一个内部作用域之前，我们把它推入一个堆栈。

```
function push(cursor, value) {
  index++

  valuesStack[index] = cursor.current

  cursor.current = value
}
```

`push`操作将旧值放入堆栈，然后将`cursor`的当前值替换为新的`value`。在我们完成内部作用域后，我们将它从堆栈中弹出。

```
function pop(cursor) {
  if (index < 0) return

  cursor.current = valueStack[index]
  valueStack[index] = null
  index--
}
```

这样，`cursor`总是指向相对于作用域的最新值。堆栈用来确保它能找到返回的路。

## 推送和弹出提供商

这就是嵌套时提供程序的工作方式。当我们开始更新一个提供商时，它会将其推入。

```
function updateContextProvider(current, workInProgress) {
  ...
  pushProvider(workInProgress, newValue)
  if (oldProps !== null) { ... }
  ...
}function pushProvider(providerFiber, nextValue) {
  var context = providerFiber.type._context push(valueCursor, context._currentValue)
  context._currentValue = nextValue;
}
```

`pushProvider`函数通过属性`value`将上下文的`_currentValue`设置为`newValue`。内在范围的消费者就是这样获得内在价值的。在此之前，你可以看到它如何将旧的`_currentValue`放入堆栈，并将其与一个全局变量`valueCursor`一起存储。

```
function popProvider(providerFiber) {
  var currentValue = valueCursor.current
  pop(valueCursor)
  var context = providerFiber.type._context context._currentValue = currentValue
}
```

当提供者完成`completeWork`中的工作时，它调用`popProvider`，后者将上下文的`currentValue`设置回来自`valueCursor`的保存值。在此之前，你可以看到它是如何从堆栈中取出旧值的。

## 摘要

在任何时候，都只有一个上下文，比如`UserContext`对象，因此`_currentValue`确实保存一个“全局”变量，并且当它进入每个提供者的范围时，只切换到保存一个局部范围值(通过`value` prop ),因为消费者需要从`_currentValue`中读取。

但是，如果您想要找到对应于所有使用者(连接在多个作用域中)的所有上下文值，您唯一可以找到的地方是堆栈，它保存每个嵌套作用域中的上下文值列表。

因此，您可能会认为上下文值在正确的范围内将**启用**到本地提供者设置中，但是我们必须承认，上下文值，例如`_currentValue`，上下文的唯一数据存储，本质上是一个全局变量。

## 附录

为什么我们关心上下文是全局变量还是局部变量？如果你仍然认为上下文不能做 redux 所提供的事情，这很重要。因为在理论上，基于上面解释的设计，一个上下文可以做任何事情，因为它没有与任何纤程连接，它是一个全局共享变量。实际上，更好的是，当上下文进入提供者的范围时，它可以切换到本地范围版本，这应该使它比 Redux 提供的更通用。

过去的问题是如何在上下文中正确使用`React.memo`。因为没有了`memo`，语境就可能成为灾难性的武器。因此，为了避免这些问题，需要改进上下文，至少需要非常清楚如何更新特定的值，而不会过度渲染。也许这不是上下文的问题，因为 Redux 也有过多的渲染。

在本文写作期间，React 正在提出`useContextSelector`，这似乎将它放在了一个光明的方向。这是[提案](https://github.com/facebook/react/pull/20646)。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)