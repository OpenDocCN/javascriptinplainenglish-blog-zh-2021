# 避免 React useEffect 中的竞争条件和内存泄漏

> 原文：<https://javascript.plainenglish.io/avoiding-race-conditions-and-memory-leaks-in-react-useeffect-2034b8a0a3c7?source=collection_archive---------3----------------------->

## 了解如何处理“无法对卸载的组件执行反应状态更新”警告

![](img/3360364f7b08e7258daf03d710b9a189.png)

让我们看一下从 API 请求中获取数据的实现，看看在这个组件中是否有发生竞争情况的可能性:

```
import React, { useEffect} from 'react';
export default function UseEffectWithRaceCondition() {
  const [todo, setTodo] = useState(null);
  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
      const newData = await response.json();
      setTodo(newData);
    };
    fetchData();
  }, []);
  if (data) {
    return <div>{data.title}</div>;
  } else {
    return null;
  }
}
```

我们已经指定了一个空数组作为对 [useEffect React 钩子](https://www.wisdomgeek.com/development/web-development/react/react-hooks-and-local-storage-lets-build-a-todo-app/)的依赖。因此，我们已经确保获取请求只发生一次。但是这个组件仍然容易出现争用情况和内存泄漏。怎么会？

如果 API 服务器花了一些时间来响应，并且在收到响应之前卸载了组件，就会发生内存泄漏。尽管组件已被卸载，但在完成时仍会收到对请求的响应。然后将解析响应并调用 setTodo。而 React 会抛出警告:

> 无法对已卸载的组件执行反应状态更新。这是不可行的，但它表明您的应用程序中存在内存泄漏。要修复此问题，请取消 useEffect 清理函数中的所有订阅和异步任务。

这个信息非常简单。

同一问题的另一个潜在场景可能是 todo 列表 ID 作为一个属性被传入。

```
import React, { useEffect} from 'react';
export default function UseEffectWithRaceCondition( {id} ) {
  const [todo, setTodo] = useState(null);
  useEffect(() => {
    const fetchData = async () => {
      const response = await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`);
      const newData = await response.json();
      setTodo(newData);
    };
    fetchData();
  }, [id]);
  if (data) {
    return <div>{data.title}</div>;
  } else {
    return null;
  }
}
```

如果钩子在请求完成之前收到了一个不同的 ID，而第二个请求在第一个请求完成之前完成，那么我们就会在组件中看到第一个请求的数据。

# 竞争条件问题的潜在解决方案

有几种方法可以解决这个问题。这两种方法都利用了 useEffect 提供的清理功能。

*   我们可以使用一个布尔标志来确保组件被安装。这样，我们只有在标志为真时才更新状态。如果我们在一个组件中发出多个请求，我们将总是显示最后一个请求的数据。
*   每当组件被卸载时，我们可以使用 AbortController 取消以前的请求。但是 IE 不支持 AbortController。所以如果我们要使用这种方法，我们需要考虑这一点。

# 使用带有布尔标志的效果清理

```
useEffect(() => {
  let isComponentMounted = true;
    const fetchData = async () => {
      const response = await fetch('https://jsonplaceholder.typicode.com/todos/1');
      const newData = await response.json();
      if(isComponentMounted) {
        setTodo(newData);
      }
    };
    fetchData();
    return () => {
      isComponentMounted = false;
    }
  }, []);
```

此修复依赖于 useEffect 的清理功能的工作方式。如果一个组件渲染多次，则在执行下一个效果之前会清除上一个效果。

由于这种工作方式，它也将正确地工作于我们的另一个多请求的例子，因为 ID 被改变了。在某种意义上，我们仍然有一个竞争条件，即在后台会有多个请求在运行。但是只有最后一次请求的结果才会显示在 UI 上。

# 使用 AbortController 清除效果

尽管前面的方法可行，但它不是处理竞争条件的最佳方式。这些请求在后台进行。在后台保存过时的请求是对用户带宽的不必要消耗。浏览器还限制了并发请求的最大数量(最多 6-8 个)。

从我们之前关于如何取消 HTTP 获取请求的帖子中，我们知道了添加到 DOM 标准中的 AbortController API。我们可以利用这一点来中止我们的请求本身。

```
useEffect(() => {
  let abortController = new AbortController();
    const fetchData = async () => {
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos/1', {
            signal: abortController.signal,
          });
      const newData = await response.json();
        setTodo(newData);
      }
      catch(error) {
         if (error.name === 'AbortError') {
          // Handling error thrown by aborting request
        }
      }
    };
    fetchData();
    return () => {
      abortController.abort();
    }
  }, []);
```

由于中止请求会抛出一个错误，我们需要显式地处理它。

这个解决方案的工作原理和前面的一样。在重新渲染的情况下，清理功能在执行下一个效果之前执行。不同之处在于浏览器也取消了请求，因为我们使用的是 AbortController。

这是我们在使用 React 的 useEffect 钩子发出 API 请求时避免竞争情况的两种方法。如果您想使用一些第三方库，这些库允许将取消请求作为一个特性，那么您可以使用 Axios 或 react query，它们也提供了许多其他特性。

如果你有任何问题，请在下面留言。

*原载于 2021 年 2 月 8 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/react/avoiding-race-conditions-memory-leaks-react-useeffect/)*。*