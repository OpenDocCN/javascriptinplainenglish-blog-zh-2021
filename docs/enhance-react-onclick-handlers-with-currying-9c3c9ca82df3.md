# 用 Currying 增强 React onClick 处理程序

> 原文：<https://javascript.plainenglish.io/enhance-react-onclick-handlers-with-currying-9c3c9ca82df3?source=collection_archive---------1----------------------->

![](img/aaef5cb1fccdabfbd164eb5377c8bfe8.png)

我想分享一个我在 React 组件中处理 onClick 处理程序时喜欢使用的设计模式。

对于我的例子，我将使用 React 中常见的设计模式来点击列表项。

我的组件工作如下:

因为我的`onClcikItem`有一个参数，所以我的按钮需要先用一个匿名函数调用它。

```
<button onClick={() => onClickItem(item)}>My Button</button>
```

这工作得很好，但是我可以用 Javascript 中一种叫做 Currying 的技术来清理一下。

*Currying 是一种将接受多个参数的函数转换成一系列接受单个参数的函数的技术*

Currying 经常在函数式编程环境中使用，但是我们仍然可以在我们的例子中利用它。

一个常见的奉承例子是这样的:

```
// Original functionfunction multiply(x,y,z) { return x * y * z
}console.log(multiply(1,2,3))// Curried versionfunction multiply(x) {
    return (y) => {
        return (z) => {
            return x * y * z
        }
    }
}console.log(multiply(1)(2)(3))
```

新函数返回导致最终值的函数。

我们可以使用这种技术从 onClickItem 函数中返回一个匿名函数，该函数满足按钮的 onClick 处理程序。

我的 curried onClickItem 函数现在看起来像这样

```
const onClickItem = (item: any) => () => { console.log("Item: ", item);};
```

通过 curried 函数，我可以更新我的按钮，这样使用它:

```
<button onClick={onClickItem(item)}>My Button</button>
```

这个函数的初始调用现在将返回一个匿名函数，可以用来代替我原来的箭头函数`onClick={ () =>`。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)