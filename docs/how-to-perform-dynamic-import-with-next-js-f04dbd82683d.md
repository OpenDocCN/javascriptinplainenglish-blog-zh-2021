# 如何用 Next.js 进行动态导入

> 原文：<https://javascript.plainenglish.io/how-to-perform-dynamic-import-with-next-js-f04dbd82683d?source=collection_archive---------5----------------------->

![](img/af60091a3110adb50c43ce90d64a9461.png)

通常，不可能根据条件导入模块。每当加载一个页面时，该特定页面上所有导入的模块也会被加载。

```
const allowImport = true;
if (allowImport) {
  import DynamicComponent from "../components/hello";
}export default function Home() {
  return (
    <div>
      <DynamicComponent />
    </div>
  )
}
```

上面的代码片段在编译时会产生一些错误。但是使用 Next.js，在动态导入的帮助下，可以根据条件加载模块。我们必须导入模块“next/dynamic”来执行动态导入。

```
import dynamic from 'next/dynamic'
const allowImport = true;
let DynamicComponent = null;
if (allowImport) {
  DynamicComponent = dynamic(() => import('../components/hello'))
}export default function Home() {
  return (
    <div>
      <DynamicComponent />
    </div>
  )
}
```

即使导入的模块不是默认的导出，我们也可以进行动态导入。

```
import dynamic from 'next/dynamic'

const DynamicComponent = dynamic(() =>
  import('../components/hello').then((mod) => mod.Hello)
)

function Home() {
  return (
    <div>
      <DynamicComponent />
    </div>
  )
}

export default Home
```

在 Next.js 中，HTML 在服务器端生成。因此，当一个特定的模块需要一个只能在浏览器中运行的库时，就会中断代码编译。使用动态导入，我们可以只在浏览器端加载特定的模块。

```
import dynamic from 'next/dynamic'

const DynamicComponentWithNoSSR = dynamic(
  () => import('../components/hello'),
  { ssr: false }
)

function Home() {
  return (
    <div>
      <DynamicComponentWithNoSSR />
    </div>
  )
}

export default Home
```

# 结论

动态导入也被用来提高网站性能，因为我们可以在初始页面加载时停止加载所有文件。但是如果你不正确地使用这个特性，它也会影响网站的性能。