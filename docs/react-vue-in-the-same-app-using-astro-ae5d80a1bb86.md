# 使用 Astro 在同一个应用程序中做出反应

> 原文：<https://javascript.plainenglish.io/react-vue-in-the-same-app-using-astro-ae5d80a1bb86?source=collection_archive---------9----------------------->

*是的，有可能，有*[*Astro*](https://astro.build/)*和飞船🚀代码更少。*

![](img/bb30ac359900ce6769522bbc8cec526b.png)

Photo by [Graham Holtshausen](https://unsplash.com/@freedomstudios?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/galaxy?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

[Astro](https://astro.build/) 是市场上一款新的 JavaScript bundler。它遵循自带框架(BYOF)策略，按需加载组件。Astro 还在测试版(v0.19)。他们计划在今年晚些时候发布 1.0.0 版。保持警惕👀出去。

```
# create a new project mkdir js-is-one 
cd js-is-one # no other config is required, only this command is enough 🔥 
npm init astro -- --template framework-multiple # then install the dependencies 
npm i # start the dev server 
npm run dev
```

该命令将加载使用多个框架开发应用程序所需的所有配置— `npm init astro --template framework-multiple`

推荐最佳太空开发体验

1.  使用 VSCode 文本编辑器
2.  使用他们官方的 Astro [VSCode 扩展](https://marketplace.visualstudio.com/items?itemName=astro-build.astro-vscode)

# 文件夹结构

```
├── src/ 
│   ├── components/ 
│       └── ReactHW.jsx 
│       └── VueHW.vue 
│   └── pages/ 
│       └── index.astro 
├── public/ 
├── astro.config.mjs 
└── package.json
```

# `astro.config.mjs`

我们使用的模板`framework-multiple`默认加载所有的框架【反应，Vue，Preact，Svelte，Solid & Astro 也是如此】，Astro 框架有一个配置文件`astro.config.mjs`，所有的框架都可以在这里配置。我将删除其他框架，如 Preact，Svelte 和固体，只保留反应& Vue

```
export default {
  renderers: [
    "@astrojs/renderer-react",
    "@astrojs/renderer-vue"
  ],
};
```

# 索引. astro

```
---
// Component Imports
import * as react from '../components/ReactHW.jsx';
import VuewHW from '../components/VueHW.vue';<html lang="en">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" /> <link rel="icon" type="image/x-icon" href="/favicon.ico" /> <style>
        :global(:root) {
            font-family: system-ui;
            padding: 2em 0;
        }
    </style>
  </head>
  <body>
      <main>
        <react.HW client:visible>
            <h1>Hello React!</h1>
        </react.HW> <VuewHW client:visible>
            <h1>Hello Vue!</h1>
        </VuewHW>
      </main>
  </body>
</html>
```

所以 React 和 Vue 共存于同一个文件中。

我需要探索的是:

1.  使用相同的 CSS-in-JS 组件
2.  对 React 和 Vue 使用相同的棉绒
3.  为两个框架使用相同的插件，如`lodash`

# Astro 是关于部分水合的

默认情况下，Astro 用零客户端 JavaScript 生成每个网站。使用任何前端 UI 组件(React、Svelte、Vue 等。)Astro 会在构建时自动将其呈现为 HTML，并剥离所有 JavaScript。

部分水合意味着——在某些情况下，我们需要客户端 JS 来评估——像自动完成搜索栏、添加到购物车按钮等等。只对需要 JavaScript 的单个组件进行水合，而将站点的其余部分保持为静态 HTML 的行为称为部分水合。

我们可以控制组件的部分水合作用，并决定如何渲染组件——部分或全部。以下是一些例子👇

# `<Component client:load />`

这使得页面加载的组件更加水乳交融。

# `<Component client:idle />`

一旦主线程空闲，这就使组件水合

# `<Component client:visible />`

元素一进入视口，这就融合了组件(使用 [IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API) )。

# `<Component client:only />`

这在页面加载时使组件水合，类似于`client:load`。

# 开发模式

命令`npm run dev`将在浏览器中加载应用`[http://localhost:3000](http://localhost:3000)`

# 使用 Astro 的其他框架

对于一个带有您选择的框架的普通项目，我列出了下面的命令👇

1.  反应——`npm init astro -- --template framework-react`
2.  Vue — `npm init astro -- --template framework-vue`
3.  苗条— `npm init astro -- --template framework-svelte`

# Codesandbox 演示

*更多内容请看*[***plain English . io***](http://plainenglish.io/)