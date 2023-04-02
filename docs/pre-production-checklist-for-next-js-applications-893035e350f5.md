# Next.js 应用程序的生产前清单

> 原文：<https://javascript.plainenglish.io/pre-production-checklist-for-next-js-applications-893035e350f5?source=collection_archive---------3----------------------->

## 在投入生产之前，检查这些性能优化

![](img/1cf157871fe63880c8094978db356e00.png)

Photo by [Sourav Mishra](https://www.pexels.com/@photosbymishra?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/grey-coupe-on-road-3136673/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

**Next.js** 是已经执行的 React 的扩展。我们使用这个令人敬畏的框架来创建面向公众的应用程序。

但是我们经常不能充分利用 Next.js 应用程序的潜力。今天，我们将看到一些优化，您可以在投入生产之前对应用程序实施这些优化。

让我们开始吧。

# 基于路由的代码拆分

当您使用 create-next-app 设置应用程序时，您的应用程序会自动根据您的应用程序的路线进行默认代码拆分。

所以当我们使用`create-next-app`创建一个新的 Next.js 项目时

```
npx create-next-app my-app
```

它创建了一个名为`/pages`的文件夹，您可以在其中使用声明性路由构建页面。所以让我们在`/pages`下创建两个文件

`/pages/home.jsx`->-`http:localhost:3000/home`

`/pages/about.jsx`->-`http:localhost:3000/about`

现在，当你加载你的应用程序时，只有当你转到`http:localhost:3000/home`时，才会加载`home.jsx`的代码。因此，当任何用户访问您的应用程序的主页时，只会发送相关的 javascript。

因此，这是 Next.js 为我们提供的默认的巨大性能优势。但是我们可以做得更好！

# 组件代码拆分

通过动态导入应用程序的组件，可以进一步最小化初始页面大小。

假设在你的`home.jsx`里面有另一个组件。通常你要做的是

```
**import** AnotherComponent **from** '../components/AnotherComponent.jsx';
```

然后在组件内部使用它

```
export function HomePage () { return <div> ... other components <AnotherComponent /> </div>}
```

现在，当你的`HomePage`被加载时，你的页面的所有组件立即被加载。它会使组件在完全加载之前没有响应。这对性能是不利的

但是随着`dynamic`的引入，你现在可以动态地导入组件

```
**import** dynamic **from** 'next/dynamic';**const** AnotherComponent = dynamic(() **=>
**       **import**('../components/AnotherComponent.jsx'));
```

因此，如果使用得当，这可以为您带来巨大的性能提升。

# 缩小图像尺寸

如果您的应用程序组件提供了大量静态图像，您应该减小图像的大小。

网上有很多免费的服务可以做到这一点。最好的是`TinyPNG`

[](https://tinypng.com/) [## TinyPNG -智能压缩 WebP、PNG 和 JPEG 图像

### 问得好！让我给你一个并排的比较。下面是我表妹的两张照片。左图是…

tinypng.com](https://tinypng.com/) 

# 图像的加载

使用 image 组件的 priority 属性来指定是否立即加载它。

默认情况下，其值设置为 false。但是如果你把它设置为 true(不是对每个图像)，那么 Next.js 将尝试预加载图像。这将最终减少 FCP 的时间(第一次内容丰富的油漆)

```
import Image from 'next/image'
.
.
.
<Image priority={true} src={"src-url"}/>
```

仅对文件夹上方的内容执行此操作。

# 固定图像大小

图像有两个必需的属性，名为`width`和`length`，您应该为这两个属性提供值。它们以像素为单位定义。您可以像下面这样做。

```
<Image width={450} height={300} src={"src-url"}/>
```

图像大小应该固定，以避免 CLS(累积布局偏移)。

# 优化 CSS

初始加载不需要所有的 CSS。也许你使用过像(语义 UI 或 AntD)这样的组件库，但只使用了少数几个组件。您的应用程序仍然会尝试加载这些库的整个 CSS。

对于应用程序来说，这可能是非常昂贵且有害的。

有一个超级酷的工具可以移除未使用的 CSS，使用 Next.js 非常容易

[](https://purgecss.com/guides/next.html) [## 移除未使用的 CSS - PurgeCSS

### Next.js 是一个 React 框架，用于可扩展的生产级应用程序。世界领先的公司使用 Next.js 来…

purgecss.com](https://purgecss.com/guides/next.html) 

这种优化将减少 FCP(第一次内容丰富的油漆)时间，这是一个核心网站的重要因素。

# 优化脚本的加载

很多时候你不得不在你的应用程序中使用外部脚本。也许它是一个跟踪你的用户的插件，或者是一个像 Olark 这样的外部聊天服务。

但是这些脚本在应用程序的第一次加载中(大多数时候)没有任何用处。

例如，只有当用户开始与网站交互时，才需要用户跟踪。为此，您无论如何都需要加载整个页面。

尝试使用 Next.js 的`[<Script />](https://nextjs.org/docs/basic-features/script)`标签，并使用 lazyOnLoad 来优化脚本的加载(而不是默认的`script`)。

根据脚本的重要性指定`strategy`属性。可能的值有

`beforeInteractive` - >如果页面交互前需要脚本
`afterInteractive` - >页面交互后
`lazyOnLoad` - >页面加载后加载脚本。

给你。为了获得一个超高性能的 Next.js 应用程序，您可以利用这些特性。

**通过**[**LinkedIn**](https://www.linkedin.com/in/56faisal/)联系我

## 资源:

**代码拆分:**[https://web . dev/Code-splitting-with-dynamic-imports-in-nextjs/](https://web.dev/code-splitting-with-dynamic-imports-in-nextjs/)
Image:[https://nextjs.org/docs/basic-features/image-optimization](https://nextjs.org/docs/basic-features/image-optimization)**purge CSS:**[https://purgecss.com/guides/next.html](https://purgecss.com/guides/next.html)

*更多内容请看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报在这里***](http://newsletter.plainenglish.io/) *。***