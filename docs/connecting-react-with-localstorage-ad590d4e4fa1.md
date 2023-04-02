# 连接 React 和 LocalStorage

> 原文：<https://javascript.plainenglish.io/connecting-react-with-localstorage-ad590d4e4fa1?source=collection_archive---------1----------------------->

## 创建 LocalStorage React 挂钩的指南

![](img/cdc4efcf103f82236f22fbe26f15bfb3.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 我的旅程

当 localStorage 更改时，React 不会重新呈现。为了在 UI 上更新 localStorage 值，我需要通过更新一个未使用的状态来强制组件重新呈现。这感觉像是让这个简单的概念工作的不必要的修改。如何让 localStorage 与 React 更紧密地集成在一起？

## 本地存储挂钩

利用 React 的`useState`钩子，我们可以创建一个`useLocalStorage`钩子来解决我们的问题。

```
function useLocalStorage(key, initialState) {
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

这将把数据保存到 localStorage 并触发组件重新呈现，从而在 UI 上反映新的 localStorage 值。它接受一个用作本地存储键的字符串`key`和一个用于初始化`useState`的字符串`initialState`，如果`key`的值不存在的话。然后，它使用更新的 setter 函数返回该值，该函数将更新 localStorage 和 state。

要使用，让用户与之交互的任何 UI 元素调用 setter 函数。

```
const Component = () => {
  const [value, setValue] = useLocalStorage('key', 'initial'); 
  return (
    <input
      onChange={e => setValue(e.target.value)}
      value={value ?? ''}
    />
  );
};
```

重要的是使用 setter 函数，而不是直接使用`localStorage.setItem`。如果您使用这个 setter 函数来更新 localStorage，React 只会重新渲染。

## 非字符串值

上面的实现只支持字符串值，因为这是 localStorage 官方支持的。然而，通过使用`JSON.stringify`和`JSON.parse`将布尔值、数字和对象转换为字符串，仍然可以支持它们。使用这个概念，`useLocalStorage`可以扩展到支持非字符串值。

```
function useLocalStorageNonString(key, initialState) {
  const serializedInitialState = JSON.stringify(initialState);
  let storageValue = initialState;
  try {
    storageValue = JSON.parse(localStorage.getItem(key)) ?? initialState;
  } catch {
    localStorage.setItem(key, serializedInitialState);
  }
  const [value, setValue] = useState(storageValue);
  const updatedSetValue = useCallback(
    newValue => {
      const serializedNewValue = JSON.stringify(newValue);
      if (
        serializedNewValue === serializedInitialState ||
        typeof newValue === 'undefined'
      ) {
        localStorage.removeItem(key);
      } else {
        localStorage.setItem(key, serializedNewValue);
      }
      setValue(newValue ?? initialState);
    },
    [initialState, serializedInitialState, key]
  );
  return [value, updatedSetValue];
}
```

在将值保存到 localStorage 之前，它被转换为字符串，在从 localStorage 读取值之后，它被转换为对象(或布尔或数字)。因为我们永远不能保证 localStorage 中的值是有效的 JSON，所以我们还必须处理任何解析错误。

## 警告

如果用户手动更改 localStorage 值，或者应用程序的某个其他部分在不使用`useLocalStorage`更新程序的情况下更改该值，`useLocalStorage`将不会更新到该新值。不幸的是，没有解决这个问题的办法，因为这是浏览器的限制。它们确实提供了一个您可以监听的存储事件`window.addEventListener('storage', <handler>)`，但是只有当存储事件从另一个选项卡或窗口被触发时，这个处理程序才会被触发。

## 最后的想法

我真的希望有一种本地的方式来对本地存储的变化做出反应。但是即使没有本地实现，您也可以使用自己的`useLocalStorage`钩子来实现该功能。

## 资源

*   [本文 Github 回购](https://github.com/mjchang/medium/tree/master/use-local-storage)
*   [本文的 CodeSandbox】](https://codesandbox.io/s/github/mjchang/medium/tree/master/use-local-storage)