# Gatsby.js — SASS、插件、主题和数据源

> 原文：<https://javascript.plainenglish.io/gatsby-js-sass-plugins-themes-and-data-sources-5d6e5c531712?source=collection_archive---------14----------------------->

![](img/1661c44b7edaa4e25c9ec2a0c99a5283.png)

Photo by [Webstacks](https://unsplash.com/@webstacks?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Gatsby 是一个基于 React 的静态网站框架。

我们可以用它从外部数据源创建静态网站等等。

在本文中，我们将看看如何用 Gatsby 创建一个站点。

# 与萨斯/SCSS 的风格

我们可以使用萨斯和 SCSS 来设计 Gatsby 项目中组件的样式。

我们只需要创建`.sass`和`.scss`文件，它们会被自动编译成`.css`。

# 使用插件

我们可以通过安装所需的包来添加插件，然后将它们添加到我们的配置中。

例如，如果我们想要添加`gatsby-source-filesystem`插件，我们运行:

```
npm install gatsby-source-filesystem
```

然后在`gatsby-config.js`中，我们加上:

```
/**
 * Configure your Gatsby site with this file.
 *
 * See: https://www.gatsbyjs.com/docs/gatsby-config/
 */module.exports = {
  /* Your site config here */
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: `${__dirname}/src/images`,
      },
    },
  ],
}
```

添加插件。

# 创建新插件

我们可以使用 Gatsby plugin starter 创建自己的插件。

我们运行:

```
gatsby new my-plugin https://github.com/gatsbyjs/gatsby-starter-plugin
```

在我们的项目文件夹中添加插件。

然后在`gatsby-config.js`中，我们通过编写以下代码添加插件:

```
/**
 * Configure your Gatsby site with this file.
 *
 * See: https://www.gatsbyjs.com/docs/gatsby-config/
 */module.exports = {
  /* Your site config here */
  plugins: [
    require.resolve(`../my-plugin`),
  ],
}
```

# 主题

盖茨比让我们用主题来抽象盖茨比配置。

我们运行:

```
npm install gatsby-theme-blog
```

将`gatsby-theme-blog`安装到我们的项目文件夹中。

为了添加主题，我们添加:

```
module.exports = {
  plugins: [
    {
      resolve: `gatsby-theme-blog`,
      options: {
        /*
        - basePath defaults to `/`
        */
        basePath: `/blog`,
      },
    },
  ],
}
```

成`gatsby-config.js`。

此外，我们可以通过运行以下命令来创建一个具有给定主题的新项目:

```
gatsby new {your-project-name} https://github.com/gatsbyjs/gatsby-starter-blog-theme
```

用`gatsby-starter-blog-theme`创造我们的盖茨比项目。

# 数据来源

我们可以将自己的数据源添加到 Gatsby 项目中。

为此，我们写道:

`gatsby-node.js`

```
exports.sourceNodes = ({ actions, createNodeId, createContentDigest }) => {
  const people = [
    { name: "james", age: 20 },
    { name: "mary", age: 23 },
  ]
  people.forEach(({ name, age }) => {
    const node = {
      name,
      age,
      id: createNodeId(`person-${name}`),
      internal: {
        type: "person",
        contentDigest: createContentDigest({ name, age }),
      },
    }
    actions.createNode(node)
  })
}
```

我们添加了`people`数组条目作为数据源，以便它们可以在 GraphQL API 中被查询。

`actions.createNode`方法让我们创建可以查询的数据。

`createNodeId`创建条目的 ID。

`createContentDigest`从字符串或对象创建稳定的内容摘要。

现在，当我们转到[http://localhost:8000/_ _ graph QL](http://localhost:8000/__graphql)时，我们可以进行以下查询:

```
query MyQuery {
  allPerson {
    nodes {
      id
      name
      age
    }
  }
}
```

来获取数据。

我们应该得到这样的结果:

```
{
  "data": {
    "allPerson": {
      "nodes": [
        {
          "id": "48340d0f-e756-5cc7-abb2-c6d83821835e",
          "name": "james",
          "age": 20
        },
        {
          "id": "d2eaea74-1415-52b0-b732-2ac106ec6f55",
          "name": "mary",
          "age": 23
        }
      ]
    }
  },
  "extensions": {}
}
```

作为响应返回。

# 结论

我们可以使用 SASS 或 SCSS，并在我们的 Gatsby 项目中添加插件、主题和数据源。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**