# 如何将 150K LOC 代码库迁移到 Vite 和 ESBuild？(第 2/3 部分)

> 原文：<https://javascript.plainenglish.io/migrating-a-150k-loc-codebase-to-vite-and-esbuild-how-part-2-3-91b0b873f388?source=collection_archive---------0----------------------->

将我们的代码库迁移到 Vite 背后的细致工作，有助于尽快失败或以最辉煌的方式成功。

这是关于将 React+TypeScript 代码库从 Webpack 迁移到 Vite 的三篇文章系列的一部分。[第 1 部分](https://noriste.medium.com/migrating-a-150k-loc-codebase-to-vite-and-esbuild-why-part-1-3-4ccd9bea2a61)是关于我们为什么决定迁移，[第 3 部分](https://noriste.medium.com/migrating-a-150k-loc-codebase-to-vite-and-esbuild-is-it-worthwhile-part-3-3-5a12894bac96)是关于事后的考虑。

![](img/bcb10b44d9c861d20ffd53f0809f90b7.png)

# 迁移代码库

我可以用以下步骤来总结迁移:

1.  **兼容性**:包括研究 Vite，使用它，以及在实际代码库之外模拟我们的场景。
2.  可行性:我们的项目在 Vite 下工作吗？让我们以最快的方式迁移代码库。
3.  **标杆**:Vite 值得吗？我们早期的假设正确吗？
4.  **再现性**:重复迁移，而不弄乱代码库，减少所需的变更。
5.  **稳定性**:确保 ESLint、TypeScript 和测试对 Vite 和 Webpack 的更新代码库感到满意。
6.  **自动化**:准备自动跳转到 Vite 所需的代码模块。
7.  **迁移**:收获前面步骤的好处。
8.  **收集反馈**:团队喜欢吗？一旦经常使用会有什么局限性？

在接下来的章节中，我将深化每一步。

# 1.和睦相处

可能是最简单的一步。Vite 的文档非常简洁明了，开始使用 Vite 不需要任何东西。我的目标是熟悉该工具，并检查 Vite 是否以及如何与我们项目的关键方面很好地配合，这些方面是:

*   具有自定义配置的类型脚本
*   打字稿别名
*   导入/导出类型
*   指定出口
*   出口总额
*   具有内部状态的 web workers
*   [Comlink](https://github.com/GoogleChromeLabs/comlink) (用于工人之间的交流)
*   快速刷新反应
*   构建项目
*   浏览器兼容性
*   React 17 的 JSX 变换兼容性

快速和肮脏，只是通过`npm init @vitejs/app`创建一个启动项目，试验它，用所有上述选项模拟一个场景，并玩它。

老实说，我以为会有更多的麻烦，但一切顺利。对 Vite 的第一个影响是非常积极的😊。

# 2.可行性

这一步只有一个明确的目标:**无论如何，将 Vite 添加到我们的代码库**。说真的，**不管我破不破 TypeScript，ESLint** ，。env 变量和测试，我只想知道是否有技术问题阻止我们将项目转移到 Vite。

这个疯狂而盲目的过程背后的原因不是以最优雅的方式成功，而是尽快失败。用最少的工作量，我必须知道我们是否可以将我们的项目移到 Vite。

甚至在阅读了 ESBuild 的文档后，对我们影响最大的变化是

*   向 TypeScript 配置中添加另外三个设置(影响大量导入并阻止使用枚举)

```
"isolatedModules": true,
"esModuleInterop": true,
"allowSyntheticDefaultImports": true
```

ESBuild 需要前两个。你可以在它的文档中找到原因。请记住，ESBuild 会删除类型批注，而不会对它们进行验证。不是强制性的，但允许我们保持代码库与 Vite 和 Webpack 兼容(稍后会详细介绍)

*   更新 TypeScript 的别名:不再有`@foo`别名，只有`/@foo`或`@/foo`，否则 [Vite 在 node_modules 目录](https://github.com/vitejs/vite/issues/279#issuecomment-636110354)中查找导入的别名。

```
resolve: {
  alias: {
    '@/defaultIntlV2Messages': '/locales/en/v2.json',
    '@/defaultIntlV3Messages': '/locales/en/v3.json',
    '@/components': '/src/components',
    '@/intl': '/src/intl/index.ts',
    '@/atoms': '/src/atoms/index.ts',
    '@/routing': '/src/routing/index.ts',
    // ...
  },
},
```

*   Vite 自动将 JSONs 转换成命名导出模块。考虑设置 [Vite 的 JSON.stringify](https://vitejs.dev/config/#json-stringify) 以防万一。

仅此而已。之后，我继续以最快的方式修复错误，唯一的目标是让代码库在 Vite 下工作。

最烦人的部分是新的 TypeScript 配置,因为它需要手动修改

*   重新导出我们之前没有迁移的类型(`export **type** { Props } from`而不是`export { Props } from`)
*   ESBuild 不支持枚举，用字符串联合替换它们(更新:`const enums`不支持，感谢 [Jakub 注意到它](https://dev.to/kubajastrz/comment/1f3ld))

然后

*   `import * as`代替`import`用于某些依赖关系
*   `import`代替`import * as`为静态资产

其他问题来自于仅由网络工作者使用的**依赖关系，因为:**

*   每当 Web Worker 导入一个依赖项时，Vite 都会优化它并重新加载页面。幸运的是，Vite 公开了一个`optimizeDeps`配置来处理这种情况，避免了重载循环。

```
optimizeDeps: {
  include: [
    'idb',
    'immer',
    'axios',
    // …
  ],
},
```

*   如果 Web Worker 在导入依赖项时出错，您就没有有意义的提示。这对我来说是一个巨大的痛苦，但是一旦发现[，Evan 很快就解决了。](https://github.com/vitejs/vite/issues/2219)

最后，几个小时后，我们的项目在 Vite 上运行了🎉它不关心我引入的肮脏和临时的攻击的数量(大约 40 次无序提交)，因为我现在 100%确定我们的项目完全兼容 Vite。

# 3.标杆管理

尽快达到这一步还有另一个好处:我们可以衡量表现来决定是继续 Vite 还是退出。

对我们来说 Vite 比 Webpack 快吗？这些是我早期的经验测量。

即使代码库增长了——我们正在将整个 25 万 LOC 项目迁移到一个全新的架构上——这些早期的测量证实了押注 Vite 是有意义的。

**注意**:我们想降低风险。Vite 吸引我们，Vite 更快，Vite 更现代…但是我们还不是专家。因此**我们保持了 Vite 和 Webpack 的兼容性。如果出现问题，我们可以随时使用 Webpack。**

# 4.再现性

可行性步骤的收获是代码库需要迁移到 Vite 的一系列改变。现在，我寻找自信:如果我从`master`分支开始，重新做同样的改变，一切都必须再次工作。这个阶段允许创建一个包含大约十个独立的显式提交的完美分支。显式提交允许**将我能在**`**master**`**上做的任何事情直接移动到基于 Webpack 的标准代码库中，以简化最终的迁移步骤。我说的是:**

*   **添加 **Vite 依赖项**:通过将它们移动到`master`，我可以在每周依赖项更新期间保持它们的更新(我们安装了`vite`、`@vitejs/plugin-react-refresh`和`vite-plugin-html`)**
*   **添加 **Vite 类型****
*   **用前述设置(`isolatedModules`、`esModuleInterop`、`allowSyntheticDefaultImports`)更新**类型脚本配置**，并相应地修改代码库**
*   **将我们的`static-assets`目录转换成 Vite 的`public`目录**

**一旦完成，启动和运行 Vite 的步骤就少了一个数量级。**

# **5.稳定性**

**因为大部分需要的修改已经在`master`上了，所以我可以专注于最精细的部分。这就是为什么现在是时候**

*   **修复 TypeScript(记住，不包括在 Vite 中)错误**
*   **修复 ESLint 错误**
*   **修复失败的测试(主要是由于失败的导入)**
*   **添加 Vite 的。环境文件**
*   **添加团队将用于启动 Vite、使用 Vite 构建项目、预览构建以及清除 Vite 缓存的脚本(参考:如果您使用 yarn 工作区，Vite 的缓存存储在本地 node_modules 中)**
*   **创建 HTML 模板**
*   **检查所有 Webpack 配置是否都有 Vite 副本**

**Env 变量和文件值得注意。我们的项目使用了一些基于`process.env`的变量，通过 Webpack 的 Define 插件进行估价。Vite 有相同的`define`选项，并有电池包括[。环境文件](https://vitejs.dev/guide/env-and-mode.html#env-files)。**

**我选择了:**

*   **对不依赖于本地/开发/生产环境的 env 变量使用`define`。一个例子**

```
define: {
  'process.env.uuiVersion': JSON.stringify(packageJson.version),
},
```

*   **支持其余的`import.meta`(Vite 存储环境变量的地方)。**

**根据我们支持 Webpack 和 Vite 的决定，我们最终得到了下面的类型定义(一个例子)**

```
declare namespace NodeJS {
  export interface ProcessEnv {
    DISABLE_SENTRY: boolean
  }
}
interface ImportMeta {
  env: {
    VITE_DISABLE_SENTRY: boolean
  }
}
```

**以及这个消耗 env 变量的类似弗兰肯斯坦的函数**

```
export function getEnvVariables() {
  switch (detectBundler()) {
    case 'vite':
      return {
        // [@ts](http://twitter.com/ts)-ignore
        DISABLE_SENTRY: import.meta.env.VITE_DISABLE_SENTRY,
      }
    case 'webpack':
      return {
        DISABLE_SENTRY: process.env.DISABLE_SENTRY,
      }
  }
}function detectBundler() {
  try {
    // [@ts](http://twitter.com/ts)-expect-error import.meta not allowed under webpack
    !!import.meta.env.MODE
    return 'vite'
  } catch {}
  return 'webpack'
}
```

**我不会说我喜欢上面的代码，但它是暂时的，仅限于少数情况。我们可以忍受。**

**这同样适用于导入 Web Worker 脚本**

```
export async function create() {
  switch (detectBundler()) {
    case 'vite':
      return createViteWorker()
    case 'webpack':
      return createWebpackWorker()
  }
}async function createViteWorker() {
  // TODO: the dynamic import can be replaced by a simpler, static
  // import ViteWorker from './store/store.web-worker.ts?worker'
  // once the double Webpack+Vite compatibility has been removed
  // [@ts](http://twitter.com/ts)-ignore
  const module = await import('./store/store.web-worker.ts?worker')
  const ViteWorker = module.default
  // [@ts](http://twitter.com/ts)-ignore
  return Comlink.wrap<uui.domain.api.Store>(ViteWorker())
}async function createWebpackWorker() {
  if (!process.env.serverDataWorker) {
    throw new Error('Missing `process.env.serverDataWorker`')
  }
  //@ts-ignore
  const worker = new Worker('store.web-worker.ts', {
    name: 'server-data',
  })
  return Comlink.wrap<uui.domain.api.Store>(worker)
}
```

**关于脚本:这里没有什么特别的，package.json 现在包括**

```
"ts:watch": "tsc -p ./tsconfig.json -w",// launches both Vite and TSC in parallel
"vite:start": "concurrently - names \"VITE,TSC\" -c \"bgMagenta.bold,bgBlue.bold\" \"yarn vite:dev\" \"yarn ts:watch\"","vite:dev": "yarn vite",
"vite:build": "yarn ts && vite build",
"vite:build:preview": "vite preview",
"vite:clearcache": "rimraf ./node_modules/.vite"
```

**最后但同样重要的是:我没能让 Vite 忽略 Webpack 的`*.tpl.html`文件。我最终移除了`html`扩展以避免 Vite 验证它们。**

# **6.自动化**

**由于前面的步骤，我可以用一些精选代码和一些正则表达式来迁移整个代码库。 [Codemod](https://github.com/facebook/codemod#:~:text=Fork%20189-,Codemod%20is%20a%20tool%2Flibrary%20to%20assist%20you%20with%20large,and%20released%20as%20open%20source.) 非常适合创建迁移脚本并以极快的速度运行 RegExps。**

**我创作了一个剧本**

*   **删除 node_modules 目录**
*   **通过 Codemod 更新 TypeScript 别名来转换代码**
*   **重新安装依赖项**
*   **承诺一切**

**注意**脚本必须是等幂的**——也就是说运行一次或多次会产生相同的结果——这在多次启动脚本并将其应用于`master`分支和打开的 PRs 时至关重要。**

**这是脚本的一小部分**

```
# replace aliases pointing to directories (idempotent codemod)codemod -m -d . - extensions ts,tsx - accept-all \
"'@(resources|components|features|journal)/" \
"'@/\1/" # replace assets imports (idempotent codemod)codemod -m -d ./app - extensions ts,tsx - accept-all 'import \* as(.*).(svg|png|jpg|jpeg|json)' 'import\1.\2' # update some imports (idempotent codemods)codemod -m -d . - extensions ts,tsx - accept-all 'import \* as tinycolor' 'import tinycolor'codemod -m -d . - extensions ts,tsx - accept-all 'import \* as classnames' 'import classnames'codemod -m -d ./apps/route-manager - extensions ts,tsx - accept-all 'import PIXI' 'import * as PIXI'
```

**[在这里](https://gist.github.com/NoriSte/0a138442e9c5a09ba469061325d3ca0a)你可以找到整个剧本。还是那句话:在最终迁移之前，您在`master`上包含的更改越多，效果就越好。**

# **7.移民**

**我设计了这个脚本来简化所有开放分支的迁移，但是我们选择关闭所有 PRs 并只在`master`上操作。**

**由于之前的许多尝试和对脚本的改进，迁移代码库只不过是挑选“特殊”提交并启动 Codemods。**

# **按下红色按钮**

**最后，花了 30 个小时玩 Vite，修复和完善，得到了回报:几分钟后，代码库在 Vite 和 Webpack 下都工作了！🎉🎉🎉**

**最终的 **vite.config.ts** 文件如下**

**请注意，这**

```
esbuild: { jsxInject: `import * as React from 'react'` }
```

**只有当你像我们一样已经[将你的代码库升级到新的 React 17 的 JSX 变换](https://reactjs.org/blog/2020/09/22/introducing-the-new-jsx-transform.html)时才有帮助。升级的要点是从 JSX/TSX 的文件中删除`import * as React from 'react'`。ESBuild 不支持新 JSX 变换，必须注入[React](https://github.com/evanw/esbuild/issues/334#issuecomment-760427837)。 [Vite 故意暴露](https://vitejs.dev/guide/features.html#jsx)T3。或者，Alec Larson 刚刚发布了 [vite-react-jsx](https://twitter.com/alecdotbiz/status/139655066421448295) ，它的效果非常好。**

**最后但同样重要的是:目前，我还不能利用 [vite-tsconfig-paths](https://github.com/aleclarson/vite-tsconfig-paths#readme) 来避免在 vite 的配置中硬编码 TypeScript 别名，因为在我们也支持 Webpack 之前，路径中“public”的存在会让 Vite 抱怨**

```
// Webpack version:
"@/defaultIntlV2Messages": ["./apps/route-manager/public/locales/en/v2.json"]// Vite version:
'@/defaultIntlV2Messages': '/locales/en/v2.json'
```

## **柏树试验**

**无关但有用:如果你的代码库中有基于 Cypress 的组件测试，你可以毫无问题地跳到 Vite 上，看看我的这篇推文[我解释了如何做。](https://twitter.com/NoriSte/status/1383721527347056643)**

# **基准和结论**

**最终的基准测试证实了 Vite 的整体速度**

**这种比较是无情的，但公平吗？不算是。Vite 的表现优于 Webpack，但是，如前所述，我们在 Webpack 内部运行 TypeScript 和 ESLint，而 Vite 不允许我们这样做。**

**Webpack 在较轻的配置下表现如何？我们能在没有 Vite 的情况下利用 ESBuild 的速度吗？哪一个能提供最好的开发者体验？我在[第三部分](https://noriste.medium.com/migrating-a-150k-loc-codebase-to-vite-and-esbuild-is-it-worthwhile-part-3-3-5a12894bac96)中回答了这些问题。**

**嗨！我是斯特凡诺·马尼，我是一个充满激情的**前端工程师**，一个**演讲者**和一个**讲师**。我作为高级前端工程师/团队领导为[工作波](https://www.workwave.com/)远程工作。**

**我喜欢创造高质量的产品，测试和自动化一切，学习和分享我的知识，帮助别人，在会议上发言，面对新的挑战。**

**你可以在 [Twitter](https://twitter.com/NoriSte?source=post_page---------------------------) 、 [GitHub](https://github.com/NoriSte?source=post_page---------------------------) 、 [LinkedIn](https://www.linkedin.com/in/noriste/?source=post_page---------------------------) 上找到我。你可以找到我最近所有的投稿/演讲等。关于[我的 GitHub 总结](https://github.com/NoriSte/all-my-contributions)。**

***更多内容请看*[*plain English . io*](http://plainenglish.io/)**