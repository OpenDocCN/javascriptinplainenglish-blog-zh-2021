# 电子和打字稿:如何使用 ipcMain 和 ipcRenderer

> 原文：<https://javascript.plainenglish.io/electron-and-typescript-how-to-use-ipcmain-and-ipcrenderer-english-4ebd4addf8e5?source=collection_archive---------5----------------------->

![](img/14f286996e27c2578c962ce75f5217b9.png)

Photo by [JJ Ying](https://unsplash.com/@jjying?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/@jjying?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在玩电子、打字稿和电子的时候，我遇到了一些问题。在我的模板的第一个版本中([El 3um 4s/memento-svelte-electronic-typescript](https://github.com/el3um4s/memento-svelte-electron-typescript))，我满足于一个工作结果。但这不是最好的结果。然后我通过做一些改进修改了代码。我不知道我的提议是否是最佳解决方案，但可以肯定的是，与第一个版本相比，我更喜欢它。

在第一个版本中，有一些主要的问题。一个在纤薄侧(我在本文最后讲到)，两个在电子侧。简而言之，Electron 的所有逻辑都被压缩到两个大文件中，`index.ts`和`preload.ts`。更重要的是，逻辑是复杂的。我使用`preload.ts`来确保苗条和电子之间的接口，但是功能在另一个文件中。另一方面，index.ts 发现自己必须管理图形界面的创建以及与 Svelte 之间的所有通信。

# 文件夹结构

在一个小项目中，比如我上传的存储库，这没什么大不了的。但是增加整体的复杂性并创建一个好的*意大利面条代码*并不需要很长时间。所以我决定后退一步，让一切更加模块化。我不止创建了两个文件，还创建了几个文件，每个文件都有一个要执行的任务:

```
> src
  > frontend
  > electron
    - index.ts
    - mainWindow.ts
    - preload.ts
    > IPC
      - systemInfo.ts
      - updateInfo.ts
      > General
        - channelsInterface.ts
        - contextBridge.ts
        - IPC.ts
```

如果乍一看，这似乎不合理地增加了项目的复杂性，我认为这是值得的:

*   `index.ts`继续作为主文件，但只负责调用必要的函数，而不是定义它们
*   `preload.ts`继续允许`BrowserWindow`和电子之间的安全通信，但仅包含可用信道列表
*   `mainWindow.ts`包含一个`Main`类来构建一个`BrowserWindow`中的电子

# `Main`类

保持`Main`类的独立允许我保持`index.ts`内的代码更干净。

首先，我需要一些基本设置的默认值和一个构造函数

然后我需要一个方法来创建主程序窗口

然后是一些额外的方法:

现在我把它们放在构造函数中:

如果我愿意，我可以停在这里。但是我还需要一样东西来截取窗口创建的时刻。我可以在`index.ts`或`Main`类本身中使用一个`app.on("browser-window-created", funct )`事件。相反，我更喜欢使用自定义的`EventEmitter` ( [链接](https://nodejs.org/api/events.html#events_class_eventemitter)):

最后，我导出了`Main`类以便我可以使用它:

在移动到`IPC`文件夹之前，我使用了`index.ts`中的`Main`类

我已经插入了`main.onEvent.on("window-created", funct)`:我将用它来定义启动时要执行的动作。那是链接到`ipcMain`、`webContents`和`autoUpdater`的代码。我将代码放在两个不同的文件中，`systemInfo.ts`和`updateInfo.ts`。这只是如何使用模板的两个例子，可以随意替换、删除或修改。当然，你可以以它们为基础添加其他功能和频道。

# 通道接口、上下文桥和 IPC

通用文件夹中的文件用于保持以前文件的整洁。

`channelsInterface.ts`包含一些接口的定义:

主文件是`IPC.ts`。`IPC`类是电子和 HTML 页面之间进程间通信的基础；

`IPC`有三个属性。`nameAPI`用于定义用于从前端调用 API 的名称。然后是有效频道列表。

与第一个版本相比，通向电子的通道不仅仅是一列名字，而是一个对象。我给每个键分配一个要调用的函数(我一会儿会解释)。只有两种方法，`get channels`和`initIpcMain`——我一会儿就用。

第三个*通用*文件包含了`generateContextBridge()`功能的定义。它接受一个类型为`IPC`的对象数组作为参数，并使用它们来生成电子和 Svelte 之间通信的安全通道列表。

我的解释可能相当混乱，但幸运的是这些文件不应该被改变。

# systemInfo.ts

此外，了解如何使用它们更有趣。这就是为什么我包括两个例子。我先说最简单的，`systemInfo.ts`。这个模块有一个单一的开放通道进出，并使用它来询问和获得一些关于电子，节点和铬的信息。

首先，我导入我刚才提到的文件:

所以我开始创建一些支持变量:

然后我创建一个`requestSystemInfo()`函数来调用。该名称不必与开放频道名称相同:

最后，我创建一个常量来导出:

之后，我需要在`preload.ts`注册频道。我只要写下:

然后我把必要的功能放在`index.ts`

# updaterInfo.ts

现在事情变得有点复杂了。我重新构建了自动更新应用程序的函数，同时将所有代码保存在`updaterInfo.ts`文件中。

所以我从创建一些支持常数开始:

在创建一个类`IPC`的对象之前，我停了一会儿，决定扩展基类。为什么？因为我必须单独声明与`autoUpdater`相关的操作。

一会儿我将展示在这个方法中插入什么，但同时，我可以创建要导出的常量:

现在我通过`validSendChannel`定义注册通道调用的函数

这些函数调用产生事件的`autoUpdater`。所以我创建了一个函数来拦截和管理这些事件:

然后，通过这个函数，我完成了`UpdaterInfo`类中的方法:

# 索引和预加载

完成`updaterInfo.ts`后，我终于完成了`preload.ts`文件:

此外，我拥有完成`index.ts`所需的所有元素:

就这样，我结束了电子部分。

# 苗条的

苗条的一面只剩下两件事要做。在第一个版本中，我在`dist/www`文件夹中插入了`index.html`、`global.css`和`favicon.png`文件。然而，将 dist 文件夹专门用于 Svelte 和 TypeScript 生成的文件更有意义。我将这三个文件移动到`src/frontend/www`文件夹:

```
> src
    > electron
    > frontend
        - App.svelte
        - global.d.ts
        - main.ts
        - tsconfig.json
        > Components
            - InfoElectron.svelte
            - Version.svelte
        > www
            - favicon.png
            - global.css
            - index.html
```

然而，问题是在编译时在`dist/www`中复制这些文件。幸运的是，您可以使用 [rollup-plugin-copy](https://www.npmjs.com/package/rollup-plugin-copy) 来自动完成这项工作。

在命令行中:

```
npm i rollup-plugin-copy
```

然后我编辑`rollup.config.js`文件，添加:

最后，我更新了苗条组件调用的函数

`InfoElectron.svelte`

成为

我用类似的方法修改`Version.svelte`里面的函数:`globalThis.api.send(...)`和`globalThis.api.receive(...)`变成`globalThis.api.updaterInfo.send(...)`和`globalThis.api.updaterInfo.receive(...)`。

今天到此为止。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) [](https://github.com/el3um4s/memento-svelte-electron-typescript) [## GitHub-El 3um 4s/memento-svelte-electronic-typescript:使用 Svelte 创建桌面应用程序的模板…

### 模板创建一个桌面应用程序与苗条，TailwindCSS，电子和打字稿(与电子更新…

github.com](https://github.com/el3um4s/memento-svelte-electron-typescript) 

*原载于 2021 年 7 月 9 日*[*https://blog.stranianelli.com*](https://blog.stranianelli.com/electron-ipcmain-ipcrenderer-typescript-english/)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)***。*** *报名参加我们的**[***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****