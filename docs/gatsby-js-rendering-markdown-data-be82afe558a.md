# Gatsby.js 呈现降价数据

> 原文：<https://javascript.plainenglish.io/gatsby-js-rendering-markdown-data-be82afe558a?source=collection_archive---------11----------------------->

![](img/128290e7cef8866c35360303457659aa.png)

Photo by [Ben Hershey](https://unsplash.com/@benhershey?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Gatsby 是一个基于 React 的静态网站框架。

我们可以用它从外部数据源创建静态网站等等。

在本文中，我们将看看如何用 Gatsby 创建一个站点。

# 降价数据

我们可以从 Markdown 文件中获取数据，并将它们用作数据源。

为此，我们安装了`gatsby-transformer-remark`和`gatsby-source-fulesystem`插件来从给定的文件夹中获取降价文件。

我们通过运行安装`gatsby-transformer-remark`:

```
npm install gatsby-transformer-remark
```

我们通过运行来安装`gatsby-source-filesystem`:

```
npm install gatsby-source-filesystem
```

然后我们写道:

`gatsby-config.js`

```
/**
 * Configure your Gatsby site with this file.
 *
 * See: https://www.gatsbyjs.com/docs/gatsby-config/
 */module.exports = {
  /* Your site config here */
  plugins: [
    `gatsby-transformer-remark`,
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `content`,
        path: `${__dirname}/src/content`,
      },
    },
  ]
}
```

`src/content/hello-world.md`

```
---
title: Hello World
date: 2020-07-10
path: /hello-world
---hello world
```

我们从`src/content`文件夹中获取降价文件。

顶部是前面的内容，我们将使用它来创建我们的页面。

当我们运行`gatsby develop`并转到[http://localhost:8000/_ _ graph QL](http://localhost:8000/__graphql)时，我们可以通过编写以下内容来查询降价文件:

```
{
  allMarkdownRemark {
    edges {
      node {
        frontmatter {
          path
        }
      }
    }
  }
}
```

然后我们得到:

```
{
  "data": {
    "allMarkdownRemark": {
      "edges": [
        {
          "node": {
            "frontmatter": {
              "path": "/hello-world"
            }
          }
        }
      ]
    }
  },
  "extensions": {}
}
```

从回应来看。

现在我们需要从 Markdown 文件创建页面。

为此，我们写道:

`gatsby-node.js`

```
const path = require(`path`)
exports.createPages = async ({ actions, graphql }) => {
  const { createPage } = actions
  const result = await graphql(`
    {
      allMarkdownRemark {
        edges {
          node {
            frontmatter {
              path
            }
          }
        }
      }
    }
  `)
  if (result.errors) {
    console.error(result.errors)
  }
  result.data.allMarkdownRemark.edges.forEach(({ node }) => {
    createPage({
      path: node.frontmatter.path,
      component: path.resolve(`src/templates/post.js`),
    })
  })
}
```

`src/templates/post.js`

```
import React from "react"
import { graphql } from "gatsby"
export default function Template({ data }) {
  const { markdownRemark } = data
  const { frontmatter, html } = markdownRemark
  return (
    <div className="blog-post">
      <h1>{frontmatter.title}</h1>
      <h2>{frontmatter.date}</h2>
      <div
        className="blog-post-content"
        dangerouslySetInnerHTML={{ __html: html }}
      />
    </div>
  )
}
export const pageQuery = graphql`
  query($path: String!) {
    markdownRemark(frontmatter: { path: { eq: $path } }) {
      html
      frontmatter {
        date(formatString: "MMMM DD, YYYY")
        path
        title
      }
    }
  }
`
```

在`gatsby-node.js`中，我们进行了与在 GraphiQL 中相同的查询。

然后我们得到响应并调用`createPage`来创建带有在 Markdown 的前端定义的文件的`path`的页面。

而`component`有模板渲染前面的事和内容。

在`post.js`中，我们从`data`道具中获取数据。

我们从`frontMatter`对象中获取`title`和`date`属性来获取前台事件数据并显示出来。

然后内容在`markdownRemark.html`属性中。

现在，当我们转到[http://localhost:8000/hello-world](http://localhost:8000/hello-world)时，我们看到:

```
Hello World
July 10, 2020
hello world
```

已显示。

# 结论

我们可以在 Gatsby 静态站点中呈现 Markdown 的数据。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**