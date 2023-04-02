# 开始使用 Gatsby.js 创建静态站点

> 原文：<https://javascript.plainenglish.io/getting-started-with-creating-static-sites-with-gatsby-js-fbdcae9c5f11?source=collection_archive---------8----------------------->

![](img/09321bcd93ca4cdac5282f532c5a031b.png)

Photo by [Sam Browne](https://unsplash.com/@samjbrowne?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Gatsby 是一个基于 React 的静态网站框架。

我们可以用它从外部数据源创建静态网站等等。

在本文中，我们将看看如何用 Gatsby 创建一个站点。

# 安装 Gatsby CLI

我们运行:

```
npm install -g gatsby-cli
```

安装 Gatsby 命令行界面。

# 创建新网站

一旦我们安装了 Gatsby CLI，我们运行:

```
gatsby new gatsby-site https://github.com/gatsbyjs/gatsby-starter-hello-world
```

让 Gatsby CLI 创建一个项目。

然后我们可以通过运行 dev 服务器开始开发:

```
cd gatsby-site
gatsby develop
```

当我们进行更改时，我们将看到显示的最新更改。

# 创建生产版本

为了创建生产构建，我们运行:

```
gatsby build
```

为了服务于本地的生产构建，我们运行:

```
gatsby serve
```

# 页

我们将页面添加到`src/pages`文件夹中。

我们可以用`Link`组件链接页面。

例如，我们可以写:

`src/pages/foo.js`

```
import { Link } from "gatsby"
import React from "react"export default function Foo() {
  return <>
    <Link to='/foo'>foo</Link>
    <Link to='/bar'>bar</Link>
    <div>foo</div>
  </>
}
```

`src/pages/bar.js`

```
import React from "react"
import { Link } from "gatsby"export default function Bar() {
  return <>
    <Link to='/foo'>foo</Link>
    <Link to='/bar'>bar</Link>
    <div>bar</div>
  </>
}
```

我们添加了`Link`组件，链接到页面将被添加。

URL 路径由文件名决定。

所以`foo.js`映射到`/foo`，而`bar.js`映射到`/bar`。

# 布局

我们可以用 Gatsby 创建一个布局组件，在多个页面之间添加共享的标记、样式和功能。

为此，我们写道:

`src/components/layout.js`

```
import { Link } from "gatsby"
import React from "react"export default function Layout({ children }) {
  return (
    <div style={{ margin: `0 auto`, maxWidth: 650, padding: `0 1rem` }}>
      <Link to='/foo'>foo</Link>
      <Link to='/bar'>bar</Link>
      {children}
    </div>
  )
}
```

`src/pages/foo.js`

```
import React from "react"
import Layout from "../components/layout"export default function Foo() {
  return <Layout>
    <div>foo</div>
  </Layout>
}
```

`src/pages/bar.js`

```
import React from "react"
import Layout from "../components/layout"export default function Bar() {
  return <Layout>
    <div>bar</div>
  </Layout>
}
```

我们将`Link`组件移到了`layout.js`，这样我们就可以在一个地方引用所有内容。

在`Layout`组件中，我们有`children`属性来呈现包装在`Layout`组件中的子组件。

# 使用 createPage 以编程方式创建页面

我们可以通过编程来创建页面。

为此，我们写道:

`gatsby-node.js`

```
exports.createPages = ({ actions }) => {
  const { createPage } = actions
  const dogData = [
    {
      name: "fido",
      breed: "Sheltie",
    },
    {
      name: "sparky",
      breed: "Corgi",
    },
  ]
  dogData.forEach(dog => {
    createPage({
      path: `/${dog.name}`,
      component: require.resolve(`./src/templates/dog-template.js`),
      context: { dog },
    })
  })
}
```

`src/templates/dog-template.js`

```
import React from "react"export default function DogTemplate({ pageContext: { dog } }) {
  return (
    <section>
      {dog.name} - {dog.breed}
    </section>
  )
}
```

我们导出`createPages`函数。

在函数内部，我们用页面的`path`调用`actions.createPage`函数。

`component`拥有我们想要呈现数据的模板。

`context`有我们想要渲染的数据。

然后在`dog-template.js`中，我们从`pageContext`道具中获取数据并渲染它们。

现在，当我们转到[http://localhost:8000/fido](http://localhost:8000/fido)时，我们看到:

```
fido - Sheltie
```

当我们转到[http://localhost:8000/sparky](http://localhost:8000/sparky)时，我们会看到:

```
sparky - Corgi
```

# 结论

我们可以使用 Gatsby.js 手动和自动添加页面

喜欢这篇文章吗？如果是这样，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**