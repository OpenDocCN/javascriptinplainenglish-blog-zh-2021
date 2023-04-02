# 在你的文档、博客和营销网站上使用 Docusaurus 的 10 个理由

> 原文：<https://javascript.plainenglish.io/10-reasons-to-use-docusaurus-for-your-docs-blog-marketing-site-48dbf2c58b70?source=collection_archive---------10----------------------->

![](img/5f75b02fcc0ada62d8d7ae099215c23f.png)

Photo by [Mehmet Turgut Kirkgoz](https://unsplash.com/@tkirkgoz?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

最近，我一直在从事一个名为 [sapling.dev](https://sapling.dev/) 的项目，该项目生成全栈 JavaScript (node + React)应用，包括完整的 CRUD APIs、Auth0 和 Stripe 集成等等。Sapling 是我开发的第一个开发工具，我很快意识到，在我们开始营销时，以下几项非常重要:

*   **顶级文档** —我们的文档需要描述用户如何生成新的代码库，如何构建新的前端和后端，如何启动和运行(npm 脚本、nvm 版本、dockerized 数据库等)。)，以及如何配置 Auth0 和 Stripe 等集成服务
*   一个不错的博客部分——Sapling 旨在帮助开发人员快速构建并遵循最佳实践，因此我们肯定希望继续添加帖子，作为在生成的代码库中做出选择的教程
*   **一般营销内容** —像其他任何东西一样，我们需要一些任意的页面，如主页、定价页面等。

我们不想重新发明轮子——我们在设计文档或博客方面的任何尝试都远远达不到我最近花时间浏览的网站，如 [React Native Docs](https://reactnative.dev/docs/getting-started) 或 [Auth0 Docs](https://auth0.com/docs/) 。

我们知道主要用 Markdown 编写是最理想的，然后我们学习了 [MDX](https://mdxjs.com/) ，它让我们可以向 Markdown 添加 React 组件。通过更多的研究，在尝试了几个备选方案后(见本文末尾)，我们偶然发现了[**Docusaurus**](https://v2.docusaurus.io/)**。**

# Docusaurus 是什么？

Docusaurus 是脸书的一个开源项目，它使得建立一个专注于内容的网站变得非常容易，比如文档、博客等等。开箱即用，您会得到一个主页、一个包含一些示例文章的博客和一个包含一些示例文档的文档部分。

*注意:当我创建我的 Docusaurus 项目时，我使用了* `*classic*` *模板，即* `*@docusaurus/preset-classic*` *…有几个选项，但这给了你我上面提到的主要部分，并在下面深入讨论。*

Docusaurus 依靠特定的结构和配置来简化内容的添加和组织。我将在下面详细介绍，但是很多配置都在根文件`docusaurus.config.js`中。对于特定于 Docusaurus 的 React / Markdown *内容*生成用例，我发现它非常快速和简单。

对于我们的 Sapling 项目，我们将静态 Docusaurus 站点和核心应用程序分开。我们的 [Docusaurus 站点](https://sapling.dev/)托管在根域 [sapling.dev](https://sapling.dev/) 上，这保证了我们的主页和内容超级快(静态，使用 s3 bucket + Cloudfront)，然后我们在 [app.sapling.dev](https://app.sapling.dev/) 上托管一个 Create React App 应用程序(用户在那里配置和生成代码库)。

# 使用 Docusaurus 的 10 个理由

排名不分先后，以下是我喜欢 Docusaurus 的 10 点:

1.  **静态站点生成(SSG)**

当您在 Docusaurus 项目中运行一个`build`命令时，它将构建静态 HTML 页面，准备好提供给浏览器。由于静态页面不会改变(例如，你的博客文章对每个浏览它的人来说看起来都是一样的)，它们非常适合缓存在像 AWS Cloudfront 或类似服务这样的 CDN 中。加载静态 Docusaurus 站点的页面会非常快。

**2。MDX 准备就绪**

如上所述，MDX 因能够呈现 React 组件而降价。这些是`.mdx`文件而不是普通的`.md`。

对于任何博客帖子、文档页面或 Docusaurus 中的任意页面(很快会有更多相关内容)，由于 Markdown，您可以轻松地编写内容，并在需要的地方添加一些 React 组件。这种灵活性被证明对我们的网站非常有用——例如，[树苗定价页面](https://sapling.dev/pricing/)是一个`.mdx`文件。它对文本和 React 组件使用了一些 markdown，在 React + Material-UI 中显示了定价选项。

**3。文档部分**

Docs 是 Docusaurus 的核心能力之一。只需很少的工作，你就可以拥有像我们为 sapphire 制作的好看的文档[。](https://sapling.dev/docs/)

你需要做的就是遵循这两个步骤:

a.在`docs`文件夹中添加一个`.md`或`.mdx`文件

b.在`sidebars.js`文件中，您将新的降价文件的`id`(稍后将详细介绍)添加到在`sidebars.js`中定义的类别之一。

让我们看看它是如何工作的…

考虑在`docs`文件夹中添加一个名为`overview.md`的新文件。您可以像这样在文件顶部添加特殊信息(顶部的元数据不会显示在页面本身上):

```
---
id: overview
title: Overview
sidebar_label: Overview
slug: /overview
---## Welcome to my Project
This is Markdown in a docs page...
```

可以将名为`overview`的`id`属性添加到`sidebars.js`文件中，从那里开始，您的`/docs`页面将在左侧栏中显示新页面，并且可以在`/docs/overview`查看该页面。

我最喜欢的一个功能是在每个文档的右边有一个大纲，它根据你使用的嵌套的 Markdown 标题创建了到文档不同主要部分的链接。

Docusaurus 还在每个文档页面的末尾创建了“下一页”和“上一页”的 UI 链接，这样用户就可以很容易地在文档中前进或后退。

*注意，如果这是你的唯一目标，你可以让你的网站“仅限文档”——查看官方文档* *。*

**4。博客版块**

与 Docs 类似，博客是 Docusaurus 的另一大核心竞争力。我们的树苗博客看起来做得很好，没有任何定制工作。

就像 Docs 一样，您将`.md`或`.mdx`文件放入`blog`文件夹。您可以像这样添加元数据(有关选项的完整列表，请参见文档):

```
---
slug: introducing-sapling
title: Introducing Sapling
author: Nate Jones
author_title: Co-Creator, Sapling
author_url: [https://github.com/<](https://github.com/neightjones)my-github>
author_image_url: [<](https://nobbos-web-img.s3.amazonaws.com/nate.png)my-image-url>
---## Full Stack JS
The blog post markdown content...
```

标题会出现在你博客的左边栏，url `/introducing-sapling`会转到你的新帖。

文件名本身应编码官方文件中提到的日期[。](https://v2.docusaurus.io/docs/blog#adding-posts)

默认情况下，当您访问`/blog/`路径(没有特定的博客链接)时，您会在一个大页面上看到所有博客文章的列表。这可能会变得很长，定制并使其看起来更好的一种方法是在你的 Markdown 中使用特殊的`<!--truncate-->`语法——在用户实际点击之前，只有`<!--truncate-->`以上的内容才会显示在“预览”视图中。

还有一种“只写博客”的模式。

**5。精心设计的主页生成**

你的 Docusaurus 网站的索引页面看起来会和 T21 页面非常相似。该页面考虑了来自您的`docusaurus.config.js`的一些配置，包括项目名称、描述等等。

这是任意页面的第一个例子(见列表中的下一点)，但恰好是为您创建的。接下来您将看到，这个页面在`src/pages/index.js`的文件位置在路由时有特殊的含义。对于 Sapling，我们用自己的定制页面替换了生成的主页。

6。带自动路由的任意页面

如果你想知道“除了文档或博客之外，我可以添加任何我想要的随机页面吗？”答案是肯定的！

基于文件名处理路由。如果你想在你的站点上有一个位于`/faq`路线的页面，只需在`src/pages/`下添加一个名为`faq.js`(或者`faq.md` / `faq.mdx`)的文件，就可以了。

如上所述，我们的[定价页面](https://sapling.dev/pricing/)是一个`.mdx`文件——因为 url 是`/pricing`，这意味着我们有一个名为`src/pages/pricing.mdx`的文件，其中包含一些 Markdown 和 React 代码。事实上，`.mdx`文件非常适合任意页面，因为 Docusaurus 知道保持这些页面的页眉和页脚不变。

见下面的页眉和页脚配置信息，但最终我们添加了一些页眉配置，以确保我们有一个链接到我们的定价页面。

**7。主题&自定义 CSS**

默认的`docusaurus.config.js`链接到一个名为`src/css/custom.css`的文件——这个文件向你展示了如何创建一些全局 CSS 来应用到整个站点。

我们做的一个直接的改变是更新默认的颜色— [查看关于这个的文档，这里是](https://v2.docusaurus.io/docs/styling-layout#styling-your-site-with-infima)。

除了全局样式之外，您仍然可以按照预期为不同的 React 组件创建单独的 CSS 文件。我们的站点在主页上使用了与 React 组件更接近的`.scss`文件。

**8。页眉&页脚配置**

标题中的导航栏可以自定义链接等等。您可以自定义您的徽标，在“文档”和“博客”之外的自定义页面上添加链接，并根据需要定位。我们移除了开箱即用的黑暗模式切换，因为它不太适合我们的主题(在 Docusaurus 配置中，我们将`themeConfig->colorMode->disableSwitch`切换到了`true`)。

类似地，页脚设置了一些到各种文档的链接、一些联系人和社交信息，以及一个“更多”部分。为了方便使用，我定制了页脚的文档部分，以指向我们网站文档中的主要类别。

**9。插件生态系统**

Docusaurus 可以通过插件系统进行扩展。我们最初使用的几个插件是`docusaurus-plugin-sass`风格的`.scss`文件，以及一个内置的谷歌分析插件。

同样，你可能习惯于在 HTML `head`中添加某些脚本或 CSS 文件(例如，在 Create React App 中，你可以访问一个`public/index.html`文件)。虽然这里没有这个文件，但是 Docusaurus 允许您使用这个导入:

```
import Head from '[@docusaurus/Head](http://twitter.com/docusaurus/Head)';
```

在`Head` React 组件中，您可以添加如下脚本，这是我们用来在 Sapling 上添加实时聊天弹出窗口的脚本(这是通过我们的 HubSpot 帐户):

```
<Head>
  {/* <!-- Start of HubSpot Embed Code --> */}
  <script
    type="text/javascript"
    id="hs-script-loader"
    async
    defer
    src="//js.hs-scripts.com/<some-id-number>.js"
  ></script>
  {/* <!-- End of HubSpot Embed Code --> */}
</Head>
```

我们在 Docusaurus 的`src/pages/index.js`文件中使用这个`Head`组件。

**10。非常适合开源项目**

在您的`docusaurus.config.js`文件中，您将看到与您项目的 GitHub url 相关的各种配置。因为 Sapling 不是 OSS，我们删除了一些信息。当您链接到 GitHub 时，您将拥有现成的功能，用户可以编辑博客帖子或文档页面，这将与您的 GitHub repo 绑定在一起。

许多像 [React Native](https://reactnative.dev/) 和 [Flux](https://facebook.github.io/flux/) 这样的大项目都使用 Docusaurus，所以它是构建 OSS 项目内容的理想方式。

# 可供选择的事物

有可靠的开源和付费选项来建立文档和/或博客和/或其他内容。以下是几个例子:

*   Gatsby 是一个非常流行的框架/工具，用来构建快速、静态生成的网站。[这里有一个在盖茨比中使用 MDX 的插件](https://www.gatsbyjs.com/plugins/gatsby-plugin-mdx/)
*   GitBook 是一个免费增值的选项，专注于创建真正好的文档
*   其他 SSG 工具如 [Next.js](https://nextjs.org/) 也非常灵活

这些都是很好的选择，但是由于我们的明确目标是为营销、文档和博客创建一个静态的站点，具有开箱即用的优秀文档/博客设计，我发现 Docusaurus 是迄今为止最容易上手的方法，几乎没有学习曲线。