# 了解 React 中的自定义挂钩

> 原文：<https://javascript.plainenglish.io/custom-hooks-in-react-6e78aeca44d2?source=collection_archive---------10----------------------->

![](img/4832352565a0c53d4f01b72087df1432.png)

不能说其他的，但很长一段时间，我不知道为什么钩子在基于类的 React 组件中不可用。正因为如此，每当我在类组件中使用钩子时，我都会得到一个错误，这是我不能完全理解的。但是我很高兴我在 React 中使用了功能组件。真的！我不知道为什么，但我发现为我的 React 项目编写所有这些函数很有趣。无论如何，让我们谈谈钩子，尤其是 React 中的定制钩子。

找到 React 中的钩子的最好方法是浏览 React 官方文档，其中说:

> 挂钩*是 React 16.8 中的新增功能，它让你不用写类就可以使用状态和其他 React 特性。*

在胡克之前，

```
import React from ‘react’
class App extends React.Component {
    constructor(props){
       super(props)
       this.state = { counter: 0 }
    } // rest of the code}
```

现在，用钩子，

```
import React, { useState }
const App = () => {
    const [counter, setCounter] = useState(0) //rest of the code
}
```

就像我说的，我只是喜欢功能组件的世界。当然，你明白我的意思，因为你可能两种方式都做了。我喜欢第二个。你可能会也可能不会。那很好。

## 但是如果我们已经在 React 中内置了钩子，为什么我们还需要定制钩子呢？为什么要大费周章？

说得好。但我也确信，有一天，当某些钩子没有按照你想象的方式工作时，你可能会想要更多的灵活性，或者做你想做的任何事情。尽管钩子有很多优点，但也有一些限制，这只会促使我们自己制作钩子。

*   **问题#1** :开箱即用的 react 钩子的问题是，它们只能在`functional components`或`custom hooks`本身中使用。
*   **问题#2** :此外，react 钩子只能在代码块的最顶层调用，不能嵌套在代码块的下面。这意味着如果我做了下面的事情，`useState`就不会工作。

```
const App = () => {
    // some cool logic {
        // some more cool logic
        const [counter, setCounter] = useState(0)
    }
}
```

# 输入，自定义挂钩

定制钩子没有什么特别的，除了是你和我制造它，谁决定发生什么以及如何发生。我觉得这很特别，对吧？哈哈！就像任何其他函数一样，自定义钩子可以有返回类型，可以返回字符串、数组、对象、数字——无论 JavaScript 有什么数据类型，它都可以返回。那真的很酷。

在制作我们的定制挂钩时要记住的一点是，最好将其命名为`use<HookName>`，就像有`useState`、`useEffect`、`useCallback`……你明白我的意思了。这让 React 注意到我们将来可能会做的任何违规行为，并指出来。

这里有一个定制钩子的例子— `useCounter`。在这里，我在我的自定义钩子中使用了 useState 和 useEffect，解决了我在上面第一期提到的问题。

在`useCounter.js`中(命名由您决定，尽管在开头使用单词`use`是个好主意)。

```
import { useState, useEffect }
const useCounter = () => {
    const [counter, setCounter] = useState(0) useEffect(() => {
        const interval = setInterval(() => {
             setCounter((prevCounter) => prevCounter + 1)
        }, 1000)

    return () => clearInterval(interval)

    }, []) return counter
}export default useCounter
```

这样一来，我现在可以在任何组件中使用这个钩子了。可能在应用程序组件中，或者在我的组件树中的某个组件中。

在 App.js 中，使用 useCounter 就像使用任何默认的 React 挂钩一样简单。假设我想要呈现由`useCounter`钩子返回的`counter`状态的值(一个数字)。没问题…

```
import React from 'react'const App = () => {
    const counter = useCounter() return (
        <main className = 'App'>
            <p>Counter: {counter}</p>
        </main>
    )
}export default App
```

就这么简单。当然，随着定制钩子处理的逻辑变得复杂，实现会变得有点棘手，尤其是当钩子处理 HTTP 请求时。但最核心的是，这就是 React 中定制钩子的样子，并且和普通钩子一样容易使用。

希望我能保持简单。我知道 React 中已经有了与自定义挂钩相关的文档，但是我发布其中一个的主要原因是，让我自己负责，用我的语言简化事情，并且与所有人分享我的学习之旅。

谢谢你过来。快乐反应！

*更多内容看* [***说白了就是***](http://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区获得独家访问写作机会和建议***](https://discord.gg/GtDtUAvyhW) *。*