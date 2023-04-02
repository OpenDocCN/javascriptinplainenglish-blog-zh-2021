# 如何用 TailwindCSS 制作动画

> 原文：<https://javascript.plainenglish.io/how-to-animate-with-tailwindcss-394842ae8b39?source=collection_archive---------5----------------------->

## *基于实用程序类的动画！*

![](img/e3a64ebd41a081f6f0083ac25370963b.png)

Photo by [Sigmund](https://unsplash.com/@sigmund?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/css?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 介绍

[TailwindCSS](https://tailwindcss.com/docs) 是一个前端框架，基于使用实用程序类来提供更大的灵活性和更简单的响应，而无需编写一行 CSS。

最近，Tailwind 背后的优秀团队发布了 Tailwind 2.0，它有一些非常惊人的功能，比如动画，甚至是黑暗模式。

如果您已经有了一些使用 Tailwind 的经验，那么编写这些新函数就和您想象的一样简单。而如果你没有任何经验，我建议你先看看这篇文章:

[](https://mbvissers.medium.com/tailwindcss-starter-guide-90815db8ecc1) [## TailwindCSS 入门指南

### TailwindCSS 会扼杀传统 CSS 吗？

mbvissers.medium.com](https://mbvissers.medium.com/tailwindcss-starter-guide-90815db8ecc1) 

但是在这篇文章中，我们仍然会从一些基础知识开始，只是比链接文章中的要少一些。

# 装置

顺风可以用多种形式安装。我将使用 [NextJS](https://nextjs.org/) 建立一个使用 React 制作网页的快速开发环境。您可以跟随或选择您自己的框架，只要安装了 TailwindCSS，您就可以跟随本文的其余部分。

在您可以工作的文件夹中打开命令行并安装 NextJS

```
npx create-next-app tailwindBlog --use-npm --example "https://github.com/vercel/next-learn-starter/tree/master/learn-starter"
```

进入新目录，运行`npm run dev`启动应用服务器，检查目前为止是否一切正常。

接下来，我们将剥离`index.js`页面并[安装 TailwindCSS](https://tailwindcss.com/docs/installation) 。

```
npm install tailwindcss@latest postcss@latest autoprefixer@latest
```

然后我们初始化顺风:`npx tailwindcss init -p`并更新我们的`index.js`。

我们将在`<main>`标签内进行编程。尝试运行此代码，以确认 TailwindCSS 已正确导入并且正在运行。

# 内置动画

TailwindCSS 附带了一些内置动画[在很多情况下都很有用。我们通过添加一些元素来看几个。](https://tailwindcss.com/docs/animation)

我们创建一个绿色圆圈形式的`div`，用`h-6 w-6`来设置高度和宽度。我们用`**animate-ping**`动画来做这个。官方文档展示了这个动画，在通知上使用红点来引起用户的注意。想象一个圆圈，上面有一个像 iOS 通知一样会跳动的数字，这很酷。

下一个是`**animate-spin**`。它会做你所期望的事情，无限旋转物体，在这个例子中是一个`div`。这对于加载动画非常有用，它会给用户一种速度的感觉。

还有一些像`**animate-bounce**`和`**animate-pulse**`这样的游戏，它们提供了加载骨骼的有用动画，或者弹出箭头指示你可以向下滚动。

要禁用一个动画，你可以使用 Tailwind 提供的`animate-none`类。如果较小的屏幕可能不使用动画或在动作完成后动态添加动画，这将非常有用。

## 前缀

动画有特殊的前缀。`motion-reduce`和`motion-safe`就是这些。但是您也可以使用现有的前缀来表示响应、悬停或聚焦。这对于按钮来说非常酷。

其中一些默认情况下没有启用，您必须在`tailwind.config.js`文件中启用它们。

更新此文件后，您可以使用更多的前缀来创建响应更快或更动态的网页。

# 自定义动画

但是你甚至可以在`tailwind.config.js`中使用 CSS 的动画语法创建自己的动画。让我们创建一个来展示这一点，因为它真的很强大，能够结合 Tailwinds easy 语法和定制自己喜欢的动画。

这个文件包含一个简单的使用单行 CSS 语法的`spin-slow`动画。但这还不是全部。使用 CSS 的更高级的动画使用`keyframes`语法。

将`keyframes`数据添加到该文件的`theme`对象中。之后，您可以在`animation`对象中使用它。然后当然在你的 JSX 或 HTML 文件中作为一个类。`animate-wiggle`在这种情况下。

我们知道，这是非常强大的。我们可以利用顺风的便利性和 CSS 动画的力量和性能来创建动画。

# 结论

我希望这篇文章对一些人有用。我在研究这个的时候学到了新的东西，所以我很高兴。

非常感谢你的阅读，祝你有美好的一天。