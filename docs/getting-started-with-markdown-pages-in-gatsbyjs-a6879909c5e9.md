# Gatsby.js 中的 Markdown 页面入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-markdown-pages-in-gatsbyjs-a6879909c5e9?source=collection_archive---------5----------------------->

Mardown 是一个伟大而简单的方法来存储简单的丰富文本，如笔记、博客或产品描述，而 [GatsbyJS](https://www.gatsbyjs.com/) 可以轻松地在您的网页中使用它们，所以让我们来看看吧。

![](img/20200e302bf9a229e46241afe2de103e.png)

Photo by [Campaign Creators](https://unsplash.com/@campaign_creators?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/marketing?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

# 什么是降价？

正如我之前提到的， [Markdown](https://en.wikipedia.org/wiki/Markdown) 是一种快速创建富文本的简单方法，它包含许多组件，从粗体文本到代码块和超链接。

使文本加粗的基本语法通常是这样的:`**bold text**`。单个星号使文本倾斜，使用反斜线通常可以创建代码块。

最常用的功能可能是 Markdown 中的标题。快速编写从`h1`到`h5`的标题，有时甚至超过这是一个令人兴奋的特性。

```
# Header that is h1
## Header that is h2
### Header that is h3
...
```

虽然这对开发人员来说似乎没什么大不了的，但是想象一下，一家中小型公司想要创建 blogposts，但是他们的站点没有像 medium 那样的功能。开发人员会给文案撰写人员一份降价备忘单，他们会在几分钟内开始写作。

## 什么是 Gatsby.js？

盖茨比。js 是一个前端框架，用于快速编写服务器渲染的快速网页。我并不了解他们的一切，但我以前使用过这个框架，开发者的体验肯定是好的。

该框架在内部使用 GraphQL 来检索可以在服务器端呈现的数据，因此页面将始终显示正确的数据。

他们实际上有一家商场。

# 安装和设置

我们需要首先安装 Gatsby-CLI，然后我们将从 Gatsby 通过 Github 链接提供的“hello-world-starter”创建一个新项目。

```
npm install -g gatsby-cligatsby new hello-world [https://github.com/gatsbyjs/gatsby-starter-hello-world](https://github.com/gatsbyjs/gatsby-starter-hello-world)
```

进入新创建的文件夹，运行`gatsby develop`来运行项目。该项目的默认网址是`localhost:8000`。

关于盖茨比还有很多东西要学，但我将只关注降价页面，以创建一篇更有针对性的文章。

让我们安装一些 Gatsby 插件来让它们工作。

```
npm install gatsby-source-filesystem
npm install gatsby-transformer-remark
```

filesystem 插件用于处理非页面文件，transformer-remark 插件用于将 Markdown 转换成 Gatsby 可读的代码。

然后我们将编辑`gatsby-config.js`来包含这两个插件。

如果你运行这个，你会得到一个错误，指出一个目录不存在，这是正确的。在您的`src`目录中，像我们在配置中定义的那样，在`/src`中创建一个名为`markdown`的新文件夹。

# 创建降价页面

设置完成，是时候创建降价文件了。这个文件可以(很可能应该)包含盖茨比所说的' [frontmatter](https://www.gatsbyjs.com/docs/how-to/routing/adding-markdown-pages/#frontmatter-for-metadata-in-markdown-files) '。

Frontmatter 可以包含您不想让用户看到的`.md`文件的元数据，或者您可能想在用户看到它之前格式化它。

```
---
slug: "/blog/first-post"
date: "2021-01-28"
title: "My first page"
---
```

看起来是这样的。只需在 Markdown 文件顶部的三重破折号之间添加键值对。Gatsby 的 GraphQL API 可以检索这些数据供您使用。

我将在我的`markdown`文件夹中创建一个名为`first.md`的新降价文件。

你可以在这里找到它，因为 Github 创建了一个 frontmatter 所在的表。但它可以是任何带有上述内容的降价文件。*虽然我把我的 slug 设置为* `*/first*`这可能很重要。

这当然不会显示任何新的东西，因为我们还没有定义模板。这个模板是 React 代码，它将告诉 Gatsby 如何样式化我们的 Markdown 文件，并呈现 frontmatter 等细节。

# 创建模板

模板位于项目的`src/templates`目录中。其中的模板可以有任何名称。我选择了`template.js`，并添加了以下代码。

呈现一个简单的 React 组件。我们获取一些数据来得到我们的 frontmatter 和 html。我们`dangerouslySetInnerHTML`到我们的`div`，在这里将设置来自 Markdown 的 HTML。在它上面，我们设置标题和日期。

GraphQL 查询从我们的 Markdown 页面中检索数据。您可以通过转到`[localhost:8000/___graphql](http://localhost:8000/___graphql)`并在 GraphiQL 界面中输入查询来检查这一点。

我们只需要将`{ eq: $slug }`替换为我们在 frontmatter 中插入的实际 slug。`{ eq: “/first” }`像这样。您现在应该会看到一些熟悉的数据被返回给您。这就是 Gatsby 将使用该查询并使用`$slug`变量获得正确的减价页面来为您做的事情。

# 使用 CreatePage 创建静态页面

从 Markdown 创建静态页面需要使用 Gatsby 提供的`CreatePage` API。我们在项目的根目录下创建一个`gatsby-node.js`文件。我们从`src/templates/template.js`中定义模板，并设置 URL 来跟随 frontmatter 中的 slug。我的情况是`/first`。

该代码还使用 GraphQL 以降序检索所有 Markdown 文件。

如果你重新启动你的服务器，并转到你的 slug 的 URL，你会看到我们已经把 Markdown 文件渲染成 HTML 格式的(最小的)样式和所有的东西。

当然，您可以使用全局 CSS 来更新这些样式。

# 干得好的

用 Markdown 创建你的第一页做得很好。尝试使用 Markdown 文件添加更多的页面，这很容易，因为我们已经完成了所有的设置。

我希望这篇文章对你有用，祝你今天过得愉快。