# Astro 将成为您最喜爱的静态网站生成器

> 原文：<https://javascript.plainenglish.io/astro-906b03f63ab8?source=collection_archive---------4----------------------->

## 用它构建下一个项目的 4 个理由

![](img/2d59625de928763538db624cf41b340a.png)

Image credits: [CSS-tricks.com](https://css-tricks.com/wp-content/uploads/2021/05/astro-homepage.png)

当我研究这篇文章时，我感到震惊。阿童木仍然不为人知。当然，静态站点生成器仍然很年轻——但是它也很有创新性，不应该错过炒作。

如果你从未听说过 Astro，不要担心——几周前，我做了一个[介绍](/astro-cec429f049d)，这篇文章你不需要任何先验知识。

自从我介绍之后，发生了很多变化 Astro 已经成为我构建静态页面的首选工具。它甚至接管了 Next 和 Gatsby。
以下是我如此热爱阿童木的原因。

# 1.编写 JavaScript，发布时不使用它

默认情况下，如果 Astro 有一个突出的特性，那就是它的零大小客户端 JavaScript 包。这意味着 Astro 实际上默认删除了组件中的所有 JavaScript 代码。

然而，我们可以使用 JS 技术编写组件，比如 React.js。我们可以在 React 中写一个表:

```
const names = ["Max", "Tom", "Carl"]export default function App() {
  return (
    <ul>
      {names.map((item, index) => {
        return <li key={index}>{item}</li>
      })}
    </ul>
  );
}
```

Astro 会在生成时预渲染这些内容，剩下的 HTML 结构会被放到最终页面中。JSX 代码和许多千字节的框架代码被简单地删除。

它仍然是一个加载速度很快的静态页面。当然，我们经常需要 JavaScript 来使页面动态化。但是对于这样的静态组件，多亏了 Astro，我们可以节省几千字节的 JavaScript。

由于组件的隔离处理，在 Astro 中，我们可以正常加载一些组件，其他的完全不需要 JavaScript——但是，其他的可以延迟加载。

# 2.更好的性能，使用相同的框架或库

如果两个不同的静态页面生成器为同一个框架工作，性能应该是一样的，对吗？不，不总是。我**不是**在说生成站点时的性能，而是影响客户端的性能(加载时长，第一次内容绘制等。).

每个 SSG 都有不同的实现方式——就渲染方式和捆绑包大小而言。

Astro 在性能方面大放异彩。我试了一下，在 Gatsby，Next.js，Astro (Next 也可以导出静态页面)里搭建了同样的 app。结果是:Astro 提供了最好的性能和最小的包。

原因是部分水合和切掉不必要的 JavaScript 代码。虽然 Next.js 和其他 SSG 包含了大量的运行时代码，但 Astro 只对真正需要的组件进行了最低限度的处理。

# 3.完美组合页面加载方式

惰性加载现在已经出现在许多框架和静态站点生成器中。

Next.js 提供的，盖茨比也是——当然还有阿童木。Astro 甚至为我们提供了两种不同的方法来做到这一点。除了完全不用 JavaScript 加载组件之外，我们还可以:

1.  仅当组件出现在客户端的视口中时才加载它。
2.  一旦浏览器的主线程空闲就加载组件，不要阻塞任何重要的东西。
3.  一旦浏览器与定义的视口匹配，就加载零部件。
4.  加载页面时以“正常”方式加载组件。

Astro 不仅在加载组件的可能性方面大放异彩，而且在实现起来也非常容易。虽然 React.js 或 Next.js 中的延迟加载稍微复杂一些，但在 Astro 中，它只是 HTML 属性:

1.  `<MyComponent client:visible/>`
2.  `<MyComponent client:idle />`
3.  `<MyComponent client:&#123;QUERY} />`
4.  `<MyComponent client:load />`

当然，在没有任何 JavaScript 的情况下加载它:`<MyComponent />`——没有任何属性。

# 4.不需要局限于一种技术

同时使用 Vue 或 React 等多种技术构建 web 应用听起来像是一个糟糕的笑话。然而，Astro 使这成为可能——在某种程度上，这是有意义的。Astro 基本上是一个 SSG，它不仅为一个库或框架工作。反例如 Gatsby 或 VuePress，分别只对 React 和 Vue 有效。

Astro 只需要安装一个额外的模块，你可以支持任何库/框架。目前支持 React，Vue，Svelte，Preact，甚至 Solid。理论上，没有什么能阻止你在同一个页面上使用 React 组件和 Vue 组件——Astro 使这成为可能。

有多大用处值得商榷。然而，如果你已经有了一个来自某个框架的组件，Astro 可以很容易地处理它，使工作更加灵活和容易。

感谢您的阅读！

如果你想了解更多关于 Astro 的知识，可以看看我的介绍:

[](/astro-cec429f049d) [## Astro 入门——创新的静态站点生成器

### 多框架的 SSG，最小化我们发布的 JS

javascript.plainenglish.io](/astro-cec429f049d) 

*更多内容请看*[***plain English . io***](http://plainenglish.io)