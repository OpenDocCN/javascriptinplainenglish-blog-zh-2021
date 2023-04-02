# 如何在 Vue 3 中设置顺风 CSS

> 原文：<https://javascript.plainenglish.io/how-to-setup-tailwind-css-in-vue-3-405c889842d9?source=collection_archive---------1----------------------->

## 如果你这么讨厌文档，这是一个精简的演练。

![](img/ee7ce0ddeeb3e223e75ba721ada6ef23.png)

[顺风社的 CSS](https://medium.com/u/d8c8c34e2236?source=post_page-----405c889842d9--------------------------------) 是这个街区最新最酷的孩子之一。作为一个实用程序库，Tailwind 让您可以轻松地构建 UI 组件。这里有一个在你的 Vue 3 项目中设置顺风的快速指南。

> 嘶！在顺风文档中有一个官方的演练，[在这里](https://tailwindcss.com/docs/guides/vue-3-vite)。

首先，使用 [vue-cli](https://cli.vuejs.org/) 生成一个 Vue 3 项目:

```
vue create my-awesome-app
```

导航到项目目录:

```
cd my-awesome-app
```

接下来，我们需要安装 tailwind 及其依赖项(PostCSS & auto-prefixer)。

```
npm install -D tailwindcss@latest postcss@latest autoprefixer@latest
```

或者使用纱线:

```
yarn add --dev tailwindcss@latest postcss@latest autoprefixer@latest
```

注意:如果您遇到此错误:

> `Error: PostCSS plugin tailwindcss requires PostCSS 8.`

您需要安装一个支持 PostCSS 7 的不同版本的 tailwind。

```
npm uninstall tailwindcss postcss autoprefixernpm install -D tailwindcss@npm:@tailwindcss/postcss7-compat @tailwindcss/postcss7-compat postcss@^7 autoprefixer@^9
```

生成 Tailwind 和 post CSS 配置文件。

```
npx tailwindcss init -p
```

这将在你的根目录下创建两个文件: **tailwind.config.js** 和 **postcss.config.js** 。顺风配置文件是你为你的应用添加定制和主题的地方。它也是告诉 tailwind 搜索页面和组件的路径的地方。它看起来像这样:

```
// tailwind.config.js
module.exports = {
  purge: [],
  darkMode: false, // or 'media' or 'class'
  theme: {
    extend: {},
  },
  variants: {
    extend: {},
  },
  plugins: [],
}
```

我们不会深入解释每一个属性，但是，我们需要更新“purge”属性以包含组件和页面的路径。

```
// tailwind.config.js
  module.exports = {
    purge: ['./index.html', './src/**/*.{vue,js,ts,jsx,tsx}'],
    darkMode: false, // or 'media' or 'class'
    theme: {
      extend: {},
    },
    variants: {
      extend: {},
    },
    plugins: [],
  }
```

接下来，创建一个名为“styles”的文件夹，并在该文件夹中创建一个条目 CSS 文件(app.css):

```
mkdir src/styles && touch src/styles/app.css
```

我们将在入口 CSS 文件中使用`@tailwind`指令导入 tailwind 的样式。

```
/* ./src/styles/app.css */
@tailwind base;
@tailwind components;
@tailwind utilities;
```

最后，在条目 Javascript 文件(main.js)中导入条目 CSS 文件:

```
import { createApp } from 'vue';import App from './App.vue';import './styles/app.css'; // HerecreateApp(App).mount('#app');
```

启动你的服务器，开始在你的 Vue 3 应用中使用 Tailwind 的优点。尝试像这样更新 **App.vue** 组件:

```
<template> <div *class*="justify-center flex bg-yellow-300 items-center h-screen"> <div *class*="text-4xl"> Hello 👋🏼 </div> </div></template><script>export default { name: 'App',};</script>
```

你会得到这样的结果:

![](img/d7e2e84cf6090b7e817415c920d88970.png)

你可以在[官方文档](https://tailwindcss.com/docs)中找到 Tailwind 的所有类和选项。

[](https://tailwindcss.com/docs) [## 文档-顺风 CSS

### 顺风 CSS 框架的文档。

tailwindcss.com](https://tailwindcss.com/docs) 

本演练也是根据官方文档简化的:

[](https://tailwindcss.com/docs/guides/vue-3-vite) [## 安装带 Vue 3 的顺风 CSS 和 Vite - Tailwind CSS

### 如果你还没有建立一个新的 Vite 项目，开始创建一个。接下来，安装 Vite 的前端依赖项…

tailwindcss.com](https://tailwindcss.com/docs/guides/vue-3-vite) 

干杯☕️

> [**在黑暗模式下阅读本文**](https://devjavu.space/post/how-to-setup-tailwind-css-in-vue-3?isDark=true) 🌙，轻松复制并粘贴代码示例，并在 [**Devjavu**](https://devjavu.space/) 上发现更多类似的内容。

*更多内容请看*[***plain English . io***](http://plainenglish.io)