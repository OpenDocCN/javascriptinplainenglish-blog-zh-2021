# 测试反应挂钩

> 原文：<https://javascript.plainenglish.io/testing-react-hooks-1fee0bfdbf42?source=collection_archive---------2----------------------->

## React 钩子测试库使用指南

![](img/239b2c21ad565fb8e80e9e8e03cc3d80.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 我的旅程

随着我越来越多地使用钩子，我也开始创建自己的钩子来将功能归纳到公共代码中。自然，下一个合乎逻辑的步骤将是测试。但是，我很快发现这个过程并不像我想象的那么简单。在测试中直接调用一个钩子会触发这个错误:

```
Invalid hook call. Hooks can only be called inside of the body of a function component.
```

但是我如何在测试中做到这一点呢？

# React 钩子测试库

[反应钩子测试库](https://react-hooks-testing-library.com/)来救援。它提供了一个`renderHook` API，将钩子包装在一个函数组件中来解决错误。这个 API 将返回有用的实用程序，使您能够完全测试您的钩子。

# 例子

让我们以一个连接 React 和 localStorage 的[简单钩子](/connecting-react-with-localstorage-ad590d4e4fa1)为例:

```
import { useCallback, useState } from 'react';export default function useLocalStorage(key, initialState) {
  const [value, setValue] = useState(localStorage.getItem(key) ?? initialState);
  const updatedSetValue = useCallback(
    newValue => {
      if (newValue === initialState || typeof newValue === 'undefined') {
        localStorage.removeItem(key);
      } else {
        localStorage.setItem(key, newValue);
      }
      setValue(newValue ?? initialState);
    },
    [initialState, key]
  );
  return [value, updatedSetValue];
}
```

这个简单的钩子就像 React 的本机`useState`钩子一样，将状态与 localStorage 同步。

现在，使用 React Hooks 测试库，让我们首先从一些简单的测试开始，以确保输出是正确的。

```
import { act, renderHook } from '[@testing](http://twitter.com/testing)-library/react-hooks';import useLocalStorage from './useLocalStorage';beforeEach(() => localStorage.clear());
afterEach(() => localStorage.clear());const key = 'KEY';test('should return localStorage value', () => {
  localStorage.setItem(key, 'value');
  const { result } = renderHook(() => useLocalStorage(key));
  expect(result.current).toStrictEqual(
    ['value', expect.any(Function)]
  );
});test('should return the default value', () => {
  const initialState = 'default';
  const { result } = renderHook(
    () => useLocalStorage(key, initialState)
  );
  expect(result.current).toStrictEqual(
    ['default', expect.any(Function)]
  );
});
```

`renderHook`接受一个调用钩子的函数。这将返回一个包含钩子返回值的`result.current`。然后对这个值进行测试，以确保它符合我们的预期。很简单，对吧？

# 相互作用

`useLocalStorage`钩子也返回一个更新状态值的 setter。使用 React Hooks 测试库与这个 setter 交互也很简单。

```
import { act, renderHook } from '[@testing](http://twitter.com/testing)-library/react-hooks';const key = 'KEY';test('should update when set is called', () => {
  const initialState = 'default';
  const { result } = renderHook(
    () => useLocalStorage(key, initialState)
  );
  expect(result.current).toStrictEqual(
    ['default', expect.any(Function)]
  );
  const [, setValue] = result.current;
  act(() => {
    setValue('value');
  });
  expect(localStorage.getItem(key)).toEqual('value');
  expect(result.current).toStrictEqual(
    ['value', expect.any(Function)]
  );
});
```

这里，用新值调用`setValue`，并检查 localStorage 和`result.current`以确保状态被正确更新。`setValue`被包装在一个`act`调用中，因此状态更新可以发生。

注意:React 测试库只是用更新后的值从`renderHook`调用中变异出原始的`result.current`。因此，执行以下操作将不起作用:

```
const [value, setValue] = result.current;
act(() => {
  setValue('value');
});
expect(value).toEqual('value');
```

# RenderHook API

## 投入

`renderHook`函数也支持选项对象作为第二个参数。

**包装器**用于在附加的 React 组件中包装钩子。这是用来给你的钩子提供它需要的额外的上下文。例如，如果你的钩子需要 Redux 的`dispatch`，你可以将 Redux 的`Provider`作为包装器传递，这样`useDispatch`就可以工作了。

```
import { createStore } from 'redux';
import { Provider, useDispatch } from 'react-redux'function hook() {
  const dispatch = useDispatch();
  ...
}test('should work', () => {
  const wrapper = ({ children }) => (
    <Provider store={createStore()}>
      {children}
    </Provider>
  );
  const { result } = renderHook(() => hook(), { wrapper });
});
```

**initialProps** 用于设置初始挂钩值。它通常与`renderHook`的**重新渲染**结合使用，以模拟道具变化。

```
function hook(value) {
  ...
  return value;
}test('should return updated value', () => {
  const { rerender, result } = renderHook(
    ({ value }) => hook(value),
    { initialProps: { value: 'initial' }}
  );
  expect(result.current).toEqual('initial');
  rerender({ value: 'updated' });
  expect(result.current).toEqual('updated');
});
```

## 输出

`renderHook`函数输出一个对象。你已经熟悉了`result`，但是还有其他有用的方法可以帮助测试钩子的整个生命周期。

rerender 是一个可以被调用的函数，用新的道具重新渲染钩子，新的道具作为参数传入。参见上面的`initialProps`示例。

**unmount** 是一个函数，可以被调用来模拟组件被从 DOM 中移除。它用来触发`useEffect`清理效果。

```
import { useEffect } from 'react';function hook() {
  ...
  useEffect(() => {
    console.log('mounted');
    return () => console.log('unmounting');
  }, []);
};test('should trigger cleanup effect', () => {
  jest.spyOn(console, 'log');
  const { unmount } = renderHook(() => hook());
  expect(console.log).toHaveBeenCalledWith('mounted');
  unmount();
  expect(console.log).toHaveBeenCalledWith('unmounting');
});
```

# 最后的想法

React hooks 测试库提供了一个简单的框架来全面测试你定制的 React Hooks 并实现完整的测试覆盖。有了它，您可以轻松地测试一个钩子从挂载到更新再到卸载的整个生命周期。既然你已经学会了这一点，那就出去确保你的 React 钩子没有 bug！

# 资源

*   [官方 React 钩子测试库文档](https://react-hooks-testing-library.com/)
*   [本文 Github 回购](https://github.com/mjchang/medium/tree/master/testing-hooks)
*   [本文的 code sandbox](https://codesandbox.io/s/github/mjchang/medium/tree/master/testing-hooks?file=/src/useLocalStorage.test.js)