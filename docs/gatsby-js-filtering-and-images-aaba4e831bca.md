# Gatsby.js —过滤和图像

> 原文：<https://javascript.plainenglish.io/gatsby-js-filtering-and-images-aaba4e831bca?source=collection_archive---------10----------------------->

![](img/a099fb1c1bacb8612ecf868bd1addaad.png)

Photo by [Richard T](https://unsplash.com/@newhighmediagroup?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Gatsby 是一个基于 React 的静态网站框架。

我们可以用它从外部数据源创建静态网站等等。

在本文中，我们将看看如何用 Gatsby 创建一个站点。

# 使用 GraphQL 过滤

我们可以使用 GraphQL 查询过滤结果中的项目。

例如，我们可以写:

```
{
  allSitePage(filter: {path: {eq: "/pokemon"}}) {
    edges {
      node {
        id
        path
      }
    }
  }
}
```

然后我们得到等于 T1 的 T0。

`eq`意为平等。

# GraphQL 查询别名

我们可以添加 GraphQL 查询别名。

例如，我们可以写:

```
{
  fileCount: allFile { 
    totalCount
  }
  filePageInfo: allFile {
    pageInfo {
      currentPage
    }
  }
}
```

`fileCount`和`filePageInfo`是别名。

冒号后的表达式是查询。

# GraphQL 查询片段

GraphQL 查询片段是可以重用的可共享的查询块。

例如，我们可以创建一个片段，并通过编写以下内容使用它进行查询:

`src/pages/index.js`

```
import React from "react"
import { graphql } from "gatsby"export const query = graphql`
  fragment SiteInformation on SiteSiteMetadata {
    title
    description
  }
`export const pageQuery = graphql`
  query SiteQuery {
    site {
      siteMetadata {
        ...SiteInformation
      }
    }
  }
`export default function Home({ data }) {
  return <div>{data.site.siteMetadata.title}</div>
}
```

我们用`query`查询创建片段。

我们为`SiteSiteMetadata`类型创建片段，它包含网站的元数据字段。

然后`pageQuery`使用我们刚刚创建的片段。

# 用`fetch`查询数据客户端

我们可以使用 Fetch API 在客户端查询数据。

例如，我们可以写:

```
import React, { useState, useEffect } from "react"const IndexPage = () => {
  const [starsCount, setStarsCount] = useState(0)
  useEffect(() => {
    fetch(`https://api.github.com/repos/gatsbyjs/gatsby`)
      .then(response => response.json())
      .then(resultData => {
        setStarsCount(resultData.stargazers_count)
      })
  }, []) return (
    <section>
      <p>Gatsby start count: {starsCount}</p>
    </section>
  )
}
export default IndexPage
```

来获取 Gatsby 项目的 Github 星数并显示出来。

# 形象

我们可以在我们的盖茨比项目中添加图像。

例如，我们可以写:

`src/pages/index.js`

```
import React from "react"
import LaptopImg from "../assets/laptop.jpg"const IndexPage = () => {
  return (
    <section>
      <img src={LaptopImg} alt="laptop" />
    </section>
  )
}
export default IndexPage
```

我们从`/assets`文件夹中导入图像，并将`src`属性设置为导入的图像。

# 参考`static`文件夹中的图像

此外，我们可以通过路径引用`static`文件夹中的图像。

例如，我们可以写:

```
import React from "react"const IndexPage = () => {
  return (
    <section>
      <img src={`laptop.jpg`} alt="laptop" />
    </section>
  )
}
export default IndexPage
```

假设我们在`static`文件夹中有图像。

# 用 gatsby-image 优化和查询局部图像

我们可以使用`gatsby-image`来添加图像。

要安装软件包所需的软件包，我们运行:

```
npm i gatsby-plugin-sharp gatsby-transformer-sharp
```

为此，我们写道:

`gatsby-config.js`

```
const path = require('path');module.exports = {
  plugins: [
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        name: `images`,
        path: path.join(__dirname, `src`, `images`),
      },
    },
    `gatsby-plugin-sharp`,
    `gatsby-transformer-sharp`,
  ],
}
```

然后，我们可以通过编写以下内容来获取页面上的图像:

`src/pages/index.js`

```
import React from "react"
import { useStaticQuery, graphql } from "gatsby"
import Img from "gatsby-image"const IndexPage = () => {
  const data = useStaticQuery(graphql`
    query {
      allFile(
        filter: {
          extension: { regex: "/(jpg)|(png)|(jpeg)/" }
          relativeDirectory: { eq: "" }
        }
      ) {
        edges {
          node {
            base
            childImageSharp {
              fluid {
                ...GatsbyImageSharpFluid
              }
            }
          }
        }
      }
    }
  `) return (
    <div>
      {data.allFile.edges.map(image => (
        <Img
          fluid={image.node.childImageSharp.fluid}
          alt={image.node.base.split(".")[0]}
        />
      ))}
    </div>
  )
}
export default IndexPage
```

我们通过`allFile`查询获得文件。

我们从`src/images`文件夹中获取我们在`gatsby-config.js`中指定的图像。

# 结论

我们可以用 GraphQL 过滤项目，我们可以用 GraphQL 查询得到图像并显示它们。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**