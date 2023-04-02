# 使用代理进行本地状态管理

> 原文：<https://javascript.plainenglish.io/use-proxy-for-local-state-management-b775718eb5b0?source=collection_archive---------3----------------------->

![](img/e4e816c6992c8b8b59b64f4c34478f64.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您使用过 Redux、Overmind 或任何支持全局状态管理需求的工具，您可能非常了解工作流的状态/缩减类型。这篇文章是**而不是**讨论如何使用这些软件包。相反，我想探索一些基本需求，比如管理以下状态单元:

```
const counter = {
  count: 1,
  inc: (state, payload) => {
    state.count += payload
  }
}
```

对于一个`counter`单元，它支持一个状态，比如`count`以及一个改变它的`inc` 函数。JavaScript 最近给了我们一种新的管理对象的方法，叫做代理。它的作用是让您管理对象下的任何属性何时被访问，无论是`get`还是`set`:

```
const handler  = {
  get: function(target, prop, receiver) { ... },
  set: function(obj, prop, value) {
 **obj[prop] = value**    return true
  }
}const p = new Proxy(counter, handler)
```

前面的代码管理`counter`到`p`的 get/set。这个控制逻辑在一个`handler`回调中被捕获。让我们用一点。

```
p.count = 0  // counter[count] = 0
p.count++    // counter[count] = 1
```

目前，它只做一个简单的对象`counter`。我们需要给它添加一些控制。

**设定**

我们可以对`set`有更多的控制。假设我们有一个`options`对象，允许我们使用`canSet`来决定它是否可以设置一个属性。

```
set: function (obj, prop, value) {
  let canSet = true
  if (options.canSet) {
    canSet = options.canSet(obj, prop, value)
  }
  if (canSet) {
 **obj[prop] = value**  } options.afterSet && options.afterSet(obj) return true
}
```

如果`options.canSet`返回`false`，可以跳过`set`。而且在`set`之后，我们可以调用一个`options.afterSet`回调函数。基本上，我们所做的是用自定义规则来保护一些属性，如果任何属性发生变化，我们也会得到通知。听起来很熟悉？一种国家管理系统。

**得到**

如果我们使用下面的代码设计`counter`，它将开箱即用。

```
const counter = { 
  count: 1, 
  inc: function() { this.count++ } 
}
```

然而，关键字`this`有点复杂，没有人知道它在运行时到底是什么。此外，我们希望`inc`在改变到下一个状态之前获得当前状态，就像在状态机中一样。为此，我们可以通过`get`将其弯曲:

```
get: function (target, prop, receiver) {
  const value = target[prop]
  if (typeof value === 'function') {
    return function () { 
      value.apply(receiver, [
        receiver, ...arguments
      ]) 
    }
  }
  return value
}
```

前面的代码基本上重写了函数方法的`get`，比如`counter.inc`。它的行为和以前完全一样，除了当它使用函数方法时，它绑定代理对象并注入代理对象作为它的第一个输入参数，并附加输入参数的其余部分。换句话说，你现在可以这样做:

```
const counter = {
  count: 1,
  inc: (state, payload) => {
    state.count += payload
  }
}const p = new Proxy(counter, handler)
p.inc(2)    // count = 3
```

**调度**

现在，这个`get`和`set`都被调整到一个状态管理系统，我们可以插入调度，例如，在屏幕上呈现一些东西。

以任何一个支持`dispatch`功能的 *UI* 框架为例，这里用`react`作为例子。

```
const useProxy = (counter) => {
  const [, dispatch] = useState(0) const [p] = useState(proxy(counter, {
    canSet: (obj, prop, value) => obj[prop] !== value,
    afterSet: () => { dispatch(v => v + 1) }
  })) return p
}
```

这里我们使用`useState`作为我们的主要调度机制，除了我们并不真正关心我们渲染什么，我们只是想在我们决定的时候触发一个渲染。我们从`counter`中插入`proxy`对象。我们在这里做两件有趣的事情。

第一，通过`canSet`，我们确保如果`value`没有从当前的`obj[prop]`改变，那么`set`不会起作用。那曾经是`useState`的工作:)

二、如果事情确实是`set`，通过`afterSet`，我们对屏幕进行调度。这里的`v => v + 1`是一个伪计数器，它只是触发渲染。

`dispatch`是一个本地分派，它只尝试从使用这个`useProxy`的组件开始更新屏幕。好了，有了这个，让我们把它插入我们的前端代码:

```
const App = () => {
  const p = useProxy(counter)
  return <h1>{p.count}</h1>
}
```

一开始没什么特别的，上面的代码确保我们可以显示当前的计数。但是，如果我们想递增计数器，我们可以这样做

```
<button onClick={() => { **p.count++** }> + <button>
```

或者我们可以

```
<button onClick={() => { **p.inc(1)** }> + <button>
```

哇哦。也许你没有被打动。也许你是。这是整个练习。请注意我们在哪里定义了所有的状态和动作。是的，他们坐在一个单元里。

以上是一个简单的例子，如果您对实现感兴趣，您可以看到我在包`proxy-states`中发布的一个生产就绪解决方案:

【https://github.com/windmaomao/proxy-state】

**字幕**

我在一个更复杂的业余爱好项目中使用过这个包。在不讨论它的作用的情况下，我将分享这个独立的单元文件。

```
const E = require('../shared/events')const DURATION_NORMAL = 1
const DURATION_QUICK = 0.5
const DURATION_PLAY = 2const _defaultLines = s => s.split("\n")const marquee = api => ({
  // lines of text
  lines: _defaultLines(api.text),
  // line number
  line: 0,
  // font size,
  size: 30,
  // roll speed
  duration: DURATION_NORMAL,
  // text color
  color: '#000',
  // line height
  height: 36,
  // if in editing mode
  editing: false,
  // editing text
  text: '',
  // internal ref
  ref: {
    // auto play tracker
    interval: null,
    // input ref
    input: null
  }, // methods
  initialize: function (m, ipc) {
    ipc.on(E.incSize, () => { m.increment() })
    ipc.on(E.decSize, () => { m.decrement() })
    ipc.on(E.rewind, () => { m.rewind() })
    ipc.on(E.save, () => { ipc.send(E.text, m.lines.join('\n')) })
    ipc.on(E.next, () => { m.next() })
    ipc.on(E.prev, () => { m.prev() })
    ipc.on(E.play, () => { m.play() })
    ipc.on(E.edit, () => { !m.editing ? m.edit() : m.display() })
  },
  teardown: function () {
    const { interval } = m.ref
    interval && clearInterval(interval)
  },
  decrement: function (m) { m.size-- },
  increment: function (m) { m.size++ },
  prev: function (m) { m.line-- },
  next: function (m) { m.line++ },
  rewind: function (m) {
    m.line = 0
    m.duration = DURATION_QUICK
    setTimeout(() => { m.duration = DURATION_NORMAL }, 500)
  },
  play: function (m) {
    if (m.ref.interval) {
      clearInterval(m.ref.interval)
      m.ref.interval = null
    } else {
      m.ref.interval = setInterval(
        () => { m.next() },
        DURATION_PLAY * 1000
      )
    }
  },
  edit: function (m) {
    m.text = m.lines[m.line]
    setTimeout(() => {
      m.ref.input.focus()
    }, 0)
    m.editing = true
  },
  display: function (m) {
    m.lines[m.line] = m.text
    setTimeout(() => {
      m.ref.input.blur()
    }, 0)
    m.editing = false
  }
})module.exports = marquee
```

对我来说，令人惊讶的部分是该单元是独立的，它还可以与渲染系统集成在一起工作(或者在这种情况下*反应*和*电子*)。当然，这种力量源于拥有一个 redux-kind 系统。这一点也不奇怪。然而，如果我们看看这样做的成本，你可能会发现它便宜得多。

*更多内容看*[***plain English . io***](http://plainenglish.io/)