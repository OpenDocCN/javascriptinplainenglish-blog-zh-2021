# 苗条框架指南

> 原文：<https://javascript.plainenglish.io/a-guide-to-the-svelte-framework-62d7084eccbd?source=collection_archive---------19----------------------->

## 苗条的框架，它的用途，以及它与其他框架的区别。

![](img/9aa8e80382a2d846f45da535c71bfabc.png)

Photo by [Ferenc Almasi](https://unsplash.com/@flowforfrank?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Svelte 是一个前端编程和设计的框架，有点类似于 Vue.js 和 React。但是苗条不仅仅是一个框架；它也是一个基于 HTML、CSS 和 JavaScript 的编译器和库。

与其他依赖虚拟 DOM 的框架相比，通过 Svelte，我们可以在编写完代码后进行编译，编译器会将我们编写的代码转换为 JavaScript 文件。这个文件具有很高的性能和速度，并且删除了我们在项目中没有使用的库和包。因此，它为您提供了一个轻量级的 JavaScript 代码，它的大小很小，并且它只包含运行站点所必需的代码，不像其他框架那样为我们生成一个文件，它的大小有点大，并且包含我们下载的所有包，尽管我们在项目中没有使用它们。

Svelte 文件有一个扩展名，每个文件由 3 个部分组成，分别是 HTML、CSS 和 JavaScript。它们不是必需的，只是可选的。例如，我们将尝试用 Svelte 制作一个简单的程序，在 HTML 部分:

```
<h1>Hello { name }</h1>
<input bind:value={ name }>
```

在这个程序中，我们想在输入中输入一个名字，它给我们一个欢迎这个名字的句子。例如，我们将输入 Adam，它会给出:*你好 Adam。*我们可以通过绑定很容易地做到这一点，由 Svelte 提供，这样我们前面的`bind:`属性的值和属性变量的值是相同的。我们可以为欢迎消息添加 CSS 格式:

```
<style>h1 {color: pink}</style>
```

对于 CSS，你可以把它写在同一个 Svelte 文件中，它只控制局部元素，或者做一个全局文件，把它和所有的 Svelte 文件链接起来，控制所有的元素。

要下载 Svelte，首先，我们可以通过 npm 或者通过 yarn 下载。这里我们将通过 npm 下载它。要使用 npm，有必要下载 Node.js，我们还需要 degit 工具，我们将从该工具克隆 Github 中的现有项目。

```
npm install -g degit
```

下载 degit 后，我们将使用 Github 中已经存在的模板，这样我们就不必创建项目文件并手动链接它们:

```
npx degit sveltejs/template my-svelte-project
```

在这里，一个名为 my-svelte-project 的项目将在您放置它的路径中为我们创建，然后我们将进入该项目:

```
cd my-svelte-project
```

这里，项目附带了一个 package.json 文件，该文件带有 devDependencies，但没有 node_modules，让我们下载它并执行以下代码:

```
npm install
```

在这里，项目的 node_modules 文件将递增，我们将在 localhost 中使用以下命令执行项目:

```
npm run dev
```

它告诉你必须在本地主机中打开文件，它会给你一个端口，可能是: [http://localhost:5000](http://localhost:5000)

在浏览器中解决这个链接，项目就可以工作了。

> 我们将在另一篇文章中见面，
> 
> 感谢阅读

*更多内容看*[***plain English . io***](http://plainenglish.io/)