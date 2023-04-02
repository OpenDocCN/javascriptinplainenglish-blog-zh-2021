# 如何在 Next.js 中使用 Markdown/MDX

> 原文：<https://javascript.plainenglish.io/how-to-use-markdown-with-next-js-733b75364eba?source=collection_archive---------16----------------------->

如果你想为博客、文档或静态页面制作一个网站，你可能会考虑使用 Markdown。 [Markdown](https://www.markdownguide.org/) 允许你将明文转换成 HTML 标签。大多数开发人员都熟悉 Markdown。

![](img/0ad83b8088e0fa17c1ee5601eca168ad.png)

Photo by [Roman Synkevych](https://unsplash.com/@synkevych?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你想优化写作，花更少的时间在编码上。假设您必须为一个静态页面编写这样的代码。没有问题，如果内容短，但如果长，我认为最好使用降价。而不是像这样写 HTML:

```
<p>
  <strong>I am</strong> using <a href="https://nextjs.org/">Next.js</a>
</p>
```

相反，您可以使用 Markdown 来表达您的风格:

```
**I love** using [Next.js](https://nextjs.org/)
```

接下来，Js 有 3 种方法将 Markdown 转换为 page:

*   使用**备注**和**备注-html** 。
*   使用 **next-mdx-remote**
*   使用 **@next/mdx**

# 1.使用备注和备注-html

```
npx create-next-app markdownyarn add remarkyarn add remark-html
```

创建文件夹源并存储文件**。md** 。更改 index.js:

```
import fs from "fs";import remark from "remark";import html from "remark-html";export default function Post({ contents }) {return <div dangerouslySetInnerHTML={{ __html: contents }} />;}export async function getStaticProps() {const content = await remark().use(html).process(fs.readFileSync("source/example.md"));return { props: { ...content } };}
```

您可以将此与 **getStaticProps** 、 **getStaticPaths** 、 **getServerSideProps** 一起使用。

# 2.使用 next-mdx-remote

```
npx create-next-app markdownyarn add next-mdx-remote
```

您可以像这样创建 **index.js** :

```
import renderToString from "next-mdx-remote/render-to-string";import hydrate from "next-mdx-remote/hydrate";export default function Post({ source }) {const content = hydrate(source);return <div className="wrapper">{content}</div>;}export async function getStaticProps() {// MDX text - can be from a local file, database, anywhereconst source = "Some **mdx** text";const mdxSource = await renderToString(source);return { props: { source: mdxSource } };}
```

源可以来自本地文件、数据库或任何地方。你可以用这个导入组件。创建一个组件，如下所示:

```
export default function Title() {return <div>Title Here</div>;}
```

并改 **index.js** 。

```
import renderToString from "next-mdx-remote/render-to-string";import hydrate from "next-mdx-remote/hydrate";import Title from "../components/title";const components = {Title,};export default function Post({ source }) {const content = hydrate(source, { components });return <div className="wrapper">{content}</div>;}export async function getStaticProps() {// MDX text - can be from a local file, database, anywhereconst source = "Some **mdx** text, with component <Title/>";const mdxSource = await renderToString(source, { components });return { props: { source: mdxSource } };}
```

组件也可以像普通一样使用道具。

```
import renderToString from "next-mdx-remote/render-to-string";import hydrate from "next-mdx-remote/hydrate";import Title from "../components/title";const components = {Title,};export default function Post({ source }) {const content = hydrate(source, { components });return <div className="wrapper">{content}</div>;}export async function getStaticProps() {// MDX text - can be from a local file, database, anywhereconst source = "Some **mdx** text, with component <Title value='example'/>";const mdxSource = await renderToString(source, { components });return { props: { source: mdxSource } };}
```

# 3.使用@next/mdx

我觉得比别人简单。可以用**。mdx** 并将索引改为它。

```
npx create-next-app markdownyarn add @next/mdxyarn add @mdx-js/loader
```

在我们更改 **index.js** 之前。我们必须创建 **next.config.js** 。

```
const withMDX = require("@next/mdx")();module.exports = withMDX({pageExtensions: ["js", "jsx", "mdx"],});
```

接下来，将 **index.js** 改为 **index.mdx** 。您可以将该文件用作普通降价。

```
I ****love**** using [Next.js](https://nextjs.org/)
```

但是，如果你想使用一个布局或者想要有一个元，你可以这样做。

```
import Layout from "../layouts/layout.js";export const meta = {title: "title example",};I ****love**** using [Next.js](https://nextjs.org/)export default ({ children }) => <Layout meta={meta}>{children}</Layout>;
```

可以直接使用 JS 对象。

所以对我来说，我喜欢用 **next-mdx-remote。我认为定制更灵活。你可以在这里克隆一个项目[。](https://github.com/jetlysandita/markdown)**

如果你知道任何其他方法，建议或问题，请在下面评论。谢谢:)