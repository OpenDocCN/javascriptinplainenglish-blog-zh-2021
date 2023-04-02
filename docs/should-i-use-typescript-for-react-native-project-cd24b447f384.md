# 我应该为我的反应本地项目使用类型脚本吗？

> 原文：<https://javascript.plainenglish.io/should-i-use-typescript-for-react-native-project-cd24b447f384?source=collection_archive---------2----------------------->

![](img/ef90732ee4423e1bc2aba0f26c05ec59.png)

Photo by [James Harrison](https://unsplash.com/@jstrippa?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> **专业人士善用自己的能力，写出别人能理解的代码。**
> 
> ―罗伯特·马丁

反应太棒了！在过去的几年里，随着许多库和框架的出现，JavaScript 的使用大量增加。这使得开发和代码维护工作变得非常容易。使用 JavaScript 可以做很多事情。但是随着代码库的增长，它变得非常难以维护。那么，让这个过程不那么痛苦的理想解决方案是什么呢？

![](img/098bf6ef3129d054025d49e2fe994618.png)

Photo by [Aarón Blanco Tejedor](https://unsplash.com/@healing_photographer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 以打字打的文件

是的。你没听错！无论团队成员的数量和项目规模如何，严格键入的代码通常都非常便于维护。我记得当我不得不开发一个由初学者用 JavaScript 开发的移动应用程序时的挣扎。我的 IDE 上绝对没有错误指示或建议，我不得不花几天时间记录和添加断点来解决一些小问题。

当您启动项目时，只使用 var/let/const 听起来可能很容易。但是，当你想编辑几个月前开发的应用程序的某些部分时，这可能会变得非常痛苦。

![](img/02dd794048f88134054764890c5b1379.png)

# 优势

*   **严格键入的**代码总是帮助您在键入时**捕捉错误**。相信我。从长远来看，这会节省很多时间！
*   **写 JSX 标签时的明智建议—** 在运行时遇到问题时，是否仅仅意识到错过了一个强制性的道具？不再是了。
    如果您错过任何必修道具，将立即受到警告。除此之外，未知道具的值会自动提示给你。
*   **描述性—** 类型脚本非常容易记录我们的定制组件，因为我们为每个组件创建了额外的道具文件，其中列出了所有道具及其描述。
*   **简化语法—** 大部分时间花在重复的代码上，我们没有意识到。

例如:考虑一种您想要从 API 响应中检索嵌套属性的情况。但是您不确定它是否存在吗？

```
const response = await getUser('cbc40f1f1d1c44944e9d3047b61cdb9e')if (
  response
  && response.data
  && response.data.company
  && response.data.company.role
) {
  const userRole = response.data.company.role;
}
```

有了 TypeScript，这变得非常容易。

```
const response = await getUser('cbc40f1f1d1c44944e9d3047b61cdb9e')
const userRole = response?.data?.company?.role;
```

该语法被称为[可选链接](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html)，在链接任何属性之前添加`?`，以便在检索子属性之前检查其存在性。

功能也是如此。通常，在某些情况下，您可能会将一个函数作为可选的道具传递。但是在子组件中，您不确定它是否存在。这就是在调用 TypeScript 之前对其进行存在性检查的方式。

```
<TextInput onChangeText={(value) => **onChange?.(value)**} />
```

这些只是我可以在本文中包括的少数例子。但是使用 TypeScript 还有很多好处，我想在另一篇文章中列出来。

# 警告

*   **学习曲线—** 作为开发人员，我们经常很忙，更新知识的时间有限。为了维护一个干净的 TypeScript 项目，您可能需要理解几个概念。
*   **最初增加了开发时间—** TypeScript 要求你为你编写的每个变量添加类型。因此，您可能需要花费比平常 JavaScript 开发更多的时间。
*   **更多的编译时间—** 因为你的代码需要在输入时编译，以便及时发现错误，这可能会占用额外的时间。此外，您的代码需要转换成 JavaScript。

# 如何创建 TypeScript 项目？

在 react-native CLI 的帮助下，创建 TypeScript 项目相当容易。

```
npx react-native init MyApp --template react-native-template-typescript
```

您也可以将现有的 JavaScript 项目转换为 TypeScript。我们不会在本文中这样做。但是你可以在官方网站上找到更多的信息。

# 结论

我知道，如果你像我一样已经是一名 JavaScript 开发人员，那么很难进入 TypeScript。最初花在学习 TypeScript 上的时间会让你走很长的路，并且随着项目越来越大，肯定会减轻你的工作压力。

现在我们已经到了这篇文章的结尾，我想让你知道这是我的第一篇关于媒体的文章。我想把我作为软件工程师的更多经验写进像这篇文章这样有用的文章中。
如果您喜欢您所阅读的内容，请随意使用鼓掌按钮或发表评论。这将有助于激励我写更多这样的文章。谢谢！快乐编码。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)