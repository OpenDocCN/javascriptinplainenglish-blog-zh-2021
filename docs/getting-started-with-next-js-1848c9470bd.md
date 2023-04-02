# Next.js 入门

> 原文：<https://javascript.plainenglish.io/getting-started-with-next-js-1848c9470bd?source=collection_archive---------10----------------------->

## 初学者指南

![](img/f0dd46f0581989077038d95c51ffe064.png)

## 为什么是下一个

从头开始创建一个反应应用程序需要安装 Webpack、Babel、react，并将 React 组件连接到 DOM。使用 Next.js 时，命令 create-next-app 会自动完成所有配置，并为我们提供一个生产就绪的应用程序。

通常，搜索引擎爬虫无法从用 JavaScript 构建的网站中提取数据，因为执行脚本和获取数据需要时间。在 Next.js 中，它有一个通过使用服务器端渲染(SSR)和静态生成(SSG)进行预渲染的内置功能。预渲染意味着渲染所需的 HTML 在服务器端生成并发送到客户端。

预渲染的好处是更好的搜索引擎优化和网站性能。从头开始的反应应用程序构建预计将手动定义路由器，而 Next.js 提供了一个直观的基于页面的路由系统。它还内置了对 CSS 和 Sass 的支持。

## 创建 Next.js 应用程序

要使用 Next.js 创建应用程序，请复制下面的命令并在您的终端上运行它。在执行命令之前，它会询问应用程序名称，您可以提供任何所需的应用程序名称。

```
npx create-next-app
```

执行该命令后，您将得到一个样板，可以根据需求进行定制。在编辑器中打开项目，导航到作为应用程序主页的 pages/index.js。用下面添加的代码替换 index.js 处的当前代码，然后使用命令 **npm run dev** 编译它，并访问以下 URL[http://localhost:3000](http://localhost:3000)。

```
function HomePage() {
  return <div>Introducing Next.js</div>;
}
export default HomePage;
```

## **创建不同页面**

考虑创建一个由主页、关于页面和联系页面组成的个人文件夹网站。我们将研究如何在 Next.js 应用程序中实现这一点。在该文件夹中，pages 创建了另外两个关于. js 和 contact.js 的文件，并分别添加了以下代码。

```
/*
*  File Name: about.js
*  Description: This is the code for about page
*/function About() {
  return <div>About Page</div>;
}export default About;
```

```
/*
*  File Name: contact.js
*  Description: This is the code for contact page
*/function Contact() {
  return <div>Contact Page</div>;
}export default Contact;
```

转到以下 URL[http://localhost:3000/联系](http://localhost:3000/contact)和[http://localhost:3000/关于](http://localhost:3000/about)；你会看到两个不同的页面，没有像传统的反应应用程序那样定义任何路由器。这是可能的，因为 Next.js 有一个直观的基于页面的路由系统。

*为了在页面之间导航，Next.js 提供了一个名为< Link >的内置标签。在 Next.js 中，页面导航只使用<链接>标签；否则，将会影响网站的性能，因为<链接>标签会阻止网站在从一个页面导航到另一个页面时重新加载。*

```
import Link from 'next/link'function HomePage() {
 return (
   <>
     <div>Home Page</div>
     <Link href="/about">
       <a>About Page</a>
     </Link>
     <Link href="/contact">
        <a>Contact Page</a>
     </Link>
   </>
  )
}
export default HomePage;
```

## 添加标题

接下来，js 提供了一个，我们可以在其中提供像标题这样的元数据，并放置我们的 web 应用程序的 favicon。

```
import Head from "next/head";function HomePage() {
  return (
    <>
      <Head>
         <title>Next App</title>
         <link rel="icon" href="/favicon.ico" />
      </Head>
      <div>
         Next App
      </div>
    </>
  );
}export default HomePage;
```

## 添加 CSS

让我们看看如何将 css 导入到 about 页面，在页面级别创建一个 styles 文件夹以创建一个 About.module.css 文件。在该文件中，编写要执行的 CSS 代码，如果只是假设创建如上所述的 CSS 文件，则 styles 文件夹可能已经存在。

```
/*
*  File Name: About.module.css
*  Description: This is the CSS for about page
*/.body {
  background-color: blueviolet;
}
```

```
/*
*  File Name: about.js
*  Description: This is the code for about page
*/import styles from "../styles/About.module.css";function About() {
  return <div className={styles.body}>About Page</div>;
}export default About;
```

我们可以使用 CSS 作为全局变量，只需导入 on _app.js。这样我们就可以避免为不同的页面创建相应的 CSS 文件。

```
/*
*  File Name: _app.js
*  Description: This is root of all pages
*/import '../styles/globals.css'function MyApp({ Component, pageProps }) {
   return <Component {...pageProps} />
}export default MyApp
```

## 结论

本文旨在对我们为什么使用 Next.js 以及如何使用它提供一个基本的理解。Next.js 的明星特性是它可以执行服务器端渲染和静态站点生成，但它的竞争对手如 Gatsby 只能执行静态站点生成。始终使用 Vercel 来部署 Next.js 应用程序，因为它提供了零配置部署和更快的性能。