# 使用 React 和 TypeScript 创建面包屑组件

> 原文：<https://javascript.plainenglish.io/create-a-breadcrumb-component-with-react-and-typescript-46863155dcea?source=collection_archive---------4----------------------->

## 一次性增强搜索结果和用户导航

![](img/8df09bbfd40e97e5df75e36bc644d9f6.png)

Photo by [Linhao Zhang](https://unsplash.com/@lintaho?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

网页上的面包屑轨迹指示用户当前在网站层级中的位置。它可以帮助用户更有效地浏览网站。面包屑允许用户在网站的层次结构中一次向上导航一级。本文探讨了如何在 React 和 Typescript 中用不到 50 行代码轻松实现 breadcrumb。

创建面包屑的目标有两个。面包屑为用户提供了一种导航网站结构的简单方法。此外，正确的实现丰富了搜索引擎的搜索结果。后者通过提供结构化数据来实现。

# 结构数据

首先，让我们更深入地了解结构化数据。搜索引擎尽最大努力解析和理解它们所抓取的网站的结构。但他们对特定网页上的内容了解有限。

结构化数据为搜索引擎提供了关于网页内容的附加信息。有各种类型的结构化数据。关于食谱、书籍、评论、文章等等的信息都可以添加到网页上。

Schema.org 为谷歌、微软、雅虎和 Yandex 支持的结构化数据提供了一个共享词汇表。值得注意的一点是，并不是所有的模式都能增强最终用户的搜索体验。

哪些模式有助于你的网站在搜索结果中显示更丰富的功能，可以在谷歌的的[搜索图库中找到。一个](https://developers.google.com/search/docs/guides/search-gallery)[的面包屑](https://developers.google.com/search/docs/data-types/breadcrumb)是显示导航的模式的一个例子，它指示页面在站点层次结构中的位置。

在网页上包含结构化数据有多种格式。最值得注意的是 [JSON-LD](https://json-ld.org/) 和[微数据](https://www.w3.org/TR/microdata/)。使用 JSON-LD，数据包含在页面的脚本标记中。相比之下，微数据将元数据嵌套在页面的现有内容中。使用这种格式，HTML 属性被用来在网页上嵌入简单的机器可读数据。

本文使用微数据，因为它减少了所需的代码量。用同样的代码达到了帮助用户和搜索引擎的目的，一举两得。

# 微观数据

微数据是一个 [HTML 标准](https://www.w3.org/TR/microdata/)。本质上，微数据由一组名称-值对组成。每个组称为一个项目。特定的名称-值对描述了项目的属性。

为了指定一个项目，将`itemscope`属性添加到一个元素中。当添加这个属性时，您就声明了该元素中包含的 HTML 是关于某个项目的。

项目有一定的类型。这是由`itemtype`属性指定的。项目类型以 URL 的形式提供给[schema.org](http://schema.org)网站。

项目的附加信息在其属性中定义。这些是通过向元素添加一个或多个`itemprop`属性来声明的。这些属性被附加到该项目的嵌套元素上。属性可以是字符串或 URL。后者通常使用`<a>`元素及其 href 属性来表示。

上面提供了一个关于电影的微数据的例子。外部 div 元素通过将 itemscope 属性及其 itemtype 设置为 [movie](http://schema.org/Movie) 来定义电影项目。嵌套元素都描述了电影的某些属性。它们所描述的是使用 itemprop 属性声明的。

这是一个相当简单的例子。然而，有时项目属性的值本身可以是另一个具有自己的属性集的项目。下一节将对此进行说明。

# 利润

在[谷歌搜索中心](https://developers.google.com/search/docs/data-types/breadcrumb)可以找到面包屑微数据的例子。使用有序列表，其中列表元素用>字符可视地分开。

外部的`<ol>`标签定义了一个名为 BreadcrumbList 的微数据项。这种类型的精确属性可以在[这里](https://schema.org/BreadcrumbList)找到。该列表包含三个元素，每个元素描述一个 itemListElement，它是 BreadcrumbList 的一个属性。

在上一节中，我们注意到，有时一个项目属性的值本身可以是另一个具有自己的属性集的项目。面包屑列表的属性就是这种情况。列表元素本身就是一个项目，即 ListItem。

可以观察到 ListItem 的三个属性。url，由元素的*项目*属性、*名称*和*位置*表示。请注意，该位置以 1 而不是 0 开始。

# 功能组件和道具

现在，让我们开始考虑 React 组件以及呈现上述标记的组件所需的数据。变量是已知的，因此为组件的属性创建类型定义相对简单。

传递给组件的数据是 breadcrumb 元素的数组，每个元素都有一个`url`和`name`，它们都是字符串。让我们将用户界面分解成 React 的组件层次结构。

可以发现最后一部分的标记中的重复元素:条目列表。这由两个功能组件实现，一个用于`Breadcrumb`本身，另一个用于其中的元素:`BreadcrumbItem`。

面包屑功能组件接收`BreadcrumbProps`作为参数。该组件可以实现为:

列表被包装在一个`nav`标签中，因为内容定义了一个导航链接块。使用(稍微修改的) [BEM](http://getbem.com/) 方法添加类名，以允许以后进行样式化。其余的标记与上面显示的 HTML 示例完全一样。需要注意的一点是，属性在 camelCase 中，这是 React 中所有 DOM 属性的预期属性。

组件接收的 breadcrumb 条目的数组是使用 [map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 函数呈现的，该函数将`BreadcrumbItemProps`对象映射到`BreadcrumbItem`组件。

`BreadcrumbItem`组件需要四个变量:`url`、`name`、`index`和一个名为`isLast`的布尔变量。前两个由数组中当前对象的属性提供，使用[扩展语法](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)。通过将正在处理的当前元素的索引加 1 来传递 position 属性。

如果某个`BreadcrumbItem`是列表的最后一个元素，则不应该呈现可视分隔符。因此，组件需要知道它是否是最后一项。这是通过检查 map 函数中当前项的索引是否等于数组长度减一(因为索引从零开始)来实现的。

最后但同样重要的是，添加了一个`key`属性，这不是传递给组件本身的属性。[键](https://reactjs.org/docs/lists-and-keys.html)是内部反应。它帮助 React 识别哪些项目已经更改、添加或删除。应该给数组内部的元素赋予键，以给元素一个稳定的标识。在代码中，索引被用作关键字。

`BreadcrumbItem`可以按如下方式实现:

`isLast`参数用于有条件地渲染分割线。当显示分隔线时，组件将返回多个 DOM 元素，因此它被包装在一个`Fragment`中。 [Fragments](https://reactjs.org/docs/fragments.html) 让您不用向 DOM 添加额外的节点就可以对孩子列表进行分组。

# 丰富结果的验证

面包屑现在可以呈现如下:

breadcrumb 变量是一个遵循`BreadcrumbProps`接口的对象。有许多方法可以达到这个目的。它可以被定义在你的服务器上的一个文件中，或者你可以从后端接收它。出于演示的目的，它被硬编码在一个常量变量中。

该组件呈现以下 html:

可以使用 Google 的 [Rich Results Test](https://search.google.com/test/rich-results) 来验证呈现的 HTML。代码可以粘贴在那里，它将显示该页面有资格获得丰富的结果。面包屑的功能已经完成。

唯一剩下的事情就是设计面包屑的样式。这将留给读者作为练习，因为有太多的方法可以达到这个目的。由于有许多方法，造型会根据情况有很大的不同。

# 结论

本文展示了一种实现包含结构化数据的面包屑的简单方法。感谢您的阅读！我鼓励你去探索其他可以用来丰富网页搜索结果的模式。

本文展示了一个微数据示例。然而，当内容还没有出现在页面上时，使用 JSON-LD 可能更简单。可以看一下 [React Schemaorg](https://github.com/google/react-schemaorg) ，它提供了两个 npm 包。其中一个以 JSON-LD 格式为 Schema.org 的[词汇表提供了类型定义。而另一个提供了在 React 应用中轻松插入有效的 Schema.org](http://schema.org/)[JSON-LD 的方法。](http://schema.org/)

# 资源

 [## Schema.org-Schema.org

### Schema.org 是一个协作性的社区活动，它的任务是创建、维护和推广…

schema.org](https://schema.org/)  [## 面包屑列表

### Schema.org 类型:面包屑列表——面包屑列表是一个项目列表，由一系列链接的网页组成，通常…

schema.org](https://schema.org/BreadcrumbList) [](https://developers.google.com/search/docs/guides/search-gallery) [## 探索搜索库和丰富的结果|谷歌搜索中心

developers.google.com](https://developers.google.com/search/docs/guides/search-gallery) [](https://developers.google.com/search/docs/data-types/breadcrumb) [## 面包屑|谷歌搜索中心|谷歌开发者

developers.google.com](https://developers.google.com/search/docs/data-types/breadcrumb)  [## HTML 微数据

### 这个[html-extensions]规范定义了新的 html 属性，以便在 HTML 中嵌入简单的机器可读数据…

www.w3.org](https://www.w3.org/TR/microdata/)