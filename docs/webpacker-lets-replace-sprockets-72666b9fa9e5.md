# Webpacker —让我们更换链轮！

> 原文：<https://javascript.plainenglish.io/webpacker-lets-replace-sprockets-72666b9fa9e5?source=collection_archive---------11----------------------->

![](img/70cbcf02db9a3b1c1c4785556a0547d5.png)

Photo by [Robert Thiemann](https://unsplash.com/@rthiemann?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/pack?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

Webpacker 是在 [webpack](https://webpack.js.org/) 之上的一个抽象。它本身是一个广泛使用的资产捆绑工具。它是非常可配置的，因此可以用于许多用例。但是由于它提供了许多选项，它变得有些臭名昭著，因为它配置起来很笨拙。Rails 社区看到了它的许多好处，但是他们想让入门变得更容易，因此他们创建了这个抽象，这反过来又“合并”到了 Rails 本身。

对于版本 6.0，Rails 使用 webpacker 作为 JavaScript 绑定的默认设置。但是如果配置正确，它可以用来整体替换链轮。

## 但是，为什么我们首先要使用 webpack 呢？

使用 webpack，我们可以很好地构建我们的 JavaScript。我们可以使用 babel 开发的现代 ES20**特性，也可以更好地分离关注点，因为我们最终有了一种从其他文件中请求函数的方式。

最大的优势是:我们可以使用 npm 的所有包，因此可以访问互联网上最大的共享空间(前端)包。[这里的](https://blog.appsignal.com/2021/02/17/using-webpacker-in-your-ruby-on-rails-app-deep-dive.html)是对 webpacker 本身更深入的探索。

## **那我们就用 webpack，用一些新的热门的 JavaScript 框架吧！**

因此，让我们看看如何设置 webpacker 来取代链轮，并使用一些额外的 webpack 加载器和插件来使用我们的 Rails 应用程序！

Webpacker 知道如何安装一些现成的 JavaScript 框架。您可以像这样安装它们:

`rails webpacker:install:<framework>`

其中框架可以是 Angular、CoffeeScript、Elm、ERB、React、Stimulus、Svelte、TypeScript 和 Vue 中的一种。

假设您要用这个命令安装 react，会发生什么情况？

Rails 将更新 package.json 文件并运行 yarn，以便所有需要的包都可用。此外，它将在 app/javascript/packs 目录中创建一个`hello_react.jsx`文件。现在你可以把这个`<%= javascript_pack_tag 'hello_react' %>`放到你的一个视图文件中，把 react‘app’包含在你的应用程序中。但是，等一下！这个`javascript_pack_tag`帮手是什么？

## 在 Webpack 的视图中包含文件

链轮增加了每个 Rails 开发者都知道的`javascript_include_tag`、`stylesheet_link_tag`、`image_url`和`asset_url`助手。同样，webpacker 增加了类似的助手，即我们已经见过的`javscript_pack_tag`，以及`stylesheet_pack_tag`、`image_pack_tag`和`asset_pack_tag`。

**短途旅行:入口点**

webpack 的一个重要概念是入口点。入口点是一个文件，它是一个[依赖图](https://webpack.js.org/concepts/dependency-graph/)的根。此外，每个作为入口点的文件都会生成一个新的输出文件。Webpacker *隐含地*知道什么文件是入口点，因此应该生成一个单独的文件。按照惯例，`app/javascript/packs`目录下的每个文件**都是**入口点。这对我们意味着什么？

这意味着我们应该在“javascript”目录下创建一个`src`、`stylesheets`和`images`目录。然后，我们可以在 application.js 文件中引用这些文件，以便将它们包含在捆绑包中。

但是，如果您想为某些页面创建较小的包，例如某种登录页面，您可以在包目录中创建一个 landing_page.js 文件，导入您真正需要的所有依赖项，然后 webpacker 将创建一个新的包，您可以将它包含在`javascript_packt_tag`助手中。

## **对 CSS 使用 web packer**

Webpacker 被配置为也能够捆绑 css。如果您创建了一个 scss 文件，您可以使用`import`将该文件导入到您的 application.js 文件中，webpack 也会创建所需的 css 文件。或者，更准确地说，它将在一个 js 文件中内联并自动加载它。许多现代 JS 框架都使用这种方法。

*Sidenode:* 你可以在 webpacker.yml 文件中查看默认启用了哪些扩展。在`extensions`选项下，您可以看到 webpacker 设置 webpack 默认处理的所有可用文件扩展名。

## 让我们用 SCSS 吧！

在创建了文件 app/JavaScript/style/app _ style . scss 之后，将它添加到 application.js: `import 'style/app_style'`。现在重新加载您的页面，您将看到在您的文件中定义的 css 被应用。(第一次你可能因为某种原因不得不重启 Rails 服务器。)

# **静态资产**

Webpacker 正在设置 webpack，以便能够处理图像或字体等其他静态资产。为此，您必须在 application.js 文件中导入静态资产。*只有这样*你才能在你的 Rails 视图中使用`image_pack_tag`或`asset_pack_tag`助手。

**重要提示:**当您使用这个标签时，您必须在您的路径前面加上“media ”,因为这是 webpack 将静态资产捆绑到的路径。

因此，在您看来，它会是这样的:

```
<%= image_pack_tag “media/images/logo.png” %>
```

如果你有很多文件要导入，我推荐使用`require.context()`方法。这样你就可以要求所有的文件都在一个指定的目录下，而不必一个一个地去做。

# **添加新插件**

如上所述，有了 webpacker，我们可以利用前端社区迄今为止开发的所有功能。这也意味着各种使开发更容易的工具以及一些仅在部署时相关的插件。

webpack 中的插件是*向其添加*功能的包。我最近需要的一个插件是`CopyPlugin`。我不得不把 CKEditor 4 添加到一个应用程序中，为了让它工作，它需要公共目录中的一些源文件。这是你如何添加一个插件到 webpacker(版本 5):

您可以将它添加到 config/web pack/{环境、开发、生产、测试}的任一文件中。js 文件。(因为我在每个模式中都需要这个功能，所以我把它放到了 environment.js 中)

**重要提示:**随着 webpacker 版本 6 的推出，这种情况将会改变！它很可能看起来像这样:

# **添加额外的装载机**

装载机是变压器。加载器将源文件转换成 JavaScript。Webpacker 预先配置了 scss/css 加载程序。如果您想要一个额外的加载器，您可以像这样添加:

同样，这只*对 web packer 5*有效！

这是 webpacker 6 的外观:

因此，这是您想要添加到 webpacker 中以取代链轮的主要内容。

# **部署**

正如我们已经习惯的那样，webpacker 将自己与`rake assets:precompile`任务挂钩。所以，没有变化。

# **结论**

正如我们所看到的，webpacker 能够完全取代资产管道的传统基础，尽管如果你想这样做，它还有一些未加工的边缘。尽管如此，让自己更加了解它是非常有益的，因为它为您的前端带来了更多的选择——最重要的是更容易与 npm 集成！这是一个巨大的推动，因为大部分前端开发都发生在这里。

加载器是用于变压器的 webpack jargoun。他们将他们处理的文件转换成 JavaScript。TypeScript 加载器是一个很好的例子。它将 TypeScript 源代码编译成 JavaScript，然后返回代码。

插件是可以添加到 webpack 中的新功能。它将在构建过程的不同步骤中被执行，这取决于你正在使用的插件的种类。

这使得在 JavaScript 文件中使用 ERB 成为可能。