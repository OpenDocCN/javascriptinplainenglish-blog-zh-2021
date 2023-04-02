# 反应道具举例说明

> 原文：<https://javascript.plainenglish.io/react-props-explained-with-examples-3d245d19ba2d?source=collection_archive---------1----------------------->

## 通过实例了解 React 道具。

![](img/121732287ba5a2bcb1e57865de2db42c.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 介绍

React 是一个非常棒的用于构建用户界面的 JavaScript 库。它用于创建组件，处理状态和**属性**，利用事件监听器和某些生命周期方法在数据发生变化时更新数据。你需要知道如何使用 React 来做所有这些事情，因为这是一项有价值的技能。

在本文中，我们将通过一些实际的例子来学习一些关于 React props 的知识。但是在开始阅读本文之前，您需要对 JSX 和 React 组件有一些基本的了解。所以让我们开始吧。

# 有哪些道具？

Props 是传递给 React 组件的参数。它们可以通过 HTML 属性传递给组件。React 属性就像 JavaScript 中的函数参数*和 HTML 中的*属性。

假设您有一个组件`App`，它呈现了一个名为`Navbar`的子组件，这是一个无状态的功能组件。您可以通过编写以下内容将一个`name`属性传递给`Navbar`:

```
<App>
  <Navbar name='about' />
</App>
```

由于`Navbar`是一个无状态的功能组件，它可以像这样访问这个值:

```
const Navbar = (**props**) => <h2> {**props.name**} <h2/>
// about
```

标准的做法是调用这个值`props`，当处理无状态的功能组件时，你基本上把它当作一个返回 JSX 的函数的参数。您可以在函数体中访问参数的值。但是对于类组件，这有一点不同。

# 传递一个数组作为道具

要将一个数组传递给 JSX 元素，它必须被视为 JavaScript 并被括在花括号中`{}`。

这里有一个例子:

```
<ParentComponent>
  <ChildComponent colors=**{["green", "blue", "red"]}** />
</ParentComponent>
```

如果子组件是无状态的功能组件，那么在访问属性`colors`时，可以使用`join()`之类的数组方法。

看看下面的例子:

```
const ChildComponent = (**props**) => <p>**{props.colors.join(', ')}**</p>
```

这将把所有的`colors`数组项连接成一个逗号分隔的字符串，并产生:`<p>green, blue, red</p>`。

# 默认道具

可以将默认属性作为组件本身的属性分配给组件，如果需要，React 会分配默认属性。如果没有提供值，将添加此默认属性。如果属性未定义，React 会指定默认属性。

下面是将默认属性传递给组件的方法:

```
**MyComponent.defaultProps = { location: 'USA' }**
```

在上面的例子中，我们定义了一个设置为字符串`USA`的位置属性。

# 将道具传递给类组件

在上面的例子中，您学习了如何将属性传递给无状态的功能组件。但是 ES6 类组件使用稍微不同的约定来访问 props。

每当你引用一个类组件时，你可以使用关键字`**this**`。要访问一个类组件中的 props，您可以在用来访问它的代码前面加上`**this**`。例如，如果一个 ES6 类组件有一个名为 data 的属性，你可以在 JSX 写`**{this.props.data}**`。

假设您有一个父类组件，它呈现另一个子类组件，并传递了一个 prop `name`。在这种情况下，你可以使用`this.props.name`来获得道具。

这里有一个例子:

```
class **ChildComponent** extends React.Component { constructor(props) { super(props);
 } render() { return ( <div>
    {/* Accecssing the prop with the this keyword */} <h1> My name is: {**this.props.name**} </h1> </div>
 );
 }
 };class **ParentComponent** extends React.Component {constructor(props) { super(props);
}render() { return ( <div> {/* Rendering the child component */}
     <**ChildComponent** **name="Mehdi"** />
  </div>
);
}
};{/* Renders: My name is: Mehdi */}
```

# 结论

在 React 中使用组件时，React 道具非常有用和重要。它们可以采用任何本地 JavaScript 类型。所以你需要对 React 的这个基本特性有一个扎实的理解。

感谢您阅读本文，希望您觉得有用。如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

# 更多阅读

[](https://medium.com/javascript-in-plain-english/the-front-end-web-developer-roadmap-for-2021-bcf88c5d4ccd) [## 2021 年前端 Web 开发者路线图

### 成为现代前端 web 开发人员的一步一步指南。

medium.com](https://medium.com/javascript-in-plain-english/the-front-end-web-developer-roadmap-for-2021-bcf88c5d4ccd)