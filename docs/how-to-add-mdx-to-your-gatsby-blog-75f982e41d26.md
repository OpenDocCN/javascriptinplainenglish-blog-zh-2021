# 如何将 MDX 添加到您的盖茨比博客中

> 原文：<https://javascript.plainenglish.io/how-to-add-mdx-to-your-gatsby-blog-75f982e41d26?source=collection_archive---------24----------------------->

在你的盖茨比博客中了解如何使用 MDX 而不是 Markdown

![](img/ebfd756098792df0be62fd01a9622dd0.png)

Photo Illustration by David Fekke

*原发布于*[*https://fek . io*](https://fek.io/blog/adding-mdx-to-your-gatsby-blog/)*。*

[MDX](https://github.com/mdx-js/mdx) 是 [Markdown](https://www.markdownguide.org/) 语法和 [React](https://reactjs.org/) JSX 语法的混合体。在 Markdown 中写文章的作者可以在文章中使用 React 组件。

目前 Markdown 允许作者在文章中添加 HTML 标签。React 的一个优点是，它使我们能够创建 HTML 元素组合的组件，然后在 React 应用程序中重用这些元素。MDX 允许我们在降价帖子中使用这些相同的组件。

```
import { Link } from 'gatsby'

import Layout from '../components/layout'
import Image from '../components/image'
import SEO from '../components/seo'

<SEO title="Home" keywords={['gatsby', 'application', 'react']} />

# Hi people

Welcome to your new Gatsby site.

Now go build something great.

<div style={{ maxWidth: '300px', marginBottom: '1.45rem' }}>
  <Image />
</div>
<Link to="/page-2/">Go to page 2</Link>
```

# 向您的博客添加 MDX

目前我在我的博客上使用常规降价。我决定我想看看将 MDX 添加到我的博客会涉及到什么。在我当前的 Gatsby 站点实现中，我使用了`gatsby-transformer-remark`插件将 markdown 转换成 Gatsby 数据，这些数据可以用来呈现我的博客文章。

Gatsby 提供了一个很好的教程，介绍如何使用 starter site 获取一个现有的 Gatsby 博客，并将其转换为使用 MDX 而不是 markdown。

[](https://www.gatsbyjs.com/blog/2019-11-21-how-to-convert-an-existing-gatsby-blog-to-use-mdx/) [## 如何将现有的 Gatsby 博客转换为使用 MDX

### mdx 是一种文件格式，允许您通过. MDX 文件将 JSX 添加到 Markdown 文件中！它由…创建并维护

www.gatsbyjs.com](https://www.gatsbyjs.com/blog/2019-11-21-how-to-convert-an-existing-gatsby-blog-to-use-mdx/) 

这个帖子是 2019 年的，有些行号不符合，但它仍然可以作为一个转换你的博客使用 MDX 的基础。

w 将使用`Gatsby Starter Blog`作为我们转换的基础。您可以使用下面的 Gatsby 命令安装它；

```
> gatsby new gatsby-blog [https://github.com/gatsbyjs/gatsby-starter-blog](https://github.com/gatsbyjs/gatsby-starter-blog)
```

在修改代码之前，您需要将 mdx 插件添加到 gatsby 站点。下面是添加 MDX 插件的 NPM 命令。

```
> npm install --save gatsby-plugin-mdx gatsby-plugin-feed-mdx @mdx-js/mdx @mdx-js/react
```

在您的`gatsby-config.json`文件中，我们将用`gatsby-plugin-mdx`配置设置替换`gatsby-transformer-remark`配置。在选项下，您需要为`extensions`添加属性，并将`plugins`属性的名称改为`gatsbyRemarkPlugins`。最终的配置应该如下例所示。

然后用`gatsby-plugin-feed-mdx`替换配置中的`gatsby-plugin-feed`插件。完成配置更改后，您可以移除旧的 NPM 模块。

```
> npm uninstall --save gatsby-transformer-remark gatsby-plugin-feed
```

# 更改节点 API

我们需要对`gatsby-node.js`文件做一些修改。我们需要将所有提到`allMarkdownRemark`的地方替换为`allMdx`。我们还需要将所有使用`MarkdownRemark`的引用类型改为使用`Mdx`。

# 将任何页面引用更改为 Markdown

既然我们已经将节点 API 更改为使用 Mdx，那么我们可以专注于将仍然引用`MarkdownRemark`的任何页面或模板更改为使用`Mdx`。在`index.js`页面中，我们用 Mdx 替换了所有的降价参考。

现在我们可以对`src/templates/blog-post.js`模板进行这些更改，但是这次引用将分别是`markdownRemark`和`mdx`。

将`markdownRemark`改为`mdx`后，在 GraphQL 查询中用`body`替换`html`。

现在让我们添加一篇 MDX 博客文章。我们将把这个文件命名为`example.mdx`,并把它和我们的其他帖子放在`blog`目录中。

```
**// example.mdx
---**
title: MDX Example
date: "2021-07-03T22:12:03.284Z"
**description: "MDX Example"
---**

**# My first MDX post**

This is a post showing MDX in action.

MDX lets you write JSX embedded inside markdown, perfect for technical blogs.
```

现在让我们创建一个组件来添加 Youtube 视频到我们的 MDX 文章。

现在我们可以将这个组件添加到我们的 MDX 帖子中。

```
**// example.mdx
---**
title: MDX Example
date: "2021-07-03T22:12:03.284Z"
**description: "MDX Example"
---**
import Youtube from "../../../src/components/yt.js"

**# My first MDX post**

This is a post showing MDX in action.

<Youtube yid="jYVM6KOWYBs" />

**## MDX**

MDX lets you write JSX embedded inside markdown, perfect for technical blogs.
```

# 结论

通过对我们的 Gatsby 博客进行一些简单的修改，我们现在可以对我们的博客文章使用基于 MDX 的 React 组件。现在，我们可以开始使用自己的组件，混合在我们简化的基于降价的标记中。现在，我们只需要一个 React 元素就可以为我们的帖子添加视频和音频。

*更多内容看* [***说白了***](http://plainenglish.io/)