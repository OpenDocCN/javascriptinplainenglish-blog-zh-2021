# 如何在笑话中模仿 React 组件

> 原文：<https://javascript.plainenglish.io/how-to-mock-a-react-component-in-jest-1fed64768b47?source=collection_archive---------8----------------------->

![](img/53fe42930f5c8fc02aa7603650c7f29e.png)

测试是反应开发最重要的方面之一。没有测试，你就不能相信你的代码会像预期的那样工作。出于测试目的，模拟 React 组件可能是相关的。本文将向您展示如何使用 Jest 在不同的场景中模拟 React 组件。使用这些信息，您将知道如何模仿默认的导出组件、命名的导出组件、来自 ES6 模块的组件以及它们所包含的属性。

# 默认导出

要模仿 React 组件，最直接的方法是使用`jest.mock`函数。您模仿导出组件的文件，并用自定义实现替换它。因为组件基本上是一个函数，所以 mock 也应该返回一个函数。实现将如下所示。

```
jest.mock("./AwesomeComponent", () => () => {
  const MockName = "default-awesome-component-mock";
  return <MockName />;
});// Tests
```

这假设您模仿的组件是文件的默认导出。除此之外，它还为测试环境中的组件创建了一个自定义名称。这将简化生成的 DOM 结构，这在快照测试中很有用。

# 命名出口

如上所述，前面的实现是针对默认导出文件的组件的。但是，如何模拟一个作为文件的命名导出的 React 组件呢？为此，实现应该模拟文件的整个导出，而不仅仅是默认导出。看起来应该是这样的。

```
jest.mock("./AwesomeComponent", () => ({
  AwesomeComponent: () => {
    const MockName = "named-awesome-component-mock";
    return <MockName />;
  },
}));
```

mock 没有返回函数，而是返回一个对象来替换文件的导出。在对象内部，我们声明需要替换的属性。然后，我们可以为它指定替换代码，这与我们之前使用的函数相同。

如果您正在处理 ES6 模块，您将需要一些额外的配置来使它工作。具体来说，您需要将`__esModule`属性添加到导出的对象中，并将其设置为 true。这表明您正在处理 ES6 模块，并使一切正常工作。实现将如下所示。

```
jest.mock("./AwesomeComponent", () => ({
	__esModule: true,
  AwesomeComponent: () => {
    const MockName = "named-awesome-component-mock";
    return <MockName />;
  },
}));
```

# 包括道具

我们现在知道了如何为一个组件创建一个模拟，它可以是一个文件的默认或命名导出。但是问题是当前的 mock 覆盖了组件的所有内容，包括 DOM 结构和 props。在某些场景中，我们想要模仿与组件相关的一切，但仍然保留用于测试目的的道具。

```
jest.mock("./AwesomeComponent", () => ({
  AwesomeComponent: (props) => {
    const MockName = "named-awesome-component-mock";
    return <MockName {...props} />;
  },
}));
```

幸运的是，将道具添加回我们的模拟实现并不需要太多的努力。类似于如何为一个普通的 React 组件定义 props，我们需要捕获函数参数并将它们传递给呈现的元素。这样做将包括传递给模拟组件的道具，并允许我们在测试中使用它们。

# 最后的想法

出于测试目的，模拟某个 React 组件可能是相关的。本文向您展示了如何在不同的场景中模拟 React 组件。这包括默认的导出组件、命名的导出组件、来自 ES6 模块的组件，以及它们所包含的属性。

如果你喜欢这篇文章，可以考虑查看一下[不常见的 React](https://www.getrevue.co/profile/chakshunyu) 时事通讯、我的 [Twitter](https://twitter.com/keraito) 的其他条目，以便将来更新，或者我的其他(React)关于 Medium 的工作。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)