# 使用帧运动在 Next.js 中创建页面过渡

> 原文：<https://javascript.plainenglish.io/how-to-create-page-transitions-in-next-js-with-framer-motion-47642c462c62?source=collection_archive---------1----------------------->

## 如何在 Next.js 中使用帧运动创建页面过渡

![](img/da047714cb2b7ae7014144c045551d56.png)

所以今天我们将看看如何在 Next.js 中实现页面间的动画

您可以简单地克隆[下一个顺风启动模板](https://github.com/avneesh0612/Nextjs-tailwind-starter-template)，并按照自述文件中的步骤操作。

我将使用 tailwind CSS 进行基本的样式设计。请随意使用任何东西。

我们将在我们的应用程序中安装 framer motion。

```
npm i framer-motion # npm
yarn add framer-motion # yarn
```

## 创建页面

首先，在 pages 文件夹中新建一个文件。这将为您创建一条新路线。

我把它命名为 **about.js** 。这是文件。我只是创建了一个`h1`标签和一个`button`，它们将重定向到主页。

现在我将在 **index.js** 中做同样的事情。

我们已经设置了两个页面。它看起来会像这样。

## 创建过渡

现在我们将前往 **_app.js**

进口`motion`:

```
import { motion } from “framer-motion”;
```

将应用程序封装在一个`motion.div`中:

我们将把`initial`、`animate`和`variants`传递给我们的`motion.div`:

这将在第一次渲染时产生动画效果，但不会改变路线。因此，我们将添加一个通过道具获得的`router.route`键。

这将给我们一个很好的淡入动画，同时改变路线

我希望你能建立美丽的页面过渡。如果你有任何问题，请随时联系我下面列出的任何一个社交网站。和平✌🏻

有用的链接:

[该项目的 Github 库](https://github.com/avneesh0612/pages-transition-with-framer-motion)

[成帧器运动文件](https://www.framer.com/motion/)

[Next.js docs](https://nextjs.org/docs)

[所有社交](https://avneesh-links.vercel.app/)

## 进一步阅读

[](https://blog.bitsrc.io/next-js-13-what-do-the-new-bleeding-edge-features-actually-do-d3e5fd418563) [## Next.js 13:新的前沿特性实际上是做什么的？

### 你听说过 Next.js 13 是一个游戏改变者，但是为什么？让我们看看有哪些新功能，有哪些变化，以及它们…

blog.bitsrc.io](https://blog.bitsrc.io/next-js-13-what-do-the-new-bleeding-edge-features-actually-do-d3e5fd418563) 

*更内容于* [***普通英语***](https://plainenglish.io/) *。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。在*[***Twitter***](https://twitter.com/inPlainEngHQ)[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*以及*[**T42 不和**](https://discord.gg/GtDtUAvyhW) *上跟随我们。对增长黑客感兴趣？查看* [***电路***](https://circuit.ooo/) *。**