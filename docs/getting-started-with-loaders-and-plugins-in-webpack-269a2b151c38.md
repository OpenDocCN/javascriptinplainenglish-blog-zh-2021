# Webpack 中的加载器和插件入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-loaders-and-plugins-in-webpack-269a2b151c38?source=collection_archive---------16----------------------->

![](img/80394bbd6fbccf92d52f980ec71afc35.png)

Photo by [Megan Newman](https://www.pexels.com/@mnnewmanphoto?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/jellyfish-underwater-1748265/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

2016 年，我在澳大利亚旅行了几周，平生第一次尝试冲浪。我喜欢它，但每当我下水时，我都有一种不安的感觉。水面下有水母，在我观察了几个不幸的游泳者后，我知道触摸它们会受伤。

对我来说，Webpack 有点像这些水母。这是发展环境的一部分，有理由存在，但我们通常会尽量远离对方，因为我们知道任何接触对我们双方来说都是痛苦的。不幸的是，我最近在工作中遇到的许多技术问题似乎都与 webpack 有关，因此避免接触很少是一种选择。我通常会向一位同事寻求帮助，我们通过谷歌和大量实验解决了这个问题。

对我来说，关于 webpack 的大部分困惑都源于我自己从来没有设置过它，也没有真正理解它背后发生了什么。我想很多人都是这样，因为你通常不会从头开始配置 webpack。例如，当您开始一个新的 Vue 项目时，Vue CLI 将为您预配置 webpack。我想 React 也是如此。这很方便，因为您不想在每次启动新项目时都花半个小时来设置 webpack。但是如果你至少一次都没有自己设置过，那么一旦你不得不定制它，这种“魔力”就很难理解了。因此，让我们看看引擎盖下，并建立自己的 webpack。不过，我们不会把一堆现有的插件缝合在一起。我们将从头开始建造它们💪。

# webpack 试图解决的问题

让我们从头开始，弄清楚 webpack 实际上是什么。 [webpack 文档](https://webpack.js.org/concepts/)将 webpack 描述为*“现代 JavaScript 应用的静态模块捆绑器”*这听起来很棒，但是如果你不太了解 bundlers，那么，最重要的是，这听起来非常抽象。简而言之，webpack 会查看您的 JavaScript 代码，找出它的所有依赖项，并将它们打包到一个目录中，作为一个或多个文件。

几年前，这是不必要的，因为 JavaScript 应用程序通常没有那么大。你可以在 HTML 中包含几个`<script>`标签。但是现在，应用程序已经变得如此之大，以至于如果你试图以正确的顺序手动包含所有的 JavaScript 文件，你的脑袋会爆炸。但是 webpack 走得更远，它使得捆绑图像、样式表甚至你的 HTML 成为可能。它通过加载器和插件完成所有这些工作，使得 webpack 非常具有可定制性——有时还会让你脑袋爆炸。

# 项目设置

我们将构建一个简单的前端应用程序，包括一些 HTML，CSS 和 JavaScript，并将所有这些与 webpack 捆绑在一起。这将是一个很小的项目，但它应该足以说明 webpack 背后的一些概念。让我们设置项目文件夹并安装 webpack 和 [webpack-cli](https://github.com/webpack/webpack-cli#readme) 。

```
mkdir webpack-from-scratch
cd webpack-from-scratch
mkdir src
echo "console.log('Hello world');" > src/index.js
yarn add -D webpack webpack-cli
```

现在我们可以从终端运行`yarn webpack bundle`，webpack 会捆绑我们的`index.js`，输出到`dist/main.js`。webpack 如何知道为我们捆绑哪个文件？按照惯例。默认的 webpack 配置假设存在一个`src/index.js`文件，并使用它作为包的入口点。“入口点”是 webpack 开始构建依赖关系树的源文件。您可以[更改入口点，甚至添加多个入口点](https://webpack.js.org/concepts/entry-points/)，但是在我们的例子中我们不必这样做。让我们来看看我们捆绑的应用程序的内容:

dist/main.js

当然，webpack 还没有真正给我们的项目增加任何价值。我们可以很容易地把`index.js`文件复制到我们自己身上。但我们会谈到这一点。首先，让我们添加一个 HTML 文件来加载 JavaScript 代码。稍后我们将研究如何自动捆绑它，但是现在，让我们将文件保存在`dist/`文件夹中。

dist/index.html

在浏览器中打开该文件，您应该会看到“Hello world”记录到您的开发人员控制台。接下来，让我们让我们的 JavaScript 实际做一些事情。在我们的网站上显示当前时间怎么样？为了保持代码模块化，创建一个新文件`src/dateFormat.js`来导出一个函数:

src/dateFormat.js

我们在`index.js`中导入函数，在网页上显示当前的工作日和时间，并每秒更新一次。

src/index.js

运行`yarn webpack bundle`重建应用程序，然后再次打开`index.html`。您应该会看到每秒更新一次的时钟。当您再次打开捆绑文件时，您会看到 webpack 已经包含了来自`src/dateFormat.js`的代码。它还精简了代码。

现在我们想给我们的页面添加一些样式。在过去，我们会自己创建样式表并将其添加到 HTML 中。但是让 webpack 处理我们所有的资产有一些好处:每个模块可以显式地导入它所依赖的资产。这使得开发人员更容易跟踪依赖关系，并且允许 webpack 只包含包中实际需要的东西。例如，如果您的网站有五个使用不同 JavaScript 和样式表的页面，您可以创建五个包，每个包都有自己的依赖树。只要你的代码库很小，这可能听起来没什么大不了的，但最终，你的应用程序会增长。排除不需要的代码可能会在页面加载过程中产生几毫秒的差异，而这在 web 上可能是永恒的。

# 用 webpack 加载样式表

我们将样式保存在`src/style.css`中。让我们给正文一个明亮的背景颜色，将文本居中，并更改字体系列和大小:

src/style.css

当我们在`index.js`文件中导入样式表时，webpack 会将它添加到依赖关系树中，并尝试在编译期间加载它。

src/index.js

运行`yarn webpack bundle`会给我们以下错误:

```
You may need an appropriate loader to handle this file type, currently no loaders are configured to process this file. See [https://webpack.js.org/concepts#loaders](https://webpack.js.org/concepts#loaders)
```

Webpack 不知道如何处理样式表。我们将不得不添加一个适当的加载程序来解决这个问题。

# 创建我们自己的样式表加载器

当 webpack 遇到导入语句时，它会将导入文件的内容加载到一个 UTF-8 字符串中。webpack 加载器只是一个函数。它将字符串作为参数，可以选择对其应用转换，并返回结果。真的就这么简单。您可以用几行 JavaScript 代码构建一个加载器:

An example loader

默认情况下，webpack 只知道如何导入 JavaScript 文件。但是你可以配置 webpack 为其他文件类型使用不同的加载器，并且你可以[为相同的文件类型链接多个加载器](https://webpack.js.org/concepts/loaders/#loader-features)。然后，每个加载器将转换资源，并将结果输出传递给链中的下一个加载器。加载器可以以他们喜欢的任何方式转换输入，但是链中的最后一个加载器**必须产生一个有效的 JavaScript 模块**，它将代替原始资源被执行。

我们希望加载器将样式表复制到我们的构建目录中。那么它应该导出生成文件的路径，而不是返回样式表内容。我们可以使用 webpack 的 loader 上下文中的 [emitFile](https://webpack.js.org/api/loaders/#thisemitfile) 函数将样式表发送到构建目录。让我们在`webpack/CssLoader.js`中创建一个样式表加载器:

webpack/CssLoader.js

这将输出一个带有随机文件名的`.css`文件，并返回一个导出文件路径的模块。我们使用一个随机的文件名来避免导入多个具有相同 basename 的样式表时的名称冲突。至关重要的是，你**将加载器定义为普通函数**而不是箭头函数，因为后者不能通过`this`访问加载器上下文。

最初，我试图从加载器返回普通文件路径，希望能够导入它。这不起作用，因为文件路径不是有效的 JavaScript 代码。还记得我之前说过，链中的最后一个加载器必须返回一个有效的 JavaScript 模块吗？请这样想:当您导入一个模块时，webpack 将评估该模块的源代码来代替导入，并在当前范围内公开该模块的导出。

A simplified explanation of the import statement

根据上面的示例，返回普通文件路径将产生以下结果:

An example of importing an invalid module

这不是有效的 JavaScript 代码。首先，没有导出，所以计算的代码不返回值。第二，文件路径没有用引号括起来，导致语法错误。当然，这是对复杂事物的一个非常简单(可能有些错误)的解释，但是我希望它有助于理解加载器的输出是什么样子。
顺便说一下，很容易改变加载器来处理其他文件类型，例如图像。看看关于 raw loaders 的 webpack 文档，了解如何在不将资源转换为 UTF-8 字符串的情况下加载资源。

现在我们已经创建了我们的加载器，我们需要告诉 webpack 使用它。让我们创建一个 webpack 配置文件:

```
touch webpack.config.js
```

并为`.css`文件设置加载器规则:

webpack.config.js

现在我们可以运行`yarn webpack bundle`而不会出现任何错误。但是我们还没有将样式表添加到 HTML 中，所以它不会做任何事情。让我们使用 JavaScript 将样式表附加到 DOM 中:

src/index.js

再次捆绑应用程序，你应该会看到一个美丽，明亮的背景🎉。

![](img/225d93e6fc7120d29207914ef245496d.png)

An impressively styled clock on the web

不幸的是，这有一个缺点:`<link>`标签是在运行时由我们的 JavaScript 代码添加到 DOM 中的，这意味着它是最后加载的，在网页呈现之后，JavaScript 代码执行之后。理想情况下，我们希望在编译期间将`<link>`标签添加到 HTML 中。我们如何做到这一点？用我们自己的插件！

# 构建一个插件在编译时生成 HTML

最初，我们已经创建了`index.html`文件，并手动将其复制到`dist/`文件夹中。当然，我们也可以继续为这个 HTML 文件添加一个样式表的`<link>`标签。但是如果我们有不止一个样式表呢？这很快变得不可收拾。如果 webpack 自动为我们做到这一点岂不是很棒？我们可以用装载机来做吗？
加载器没有模块所依赖的其他资源的信息。我们可以创建一个 HTML 加载器，但是它不知道需要将哪些样式表添加到模板中。相反，我们必须创建一个 webpack 插件。让我们来看看插件是如何工作的。

当我们运行`webpack bundle`命令时，webpack 运行一系列步骤来生成最终的包。它解决依赖性，优化代码，释放资产——这个列表很长。一个插件允许我们挂钩到这些步骤中的每一个来做额外的工作。不幸的是，尽管编写一个插件本身并不复杂，但我很难弄清楚所有可用的钩子是如何工作的，以及我必须使用哪一个。webpack 文档包含了可用钩子的列表，但是关于每个钩子的信息非常有限。对我帮助最大的是钻研一些 webpack 插件的源代码[。好消息是你很少需要自己写插件。现有的 webpack 插件有很多](https://github.com/webpack/webpack/tree/master/lib)，你平时想做的大部分东西已经被别人想出来了。例如，类似于我们将要构建的插件(事实上，它要强大得多)是 [html-webpack-plugin](https://webpack.js.org/plugins/html-webpack-plugin/) 。但我们是来拆纸盒的，所以磨快你的刀。

插件是一个带有`apply`方法的 JavaScript 类。该方法接收一个编译器实例作为参数，它公开了一个我们可以利用的钩子列表。在 webpack 发出所有资产后，我们需要挂钩到编译中，因为这允许我们获得需要添加到 HTML 模板的样式表列表。
我们进入`thisCompilation`钩子，这反过来让我们能够访问`compilationContext`。这再次暴露了我们可以利用的几个钩子，其中之一是`processAssets`钩子。`processAssets`挂钩有多个阶段，我们挂钩到输出额外资产的阶段。我说过这东西很复杂吗？希望代码能让这一点更加清晰。让我们在`webpack/HtmlPlugin.js`中创建插件:

webpack/HtmlPlugin.js

存在嵌套钩子的事实并没有减少这种混乱。我怎么知道要接入哪个钩子？我只是看了一下 [html-webpack-plugin](https://webpack.js.org/plugins/html-webpack-plugin/) 的源代码，看看他们做了什么。关于 `[processAssets](https://webpack.js.org/api/compilation-hooks/#processassets)` [钩子](https://webpack.js.org/api/compilation-hooks/#processassets)的 [webpack 文档实际上很不错，但是我不认为我自己会找到这个钩子。我还运行了许多测试编译，在那里我只是`console.logged`钩子的参数，看看它们的接口是什么。](https://webpack.js.org/api/compilation-hooks/#processassets)

钩子使用了一个 HTML 模板，我们还没有创建它。让我们接下来这样做:

webpack/HtmlPlugin.html

最后，让我们将插件添加到我们的 webpack 配置中:

webpack.config.js

与我们添加自定义加载器时不同，我们需要导入插件，实例化它并将插件实例传递给 webpack。现在您可以从`index.js`中删除事件监听器，但是保留样式表导入。我们不再需要`stylesheetPath`，但是如果没有导入，webpack 不会将样式表添加到依赖关系树中。

src/index.js

当您再次运行`yarn webpack bundle`时，它应该向输出目录发出三个文件:

```
dist/
|- 1612259960631-0.19359674520973624.css
|- index.html
|- main.js
```

`index.html`应该仍然有加粗的文本和美妙的背景颜色，但是现在样式在 JavaScript 之前加载。

# 结论

回过头来看，我们从与 webpack 捆绑在一起的一个 JavaScript 文件开始。然后我们添加了一个样式表，并构建了自己的 webpack 加载器来导入它。最后，我们开发了一个插件，它可以生成一个 HTML 文件，并用`<link>`标签填充到所有的包样式表中。

当然，您通常不会从头开始构建它。有更好的 webpack 加载器和插件可以做得更好，我们只用几行代码就做到了。但我希望你这次享受了为自己建造东西的练习——至少我享受了。我现在也不那么害怕深入 webpack 了，尽管我们仍然只是触及了表面。关于 webpack 能做的事情，你可以写一整本书。谈到书籍，我认为 survivejs.com 上的 [webpack 书籍是了解 webpack 更多信息的绝佳资源。如果你不断尝试，就把它作为参考。例如，您可以扩展插件，让它自动添加链接到 JavaScript 包的`<script>`标签。如果您决定](https://survivejs.com/webpack/foreword/)[更改包名](https://webpack.js.org/configuration/output/#outputfilename)或者如果您配置 webpack 输出多个包，这将非常有用。

感谢您的阅读。

*原载于 2021 年 2 月 13 日*[*https://stricker . digital*](https://stricker.digital/posts/unboxing-webpack/)*。*