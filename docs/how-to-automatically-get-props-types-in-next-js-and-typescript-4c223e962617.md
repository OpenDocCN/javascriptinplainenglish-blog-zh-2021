# 如何在 Next.js 和 TypeScript 中自动获取道具类型

> 原文：<https://javascript.plainenglish.io/how-to-automatically-get-props-types-in-next-js-and-typescript-4c223e962617?source=collection_archive---------1----------------------->

## 避免使用带有 InferGetServerSidePropsType 和 InferGetStaticPropsType 的样板代码

![](img/6faa53226253f8d58f655486aecc90e9.png)

Photo by [AltumCode](https://unsplash.com/@altumcode?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

这里提到的[，Next.js 官方支持 TypeScript。随着时间的推移，已经添加了一些功能来避免编写样板代码。其中最有用的由`InferGetServerSidePropsType`和`InferGetStaticPropsType`表示。](https://nextjs.org/docs/basic-features/typescript)

这些将自动推断出分别来自`[getServerSideProps()](https://nextjs.org/docs/basic-features/data-fetching#when-should-i-use-getserversideprops)`或`[getStaticProps()](https://nextjs.org/docs/basic-features/data-fetching#when-should-i-use-getstaticprops)`函数的页面组件道具的类型。尽管它们无疑代表了一个节省时间的特性，`InferGetServerSidePropsType`和`InferGetStaticPropsType`有一些限制，阻止它们正确推断道具类型，导致`props: never`错误。

现在让我们看看如何使用`InferGetServerSidePropsType` `InferGetStaticPropsType`并避免这些限制。

# InferGetServerSidePropsType 和 InferGetStaticPropsType 在运行

让我们通过一个例子来看看`InferGetServerSidePropsType`是如何工作的:

如您所见，`InferGetServerSidePropsType`允许您避免将`UserPage`组件`user` prop 声明为`User`。如果没有`InferGetServerSidePropsType`，用户页面函数签名将是这样的:

最后一种方法显然涉及到代码重复、样板代码，并且使整个代码库不太容易维护。

记住`InferGetServerSidePropsType`与`getServerSideProps()`一起工作。同样，`InferGetStaticPropsType`与`getStaticProps()`一起工作。它们的用途和功能实际上是相同的。因此，不需要显示`InferGetStaticPropsType`运行的例子。

# 使用 infer-next-props-type 解决了类型推断问题

[类型推理](https://en.wikipedia.org/wiki/Type_inference)很棒，在某些情况下甚至像魔术一样。另一方面，它涉及可能容易失败的复杂程序。在撰写时，在 Next.js ≤ 12 中，`InferGetServerSidePropsType`和`InferGetStaticPropsType`都有几个重大问题导致 Next.js 推断`never`为道具类型。如果你想了解更多，请点击这个链接。

这些限制可能会成为一个问题，并阻止您完全使用它们。考虑到使用`notFound`时推断过程也会失败，这一点尤其正确。正如官方文档中的[所述，`notFound`是一个可选的布尔值，它将强制 Next.js 重定向到 404 页面。下面是它如何工作的一个例子:](https://nextjs.org/docs/basic-features/data-fetching)

在这种情况下，当数据检索逻辑失败时，`notFound`布尔值被返回，结果 404 页被加载。

每当使用该逻辑时，`InferGetServerSidePropsType`和`InferGetStaticPropsType`失败并返回`never`作为道具类型。换句话说，这种基本和常见的错误处理逻辑使得`InferGetServerSidePropsType`和`InferGetStaticPropsType`不起作用，因此不可使用。

幸运的是， [HaNdTriX](https://github.com/HaNdTriX) GitHub 用户发布了一个关于[infer-next-props-type](https://www.npmjs.com/package/infer-next-props-type)NPM 类型脚本库的修复程序。如这里描述的，使用起来非常简单。您所要做的就是用下面的代码行导入它:

```
import InferNextPropsType from "infer-next-props-type"
```

并按如下方式使用它:

所以，你所要做的就是用`InferNextPropsType`替换`InferGetServerSidePropsType`或`InferGetStaticPropsType`。事实上，该库以相同的`InferNextPropsType`类型不加区分地支持`getServerSideProps()`和`getStaticProps()`。

阅读 [this](https://github.com/vercel/next.js/issues/15913#issuecomment-950330472) 找到该库处理的导致标准 Next.js 推断过程失败的所有案例的列表。

# 结论

在本文中，我们学习了如何在 Next.js 和 TypeScript 中正确使用类型推断。Next.js 提供了一些特性来避免样板代码，让您在使用 TypeScript、`InferGetServerSidePropsType`和`InferGetStaticPropsType`进行开发时更加轻松。这很好，但是它确实有一些严重的限制，阻止您使用这些特性。幸运的是，社区已经采取措施来解决最棘手的问题，而了解这方面的一切正是本文的目的。

感谢阅读！我希望这篇文章对你有所帮助。请随意留下任何问题、评论或建议。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****