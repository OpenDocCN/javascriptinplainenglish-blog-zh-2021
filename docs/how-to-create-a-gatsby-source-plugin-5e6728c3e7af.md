# 如何创建一个 Gatsby 源代码插件

> 原文：<https://javascript.plainenglish.io/how-to-create-a-gatsby-source-plugin-5e6728c3e7af?source=collection_archive---------15----------------------->

## Gatsby 使得通过 GraphQL 和自定义插件向您的站点添加数据变得非常容易！

![](img/d57b1e8ae3c7d9335cd35aaebaf7da7c.png)

Photo Illustration by David Fekke

Gatsby 的一个强大之处在于，你可以将来自完全不同领域的多种来源的内容放入你的网站。盖茨比通过插件做到了这一点。

盖茨比有两种主要形式的插件，“源”和“转换器”。Source 插件允许您将 Gatsby 站点外部的数据引入 Gatsby，Transformer 插件允许您将来自源的数据传递和转换为站点中需要的特定内容。

一旦数据被配置为通过一个源插件进入您的站点，您将能够使用 GraphQL 查询来查询您需要添加到您的站点的特定内容。

您还可以使用 Gatsby 的内置查询编辑器，在运行`gatsby develop`之后，可以通过 GraphiQL `http://localhost:8000/___graphql` url 访问该编辑器。

# 来源

Gatsby 有无限多的来源，包括 API、内容引擎、静态文件甚至数据库。在这篇文章中，我将创建一个从外部 API 获取内容的插件。

# 创建插件

为了创建我的 Gatsby 插件，我将使用 Gatsby CLI 创建一个新的 Gatsby 站点和一个 Gatsby 插件模块。让我们首先使用“Hello World”启动器创建网站。

```
gatsby new playground-site [https://github.com/gatsbyjs/](https://github.com/gatsbyjs/gatsby-starter-plugin)gatsby-starter-hello-world
```

现在让我们在创建操场站点的同一个目录下创建一个源码插件。

```
gatsby new source-plugin [https://github.com/gatsbyjs/gatsby-starter-plugin](https://github.com/gatsbyjs/gatsby-starter-plugin)
```

如果你愿意，你也可以把插件创建到你的 playground-site 文件夹的‘plugins’文件夹中。对于这个例子，我们将把站点和插件放在不同的文件夹中。

```
/playground-site 
/source-plugin 
├── .gitignore 
├── gatsby-browser.js 
├── gatsby-node.js 
├── gatsby-ssr.js 
├── index.js 
├── package.json 
└── README.md
```

# 配置您的插件

现在，让我们通过编辑“游乐场-站点”文件夹根目录下的 **gatsby-config.json** 文件来配置 are“游乐场-站点”使用插件。

```
module.exports = {
  plugins: [require.resolve(`../source-plugin`)],
}
```

我们可以通过在我们的操场上运行`gatsby develop`来测试这个配置是否正确。当你运行游乐场网站时，你应该在终端上看到“加载的盖茨比启动器插件”。

# 向我们的插件添加数据

现在我们已经有了我们的示例插件，让我们修改它，这样它就可以从一个 API 拉进一个源代码。对于这个例子，我将使用星球大战 API。我希望能够使用 GraphQL 从星球大战 API 中查询船舶数据。

Gatsby 提供了一个 API，您可以通过一个名为`createNode`的函数来创建 GraphQL 节点。我们可以在导出名为`sourceNodes`的异步函数的 **gatsby-node.js** 文件中的函数内部使用它。

对于这个例子，我将使用`axios`模块从星球大战 API 获取数据。在您的插件模块中，您可以使用以下 npm 命令添加它；

```
source-plugin> npm i axios --save
```

这将把`axios`添加到 project.json 依赖项中。现在我们已经添加了`axios`，我们可以修改 **gatsby-node.js** 文件，这样 sourceNodes 函数看起来像下面这样；

我们修改了插件中的 **gatsby-node.js** 文件，这样它就可以查询星球大战 API 中的所有飞船，并为每艘飞船添加节点。我们现在通过运行`gatsby develop`命令并查询位于[http://localhost:8000/_ _ _ GraphQL](http://localhost:8000/___graphql)的 Graph QL*I*QL 工具来测试插件是否正在使用 Graph QL 添加节点。

尝试在 graphiql 中执行以下查询；

```
query MyQuery {
  allShip {
    edges {
      node {
        id
        name
        model
      }
    }
  }
}
```

# 在我们的网站上使用这些数据

现在我们有了查询数据的插件，我们可以用它来查询数据并显示在我们的主页上。让我们修改 **index.js** 文件，以便它使用 GraphQL 从我们的插件中查询数据；

正如你在上面的例子中看到的，我们在`graphql`中导入，创建一个查询来获取我们的船数据，然后通过主页函数中的“数据”解构造器输出。

# 结论

Gatsby 使得通过使用源代码插件来扩展内置功能以导入数据变得非常容易。结合 GraphQL 的强大功能，我们现在可以轻松地向 Gatsby 站点添加新的数据源。

*原发布于*[*https://fek . io*](https://fek.io/blog/how-to-create-a-gatsby-source-plugin/)*。*