# 如何在顺风 CSS 中使用 Svelte

> 原文：<https://javascript.plainenglish.io/tailwind-css-svelte-315075404c04?source=collection_archive---------5----------------------->

![](img/7051ae4b72c033ad7c66c2f79b0f01d3.png)

Photo credit: Marek Piwnick

正如我几天前所说的，我决定专注于一些更复杂的项目。第一个是“GEST-Dashboard”。够难听的名字，不过以后我会改的。我需要一个在离线电脑上打开 web 应用程序的工具。在我的脑海中，每个 web 应用程序都是一个包含所有文件的文件夹。我会用电子结合苗条和顺风。我遇到了一些有趣的问题。其中之一就是如何将 TailwindCSS 与 Svelte 融合。

我在网上找到了一些教程，但是很多都过时了。有一个做得很好，由 [sarioglu](https://dev.to/sarioglu) : [使用带尾翼的苗条——一个更好的方法](https://dev.to/sarioglu/using-svelte-with-tailwindcss-a-better-approach-47ph)。也值得看一看[dionysiusmarquis/svelte-tailwind-template](https://github.com/dionysiusmarquis/svelte-tailwind-template)库。这些帖子让我很受启发。这些是我把苗条和顺风结合起来的步骤。

我从我的[纪念品——细长的电子打字稿](https://github.com/el3um4s/memento-svelte-electron-typescript)开始。

[](https://github.com/el3um4s/memento-svelte-electron-typescript) [## GitHub-El 3um 4s/memento-svelte-electronic-typescript:使用 Svelte 创建桌面应用程序的模板…

### 模板创建一个桌面应用程序与苗条，TailwindCSS，电子和打字稿(与电子更新…

github.com](https://github.com/el3um4s/memento-svelte-electron-typescript) 

首先，我检查自从我上次工作以来哪些包需要更新:

```
npm outdated
```

所以我更新了一切:

```
npm update
```

我想把所有东西都更新到最新版本(这有点冒险，我可能会不小心弄坏什么东西，也因为我还没有实现一个可靠的测试系统)。我用`npm install <packagename>@latest`

```
npm install @rollup/plugin-commonjs@latest @rollup/plugin-node-resolve@latest electron@latest electron-reload@latest
```

这会生成一些错误和警告:

```
src/electron/mainWindow.ts:38:9 - error TS2322: Type '{ enableRemoteModule: true; }' is not assignable to type 'WebPreferences'.
Object literal may only specify known properties, and 'enableRemoteModule' does not exist in type 'WebPreferences'.(node:15840) electron: The default of nativeWindowOpen is deprecated and will change from false to true in Electron 15
```

我通过改变`mainWindow.ts`模块来修复它:

现在是时候转到顺风了。我需要一些包裹。要启动 [TailwindCSS](https://tailwindcss.com/) :

```
npm i -D tailwindcss
```

然后要处理的事情 [PostCSS](https://github.com/postcss/postcss) :

```
npm i -D postcss postcss-load-config autoprefixer rollup-plugin-postcss
```

一旦完成，我开始配置该项目能够结合使用苗条和电子顺风。我需要另外两个文件:`tailwind.config.js`和`postcss.config.js`。我创造它们:

然后我必须配置 **rollup** 来管理 PostCSS 文件。我对`rollup.config.js`进行了修改，增加了:

这让我可以生成一个专用于 Tailwind 的`base.css`文件。我必须告诉`index.html`文件在哪里可以找到。所以我将这一行添加到主 html 文件中:

这个项目仍然缺少一样东西:某种风格的 TailwindCSS。我从创建一个`css/tailwind.pcss`文件开始。在编写图形组件时，我使用一个单独的文件来加速测试。

然后将文件导入`App.svelte`:

现在我可以使用 Tailwind 了，例如通过在链接中添加`btn-orange`类:

最后，到存储库的链接是[el3 um4s/memorial-SVE te-electronic-type script](https://github.com/el3um4s/memento-svelte-electron-typescript)。

[](https://github.com/el3um4s/memento-svelte-electron-typescript) [## git hub-El 3 um4s/memorial-svelte-e-type script:使用 SVE LTE 创建桌面应用程序的模板…

### 模板，以创建一个桌面应用程序与 Svelte，TailwindCSS，电子和类型脚本(与电子更新…

github.com](https://github.com/el3um4s/memento-svelte-electron-typescript) 

谢谢你的阅读！请继续关注更多信息。

***不要错过我的下一篇文章——注册我的*** [***中邮件列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 加入 Medium，加入我的推荐链接— Samuele

### 阅读萨缪尔(以及媒体上成千上万的其他作家)的每一个故事。不是中型会员？加入这里，分享…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原为发表于 2021 年 9 月 18 日*[*https://blog.stranianelli.com*](https://blog.stranianelli.com/tailwind-and-svelte-english/)*。*

*多内容见于* [*中。注册我们的*](http://plainenglish.io/) [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区不和*](https://discord.gg/GtDtUAvyhW) *中获得独家写作机会和建议。*