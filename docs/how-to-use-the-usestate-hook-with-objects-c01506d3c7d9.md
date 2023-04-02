# 如何对对象使用 useState 钩子？

> 原文：<https://javascript.plainenglish.io/how-to-use-the-usestate-hook-with-objects-c01506d3c7d9?source=collection_archive---------14----------------------->

![](img/e0431361e4df014035bf5ef265a60713.png)

Photo by [Vidar Nordli-Mathisen](https://unsplash.com/@vidarnm?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 程序中，我们经常要处理对象值。

因此，我们经常需要创建对象状态并更新它们。

在本文中，我们将研究如何在 React 组件中更新对象状态。

# 合并对象

用新属性值更新对象状态的主要方法是将旧对象与新属性合并。

例如，我们可以写:

```
import { useState } from "react";export default function App() {
  const [name, setName] = useState({
    firstName: "",
    middleName: "",
    lastName: ""
  }); return (
    <div className="App">
      <input
        value={name.firstName}
        type="text"
        onChange={(e) =>
          setName((name) => ({ ...name, firstName: e.target.value }))
        }
        name="firstName"
        placeholder="first name"
      />
      <br />
      <input
        value={name.middleName}
        type="text"
        onChange={(e) =>
          setName((name) => ({ ...name, middleName: e.target.value }))
        }
        name="middleName"
        placeholder="middle name"
      />
      <br />
      <input
        value={name.lastName}
        type="text"
        onChange={(e) =>
          setName((name) => ({ ...name, lastName: e.target.value }))
        }
        name="lastName"
        placeholder="last name"
      />
    </div>
  );
}
```

我们有一个设置为对象初始值的`name`状态。

在此之下，我们添加了 3 个输入元素。

它们中的每一个都将`onChange`属性设置为调用`setName`的函数。

我们将一个回调传递给接受`name`参数的`setName`函数，该参数具有`name`状态的当前值。

它返回一个对象，用 spread 操作符复制了`name`的属性。

然后我们在它的末尾添加我们想要改变的属性。

它必须在末尾，以便新属性覆盖原始状态下已经存在的属性值。

`e.target.value`有输入值。

我们还可以通过创建一个函数来减少重复，该函数返回一个改变我们想要的属性的函数。

为此，我们写道:

```
import { useState } from "react";export default function App() {
  const [name, setName] = useState({
    firstName: "",
    middleName: "",
    lastName: ""
  }); const handleChange = (field) => {
    return (e) => setName((name) => ({ ...name, [field]: e.target.value }));
  }; return (
    <div className="App">
      <input
        value={name.firstName}
        type="text"
        onChange={handleChange("firstName")}
        name="firstName"
        placeholder="first name"
      />
      <br />
      <input
        value={name.middleName}
        type="text"
        onChange={handleChange("middleName")}
        name="middleName"
        placeholder="middle name"
      />
      <br />
      <input
        value={name.lastName}
        type="text"
        onChange={handleChange("lastName")}
        name="lastName"
        placeholder="last name"
      />
    </div>
  );
}
```

我们有返回状态改变函数的`handleChange`函数。

它接受`field`参数，我们通过将它传递到`setName`回调中返回的对象的括号中，将它用作属性名。

# 结论

我们可以对对象使用`useState`钩子，方法是向我们的状态改变函数传递一个回调，返回现有状态对象的副本，然后将属性设置为我们想要的值。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)