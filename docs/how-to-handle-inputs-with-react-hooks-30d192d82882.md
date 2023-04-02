# 如何用 React 钩子处理输入？

> 原文：<https://javascript.plainenglish.io/how-to-handle-inputs-with-react-hooks-30d192d82882?source=collection_archive---------14----------------------->

![](img/e3820704397460380404bc7606a2e918.png)

Photo by [Egor Myznik](https://unsplash.com/@vonshnauzer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

处理输入值是我们在 React 应用程序中经常要做的事情。

在本文中，我们将了解如何在 React 组件中处理输入。

# 处理输入

为了处理输入，我们可以写:

```
import { useState } from "react";const initialState = {
  username: "",
  email: "",
  password: ""
};export default function App() {
  const [{ username, email, password }, setState] = useState(initialState); const onChange = (e) => {
    const { name, value } = e.target;
    setState((prevState) => ({ ...prevState, [name]: value }));
  }; return (
    <form>
      <div>
        <label>
          Username:
          <input value={username} name="username" onChange={onChange} />
        </label>
      </div>
      <div>
        <label>
          Email:
          <input value={email} name="email" onChange={onChange} />
        </label>
      </div>
      <div>
        <label>
          Password:
          <input
            value={password}
            name="password"
            type="password"
            onChange={onChange}
          />
        </label>
      </div>
      <button>Submit</button>
    </form>
  );
}
```

我们用`useState`钩子创建一个状态。

它的初始值被设置为具有`username`、`email`和`password`属性的对象。

然后我们用`onChange`函数来更新状态的值。

我们通过回调来调用`setState`以获得状态的当前值`prevState`。

我们返回一个新对象，它是`prevState`的副本，但是将`[name ]`的动态属性设置为`e.target.value`。

`e.target.value`有输入值。

在此之下，我们有带有`value`属性的输入来设置这些输入字段的输入值。

并且`onChange`属性被设置为`onChange`函数，该函数让我们将状态更新为我们想要的状态。

# 结论

我们可以通过获取用`e.target.value`输入的值来处理输入值。

然后，我们可以用新值更新状态对象，方法是复制它，并用 state setter 函数中的回调覆盖我们想要的属性值。

*更多内容看* [***说白了. io***](https://plainenglish.io/)