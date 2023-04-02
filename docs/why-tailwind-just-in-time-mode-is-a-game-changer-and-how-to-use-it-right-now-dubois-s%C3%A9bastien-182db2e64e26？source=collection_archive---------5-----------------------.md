# 顺风的及时模式是一个游戏改变者

> 原文：<https://javascript.plainenglish.io/why-tailwind-just-in-time-mode-is-a-game-changer-and-how-to-use-it-right-now-dubois-s%C3%A9bastien-182db2e64e26?source=collection_archive---------5----------------------->

## 以及现在如何使用它

了解如何将您的应用程序迁移到 [Tailwind](https://tailwindcss.com/) 2.1+，以及如何启用 Tailwind 的[即时](https://github.com/tailwindlabs/tailwindcss-jit)模式。

**更新 2021–04–06**:适应了顺风 v2.1 发布后的内容

![](img/87f5494eea0eed9170cf68c0d089ba83.png)

大约两周前，亚当·瓦森[宣布了一项新的顺风实验](https://blog.tailwindcss.com/just-in-time-the-next-generation-of-tailwind-css) : [准时](https://github.com/tailwindlabs/tailwindcss-jit)。从那时起，Tailwind 2.1 [已经发布](https://github.com/tailwindlabs/tailwindcss/releases/tag/v2.1.0)，它引入了对这一新特性的官方支持。

在这篇文章中，我将告诉你这是怎么回事，以及你如何利用它。

**警告**:此时顺风的准时制模式还在预览中。我用它来生产我的产品，到目前为止还没有任何问题，但是你永远不知道。

# 什么是顺风的即时模式，为什么要关注？

自从开始用[顺风](https://tailwindcss.com/)之后，就再也没有回头。感觉比老式的 CSS 更有效率。想要一些空白，一些左边的填充，和圆角？给你:`m-2 px-2 rounded-lg`。能够非常简洁地快速表达复杂的 CSS 规则是 Tailwind 的关键优势之一。

有些人误解了这一点，认为他们必须用大量的顺风指令来填充 HTML 模板，但这只是一种方法；你也可以使用标准的 CSS 类，并在其上应用顺风规则，以一种更经典的方式工作。虽然，这篇文章的目标不是说服你使用 Tailwind 我认为有足够多的文章涉及这一点。在这里，我将把重点放在什么是准时制模式，以及它为什么有趣。

顺风的一个主要缺点是它会产生*兆字节*的 CSS 代码。原子 CSS 类是为项目中的每一个规则和变体生成的。例如，Tailwind 包含宽度为的[实用程序类。正如您在文档中看到的，默认情况下，它包括以下值:`w-0 w-0.5 w-1 w-1.5 w-2 w-2.5 w-3 w-3.5 w-4 w-5 w-6 w-7 w-8 w-9 w-10 w-11 w-12 w-14 w-16 w-18 w-20 w-24 w-28 w-32 w-36 w-40 w-44 w-48 w-52 w-56 w-64 w-1/2 w-1/3`，以及更多。此外，您可以使用`tailwind.config.js`配置文件定制这些。最小宽度、最大宽度、高度、字体、颜色等等也是如此！](https://tailwindcss.com/docs/width)

很多规则也可以组合。例如，您可以使用`text-red-500`来获得生动的红色文本，或者使用`bg-red-500`来改变背景的颜色。为了支持这一点，Tailwind 为每一种可能的规则组合(例如，边框颜色、背景颜色、悬停、焦点等)生成 CSS 类。

可以想象，生成的 CSS 代码非常庞大，随着添加更多的颜色、变体等，情况会成倍恶化。这导致了*巨大的*束尺寸。幸运的是，Tailwind 包含了对 PurgeCSS 的内置支持，允许我们去掉所有未使用的类。

PurgeCSS 非常适合生产构建，因为它去除了所有未使用的实用程序类，从而产生了最佳的 CSS 包。不幸的是，在开发过程中，使用它并不是一个真正的选择；只是太花时间了。结果是，随着顺风生成的 CSS 包变得越来越大，应用程序的构建速度越来越慢，Web 浏览器开发工具也因为要接收的 CSS 数量而变得缓慢。这当然是开发者体验的一个主要问题。大型团队的税收是巨大的。每次您更改全局样式时，顺风“编译器”都需要重新生成整个样式。

这就是准时制(JIT)模式发挥作用的地方。在启用了 Tailwind 的 JIT 模式的情况下，Tailwind 编译器只会为您真正利用的 Tailwind 规则生成 CSS 代码。这真是太棒了！

为什么？因为这意味着所有的肿胀都消失了！启用 JIT 后，我们只得到真正需要的 CSS 类。正因为如此，CSS 代码的生成速度更快，从而大大缩短了启动时间。此外，由于 CSS 更少，浏览器开发工具的响应速度更快。作为一个额外的好处，CSS 在开发和生产之间是一样的。光是这些好处就足以激励我启用 JIT。但还有更多！

以前，许多 [Tailwind 变体](https://tailwindcss.com/docs/configuring-variants)在默认情况下被禁用，因为它们会导致生成数兆字节的 CSS(例如，暗模式、负责、悬停、可见焦点、活动、禁用等)。因为 JIT“按需”生成样式，这意味着所有这些变体都可以直接使用，无需配置。

JIT 模式也带来了新的有趣的特性。其中之一是将多个规则堆叠在一起的可能性。例如，让我们在元素激活时将字体加粗，并停留在中间断点:`sm:focus:hover:active:font-bold`。以前，像这样的堆叠规则是不可能的。这打开了一个充满新可能性的世界。

JIT 带来的另一个很酷的特性是可以在不改变设计系统配置的情况下，为某些规则使用自定义值。以前，唯一的方法是要么求助于标准 CSS，要么定制 Tailwind 的配置，这会导致更多的 CSS 膨胀。例如，添加一种颜色意味着因为所有的组合而添加大量的 CSS。现在，如果某个地方有您需要的颜色，您可以执行以下操作:`bg-[#a0cdae]`。太棒了。

不用说，这是 Tailwind 向前迈出的巨大一步:更少的配置，更多的功能，更好的性能。这是各方面的胜利！

虽然[有一些限制](https://github.com/tailwindlabs/tailwindcss-jit#known-limitations)，但没什么太烦人的。

如果您想了解更多信息，请观看简介视频:

现在让我们看看如何启用 JIT！

# 启用 Tailwind 的 JIT 模式

在这里，我假设您已经在项目中使用了 Tailwind 和 PostCSS。

首先，您需要升级到 Tailwind 2.1，这是第一个包含 JIT 模式的版本。此外，确保将`autoprefixer`更新为最新版本！

完成后，修改您的 Tailwind 配置(即`tailwind.config.js`)以启用 JIT 模式:

```
module.exports = {
  mode: 'jit',
  ...
}
```

此时，确保`purge`选项已启用并正确配置。它应该包括所有包含 Tailwind“规则”的文件。以下是我在基于 [Nrwl NX](https://nx.dev/) 的 Angular 应用程序中使用的配置:

```
// Help Tailwind configure PurgeCSS correctly
// Reference: https://tailwindcss.com/docs/controlling-file-size/#app
purge: {
  content: [
    "./apps/**/*.html",
    "./apps/**/*.ts",
    "./apps/**/*.scss",
    "./libs/**/*.html",
    "./libs/**/*.ts",
    "./libs/**/*.scss",
  ],
  // PurgeCSS options
  // Reference: https://purgecss.com/
  options: {
    rejected: true,
    printRejected: true,
  },
},
```

就这样！是的，真的！这有多酷？；-)

# 调整现有代码

下一步是调整您现有的代码。在这里，我将强调我必须在我的项目中做出的一些改变。不过，请注意，其中一些可能与 Tailwind 2 有关，而不是 JIT，因为我的项目以前仍然使用 Tailwind 1.x。对于每种情况，我将向您展示迁移前后的代码。

## 不再可能在`@screen`中嵌套`@apply ...`

之前:

```
.create-page-body {
  @apply mt-4 flex flex-wrap gap-8 justify-between;

  @screen md {
    @apply mt-10;
  }

  @screen lg {
    @apply justify-around;
  }
}
```

之后:

```
.create-page-body {
  @apply mt-4 flex flex-wrap gap-8 justify-between md:mt-10 lg:justify-around;
}
```

正如你在上面看到的，由于`@screen`规则，代码变得不那么杂乱，感觉也更轻松了。当然有利也有弊。也许以后会再次支持旧的语法，我不确定。

## 再也没有`!important`规则了

之前:

```
.create-page-user-autocomplete-input-box {
  @apply border-gray-400 !important;
}
```

之后:

```
.create-page-user-autocomplete-input-box {
  @apply !border-gray-400;
}
```

这些规则现在可以以`!`为前缀来执行，以覆盖 CSS 级联。

**警告**:打破 CSS 级联是邪恶的，我知道。但有些情况下是必要的。

## 就是这样！

信不信由你，但这些几乎是我在启用 JIT 的情况下让我的项目在 Tailwind 2.1 下工作所必须做的唯一改变。精彩！

# 在故事书中启用 JIT

如果你在你的项目中使用 [Storybook](https://storybook.js.org/) ，那么你可能也想在那里启用 JIT。目前这样做需要更多的工作，因为 Tailwind 的 JIT 模式只支持 PostCSS 8+。幸运的是，最近[故事书 6.2](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#deprecated-implicit-postcss-loader) 引入了对 PostCSS 8 的支持。

**提示**:故事书 6.2 包含了对 Angular 的重大改进。稍后我可能会写一篇关于这个的文章:[https://github . com/storybook js/storybook/blob/next/migration . MD # 62-angular-overhaul](https://github.com/storybookjs/storybook/blob/next/MIGRATION.md#62-angular-overhaul)

假设您已经升级到 Storybook 6.2+，下面是如何启用 JIT。

首先，您需要安装新的 [PostCSS 附加组件](https://github.com/storybookjs/addon-postcss):

```
npm install -D @storybook/addon-postcss
```

你可以在这里找到它的文档。安装后，您需要修改 Storybook 的`main.js`配置文件才能启用它:

```
{
  name: "@storybook/addon-postcss",
  options: {
    /**
     * Make sure to use the expected PostCSS version
     */
    postcssLoaderOptions: {
      implementation: require("postcss"),
    },
  },
},
```

这个新的 Storybook 插件的好处是，它使 Storybook 和应用程序的其余部分保持一致变得轻而易举，并且在任何地方都使用相同的 PostCSS 版本。

当然，你也需要修改 Storybook 的 Webpack 配置来加载 Tailwind。如果你不知道如何给故事书添加顺风，那么看看我之前的文章。

# 将来的

Tailwind 的 JIT 模式是刚出炉的，但工作起来很有魅力。JIT 很可能会成为顺风 3 的默认模式。我确信它将会*严重*影响顺风的未来发展(更好！).

# 结论

在本文中，我解释了为什么 Tailwind 新的即时模式是一个游戏规则改变者，以及如何启用它。

总之，我的建议是现在就试一试*。它非常有效，并且带来了重要的好处。仅仅是性能提升就值得付出这么一点点努力！*

*今天到此为止！*

*PS:如果你想学习大量关于产品/软件/Web 开发的其他很酷的东西，那么[看看开发概念系列](https://dev-concepts.dev)，[订阅我的时事通讯](https://mailchi.mp/fb661753d54a/developassion-newsletter)，还有[来 Twitter 上打个招呼吧！](https://twitter.com/dSebastien)*

**原载于 2021 年 4 月 3 日 https://dsebastien.net*[](https://dsebastien.net/blog/2021-04-03-migrating-angular-to-tailwind-2-and-jit)**。***