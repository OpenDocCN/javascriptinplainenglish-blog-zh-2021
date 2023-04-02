# 15 个定制挂钩，使您的 React 组件重量轻

> 原文：<https://javascript.plainenglish.io/15-custom-hooks-to-make-your-react-component-lightweight-8b59b122d83a?source=collection_archive---------0----------------------->

下面是 15 个定制钩子，让你的 React 组件轻量级

![](img/657497b80b4331dfc7243e2584ab7779.png)

Photo by [Arnold Francisca](https://unsplash.com/@clark_fransa?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/coding?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

React hooks 是 React 社区的热门词汇。希望每个 React 开发者都知道钩子是什么。简单地说，钩子提供了在功能组件中使用生命周期方法的优势，也鼓励我们编写功能组件。

让我们开始定制挂钩吧！定制钩子允许您将组件逻辑提取到一个可重用的函数中，这增加了组件分离和可靠性。这里我们将看到 15 个[react——使用](https://github.com/streamich/react-use)包定制钩子，使我们的组件变得轻量级。

# **1。使用空闲**

useIdle 挂钩跟踪页面上的用户是否空闲。您可以传递两个参数— `ms`是考虑空闲的时间，`initialState`允许用户最初设置空闲。

```
import {useIdle} from 'react-use';const Demo = () => {
  const isIdle = useIdle(3e3);return (
    <div>
      <div>User is idle: {isIdle ? 'Yes 😴' : 'Nope'}</div>
    </div>
  );
};
```

# 2.使用间隔

用于间隔相关功能的挂钩。它在组件自动卸载时处理`clearInterval`。它还允许通过将延迟设置为空来暂停时间间隔。

```
import * as React from 'react';
import {useInterval} from 'react-use';const Demo = () => {
  const [count, setCount] = React.useState(0);
  const [delay, setDelay] = React.useState(1000);
  const [isRunning, toggleIsRunning] = useBoolean(true);useInterval(
    () => {
      setCount(count + 1);
    },
    isRunning ? delay : null
  );return (
    <div>
      <div>
        delay: <input value={delay} onChange={event => setDelay(Number(event.target.value))} />
      </div>
      <h1>count: {count}</h1>
      <div>
        <button onClick={toggleIsRunning}>{isRunning ? 'stop' : 'start'}</button>
      </div>
    </div>
  );
};
```

# 3.使用滚动条

这个钩子用于监听元素的滚动事件，并在滚动时重新呈现。不需要手动添加 JavaScript 事件侦听器。

```
import {useScroll} from 'react-use';const Demo = () => {
  const scrollRef = React.useRef(null);
  const {x, y} = useScroll(scrollRef);return (
    <div ref={scrollRef}>
      <div>x: {x}</div>
      <div>y: {y}</div>
    </div>
  );
};
```

# 4.使用开关

这个钩子用于在两种状态之间切换，比如真、假。这种方法减少了人工逻辑。

```
import {useToggle} from 'react-use';const Demo = () => {
  const [on, toggle] = useToggle(true);return (
    <div>
      <div>{on ? 'ON' : 'OFF'}</div>
      <button onClick={toggle}>Toggle</button>
      <button onClick={() => toggle(true)}>set ON</button>
      <button onClick={() => toggle(false)}>set OFF</button>
    </div>
  );
};
```

# **5。使用标题**

这个钩子用来设置页面标题。

```
import {useTitle} from 'react-use';const Demo = () => {
  useTitle('Hello world!');return null;
};
```

# 6.使用以前的

这个钩子用于获取前一个状态。我们可能不需要编写定制的逻辑来获取以前的状态。

```
import {usePrevious} from 'react-use';const Demo = () => {
  const [count, setCount] = React.useState(0);
  const prevCount = usePrevious(count);return (
    <p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <button onClick={() => setCount(count - 1)}>-</button>
      <p>
        Now: {count}, before: {prevCount}
      </p>
    </p>
  );
};
```

# **7。使用设置状态**

这个钩子用于将对象合并到它们的当前状态，类似于类组件中的`this.setState`。如果你正在使用多个状态，可以使用`useSetState`将其降低到一个对象状态

```
import {useSetState} from 'react-use';const Demo = () => {
  const [state, setState] = useSetState({});return (
    <div>
      <pre>{JSON.stringify(state, null, 2)}</pre>
      <button onClick={() => setState({hello: 'world'})}>hello</button>
      <button onClick={() => setState({foo: 'bar'})}>foo</button>
      <button 
        onClick={() => {
          setState((prevState) => ({
            count: (prevState.count || 0) + 1,
          }))
        }}
      >
        count
      </button>
    </div>
  );
};
```

# 8.使用 Cookie

这个钩子用于返回一个`cookie`的当前值，一个更新`cookie`的回调和一个删除`cookie.`的回调

```
import { useCookie } from "react-use";const Demo = () => {
  const [value, updateCookie, deleteCookie] = useCookie("my-cookie");
  const [counter, setCounter] = useState(1);useEffect(() => {
    deleteCookie();
  }, []);const updateCookieHandler = () => {
    updateCookie(`my-awesome-cookie-${counter}`);
    setCounter(c => c + 1);
  };return (
    <div>
      <p>Value: {value}</p>
      <button onClick={updateCookieHandler}>Update Cookie</button>
      <br />
      <button onClick={deleteCookie}>Delete Cookie</button>
    </div>
  );
};
```

# 9.使用权限

这个钩子用来获取浏览器 API 的权限状态。传递 API 名称以获取权限状态。

```
import {usePermission} from 'react-use';const Demo = () => {
  const state = usePermission({ name: 'microphone' });return (
    <pre>
      {JSON.stringify(state, null, 2)}
    </pre>
  );
};
```

# 10.使用反跳

这个钩子用于延迟事件，直到等待时间结束。在下面的代码中，setState 在等待时间结束后执行。

```
const Demo = () => {
  const [state, setState] = React.useState('Typing stopped');
  const [val, setVal] = React.useState('');
  const [debouncedValue, setDebouncedValue] = React.useState('');const [, cancel] = useDebounce(
    () => {
      setState('Typing stopped');
      setDebouncedValue(val);
    },
    2000,
    [val]
  );return (
    <div>
      <input
        type="text"
        value={val}
        placeholder="Debounced input"
        onChange={({ currentTarget }) => {
          setState('Waiting for typing to stop...');
          setVal(currentTarget.value);
        }}
      />
      <div>{state}</div>
      <div>
        Debounced value: {debouncedValue}
        <button onClick={cancel}>Cancel debounce</button>
      </div>
    </div>
  );
};
```

# 11.使用地理定位

这个钩子用于获取用户的地理位置。useGeolocation 返回纬度、经度、海拔和更多信息。

```
import {useGeolocation} from 'react-use';const Demo = () => {
  const state = useGeolocation();return (
    <pre>
      {JSON.stringify(state, null, 2)}
    </pre>
  );
};
```

# 12.使用网络状态

这个钩子用来获取浏览器的网络状态。useNetworkState 可用于向用户显示连接状态。

```
import {useNetworkState} from 'react-use';const Demo = () => {
  const state = useNetworkState();return (
    <pre>
      {JSON.stringify(state, null, 2)}
    </pre>
  );
};
```

# 13.使用 CopyToClipboard

useCopyToClipboard 钩子用于将文本复制到剪贴板。

```
const Demo = () => {
  const [text, setText] = React.useState('');
  const [state, copyToClipboard] = useCopyToClipboard();

  return (
    <div>
      <input value={text} onChange={e => setText(e.target.value)} />
      <button type="button" onClick={() => copyToClipboard(text)}>copy text</button>
      {state.error
        ? <p>Unable to copy value: {state.error.message}</p>
        : state.value && <p>Copied {state.value}</p>}
    </div>
  )
}
```

# 14.使用图标

useFavicon 挂钩用于设置页面的 Favicon。

```
import {useFavicon} from 'react-use';const Demo = () => {
  useFavicon('[https://cdn.sstatic.net/Sites/stackoverflow/img/favicon.ico'](https://cdn.sstatic.net/Sites/stackoverflow/img/favicon.ico'));return null;
};
```

# 15.使用错误

useError 挂钩用于分派错误。

```
import { useError } from 'react-use';const Demo = () => {
  const dispatchError = useError();const clickHandler = () => {
    dispatchError(new Error('Some error!'));
  };return <button onClick={clickHandler}>Click me to throw</button>;
};// In parent app
const App = () => (
  <ErrorBoundary>
    <Demo />
  </ErrorBoundary>
);
```

# **结论**

在 [react-use](https://github.com/streamich/react-use) 包中还有一些自定义的钩子，希望你觉得有用。感谢您的阅读。

需要学习更多？欢迎随时在[推特](https://twitter.com/Nilanth)上联系。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)