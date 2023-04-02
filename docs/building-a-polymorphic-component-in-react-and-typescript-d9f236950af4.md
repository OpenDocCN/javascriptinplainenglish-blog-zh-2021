# 在 React 和 TypeScript 中构建多态组件

> 原文：<https://javascript.plainenglish.io/building-a-polymorphic-component-in-react-and-typescript-d9f236950af4?source=collection_archive---------0----------------------->

![](img/63271b744e33d00130cddc3f539fd54a.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/Lego?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

> “多态组件是一种可以根据其实例化方式以多种方式运行的组件”。

我目前正在开发一个[组件库](https://github.com/watife/dorai-ui)，我想要支持的特性之一是这个库的用户能够改变我最初设置的组件类型。

让我们为一个可访问的模式对话框构建一个标题组件。

上面的代码表示一个简单的标题组件，但是如果模型的消费者希望标题是一个链接或者其他 HTML 元素呢？我们如何支持多种类型的 HTML 元素？。我们可以很容易地做到这一点。

> **注意:**组件必须大写，否则 jsx 会将其视为 HTML 标签<组件>。

该类型的名称已经更改为 *"TitleOwnProps，"*，它代表我们自己定义的道具，并且它接收一个*"作为"*道具，这是类型" *React。ElementType* (应该是 HTML 元素)。此外，我正在传播其余的道具，但这不会有多大帮助，因为我们传递到标题中的 *"href"* 不被识别为有效的道具，而且，组件的类型仍然是类型 *"any。"*我们可以用不同的方式解决上述问题，但是我将使用[泛型](https://ts.chibicode.com/generics)进行演示。

" *TitleOwnProps* "现在需要泛型类型，而 *"as"* 属性被设置为传递的类型。泛型扩展了*“React。*element type；因此，它不是类型 *"any"* 而是一个 HTML 元素。

我们还需要创建一个“ *TitleProps* ”，它将选择所有的通用类型 Props，如果它们存在于我们的类型中，就用我们传递的唯一类型覆盖它们。

由于[省略了](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)，我仔细挑选了所有的 React。类型的 ComponentProps 传递并移除了我们的 TitleOwnProps 键，因为我们将自己传递它并将所有内容合并到一个道具类型" *TitleProps* "现在我们的标题组件可以接收这个新道具了。

现在我们可以有一个通用组件，如下所示:

标题组件接收类属；类型默认为*【H2】*标签。这意味着我们的 TitleProps 默认为 h2，但是 typescript 可以[推断出](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-4.html#higher-order-type-inference-from-generic-functions)通用函数类型。这使我们能够将 HTML 元素传递给“as ”,并为我们提供一个功能正常的动态组件。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***