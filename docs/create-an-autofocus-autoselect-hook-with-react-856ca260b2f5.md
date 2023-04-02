# 用 React 创建自动对焦/自动选择挂钩

> 原文：<https://javascript.plainenglish.io/create-an-autofocus-autoselect-hook-with-react-856ca260b2f5?source=collection_archive---------2----------------------->

![](img/5e91898ce29c656dc8803126a1fe846f.png)

Photo by [Japheth Mast](https://unsplash.com/@japhethmast?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如果您不熟悉钩子，或者想看一个有趣的例子，本文将演示如何将一些通用代码抽象成钩子，以便在您的代码中反复使用。

## 使用自动聚焦挂钩

让我们解开这段代码，因为有很多事情要做。首先，一个钩子只是一个需要在函数的每一次渲染中在 [**上运行的函数。**](https://reactjs.org/docs/hooks-rules.html#only-call-hooks-from-react-functions)当我们看到下面的组件代码时，我们将看到如何运行它。现在，只要理解这个钩子是一个函数，它接受一个参数，这个参数将决定当我们选择它时，我们是否想要选择和高亮显示输入中的文本。

在第 5 行和第 7 行，我们创建 refs 来保存值。T **第 5 行的 ref 确保一旦 isSelectText 的初始值被传入，它就不会被更改。我们需要这样做，以便 useEffect 在** [**下面，这样 linter 就不会抛出关于缺少依赖项的警告**](https://github.com/facebook/react/issues/14920) **。**

第 10 行是一个检查，以确保我们不会得到一个空引用(这是不应该发生的)。**之后，我们聚焦文本框，然后根据传入钩子的内容选择或不选择文本(isSelectText)。**

**最后，我返回一个具有属性‘ref’的对象，它包含我们关注的输入元素 ref。有些人可能不同意我返回一个对象而不是一个数组的决定，但是我认为这严重限制了使用对象析构所能达到的代码的整洁。**

## 使用 useAutoFocus 挂钩

现在我们有了钩子，让我们把它用在一个简单的输入上，看看它的神奇之处。

**在第 14 行，我调用了钩子并析构了返回值。这允许我将从钩子返回的对象的“ref”属性传递给子元素/组件。**如果您不喜欢全部放在一行中，您可以很容易地调用 return 语句上面的钩子，并将 ref={ < ref > }赋给 input 元素。

## 包扎

我希望你喜欢阅读这篇文章和我的钩子。请在您的代码中自由使用此代码，并根据您的需要进行修改。另外，如果你想看到更多类似的内容，请留下一些掌声并关注我。编码快乐！

回购:[https://doughill1000.github.io/auto-focus-hook/](https://github.com/doughill1000/auto-focus-hook)

工作实例:[https://doughill1000.github.io/auto-focus-hook/](https://doughill1000.github.io/auto-focus-hook/)

*更多内容看*[***plain English . io***](http://plainenglish.io/)