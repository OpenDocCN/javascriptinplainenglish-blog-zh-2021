# 如何用 Next.js 和 React 创建一个国际网站

> 原文：<https://javascript.plainenglish.io/how-to-create-an-international-website-with-next-js-and-react-hooks-14fec9c61fac?source=collection_archive---------7----------------------->

![](img/1b1fd968315441bac08e7a29ae1dc643.png)

Photo by [Soner Eker](https://unsplash.com/@sonereker?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

## 用一个简单的 React 自定义挂钩提供多语言网站

# 介绍

当使用 Next.js 创建网站时，你经常会遇到在网站上提供多种语言的问题，有时你会使用像 Strapi 这样的 CMS 来处理不同的语言输出。然而，在这种情况下，网站是静态的(不依赖于后端),文本直接存储在 HTML 中。

我提供的解决方案使用 Next.js 内置的 [i18n 工具](https://nextjs.org/docs/advanced-features/i18n-routing)，使用 JSON 或 MarkDown 文件，这些文件与为您处理不同语言输出的自定义 react 挂钩相结合。

我将首先解释如何准备您的文件夹和文件，然后如何添加不同语言的内容，然后如何创建和使用自定义挂钩，最后，我将简要解释如何在您的 UI 中更改区域设置。

# 1.准备网站

你应该做的第一件事是按照 Next.js [主页](https://nextjs.org/learn/basics/create-nextjs-app/setup)上精心制作的教程来设置你的 Next.js 应用。一旦你完成了，我们将开始修改你的应用程序根目录下的 **next.config.js** 文件。

根据你要添加到你的网站上的语言，你的文件看起来会和上面显示的有点不同。然而，过程将是相同的。在这个例子中，我将在默认的英语版本中添加法语和德语。

将 i18n 模块添加到您的文件中，插入区域设置，设置默认区域设置，然后选择“是”或“否”,您希望您的网站自动检测用户的语言。(如果您希望文件中的更改生效，请不要忘记重启您的应用程序)

```
module**.**exports **=** { reactStrictMode: true, i18n: {
      localeDetection: false,
      locales: ["fr", "en", "de"],
      defaultLocale: "fr",
   },}
```

next.config.js

一旦你这样做了，我们还将添加一个系统，我们的应用程序中的所有文件将更容易访问。为此，在应用程序目录的根目录下创建/修改 **jsconfig.json** 文件。(如果您希望文件中的更改生效，请不要忘记重启您的应用程序)

```
{
"compilerOptions": {
   "baseUrl": ".",
   "paths": {
      "@/components/*": ["components/*"],
      "@/styles/*": ["styles/*"],
      "@/context/*": ["context/*"],
      "@/locales/*": ["locales/*"],
      "@/pages/*": ["pages/*"],
      "@/public/*": ["public/*"],
   }
}
}
```

jsconfig.json

现在您已经完成了所有必要的修改，您将能够通过您的路由器对象访问区域数据。

# 2.开始添加您的内容

在开始添加内容之前，你需要了解如何添加内容。因为我们不会使用外部文本编辑器，所以我们会将网站的内容存储在 JavaScript 文件中，这些文件将根据当前活动的语言环境导入到组件中。

我将这些文件存储在我的应用程序根目录下的“locales”文件夹中，每页有 3 个文件(每页每种语言一个文件，在本例中是英语、法语和德语)。

my _ app/
├─locales/
│├─pages/
││├─home/
││├─en . js
││├─fr . js
││├─de . js
││├─about/
││├─contact/
│├─components/

每个文件具有相同的结构但有其他内容。

```
//en.jsexport default { 
   hero_text: "This is the HERO" 
}; //fr.jsexport default {
   hero_text: "Ceci est le HERO",
}; //de.jsexport default {
   hero_text: "Das is der HERO"
};
```

你可以对你网站的每个页面都这样做，如果你想添加 markdown，你也可以这样做(只要你使用 react-to-markdown 将 markdown 转换成 HTML)。

对于这个例子，我创建了一个简单的主页，其中的文本会根据当前使用的地区而改变。

```
**import** HomeStyle *from* "@/styles/Pages/Home/Home.module.scss";**import** { useLocales } *from* "@/components/hooks/useLocales"; export default *function* Home() {**const** text **=** useLocales("home");

   **return** (
      <> <main *className*={HomeStyle.container}> <h1>{text.hero_text}</h1> </main> </> );}
```

/pages/index.js

正如你所看到的，我已经实现了`useLocales`钩子，在下一节中，我将解释它是如何工作的以及它做了什么。

# 3.旋转木马钩

这个挂钩的目的是能够在每个组件中导入所需的语言文件，而不必在每个组件中单独导入每个文件，也不必为每个单独的文件创建条件逻辑。

在“components”文件夹中添加一个名为“hooks”的文件夹和一个名为 **useLocales.js** 的文件。

my _ app/
├─locales/
├─components/
│├─hooks/
│├─uselocales . js

在文件内部从 React 和 Next.js 导入`useState`、`useEffect`和`useRouter`

```
*import* { useState, useEffect } *from* "react";*import* { useRouter } *from* "next/router";
```

/components/hooks/useLocales.js

一旦你完成了这些，你可以继续创建`useLocales`箭头函数，析构区域设置，并用`useState`创建一个`text`状态变量。然后使用钩子将文本变量返回给组件。

```
export ***const*** useLocales **=** (path) *=>* {***const*** router **=** useRouter();
   ***const*** { locale } **=** router;***const*** [text, setText] **=** useState({});***return*** text;};
```

/components/hooks/useLocales.js

现在添加一个`useEffect`,它将确保组件被赋予正确的语言环境，并且只有在组件沿着路径传递的情况下。将区域设置作为参数添加将在每次区域设置更改时更改文本。有关动态导入的更多信息，请访问相关主题的 [Next.js 文档](https://nextjs.org/docs/advanced-features/dynamic-import)。*在这个例子中，你可以看到在第一部分配置路径的重要性，因为有了它，钩子在任何地方都可用*。

```
useEffect(() *=>* { if (path) {      import(`@/locales/pages/${path}/${locale}`)**.**then((t) *=>* {
         setText(t**.**default); });}
}, [locale]);
```

/components/hooks/useLocales.js

完成的钩子看起来像这样。

```
*import* { useState, useEffect } *from* "react";*import* { useRouter } *from* "next/router";export ***const*** useLocales **=** (path) *=>* { ***const*** router **=** useRouter();
   ***const*** { locale } **=** router; ***const*** [text, setText] **=** useState({}); useEffect(() *=>* { if (path) { import(`@/locales/pages/${path}/${locale}`)**.**then((t) *=>* {
         setText(t**.**default); }); }
   }, [locale]);***return*** text;};
```

/components/hooks/useLocales.js

# 4.如何使用钩子

回到 **index.js** 文件，您可以看到您可以使用简化的路径简单地导入钩子，然后提取`text`对象。然后，您可以通过析构您在 JavaScript 文件中编写的文本来使用对象。

```
***import*** HomeStyle *from* "@/styles/Pages/Home/Home.module.scss";
***import*** { useLocales } *from* "@/components/hooks/useLocales";export default *function* Home() { ***const*** text **=** useLocales("home");

   ***return*** (
      <> <main *className*={HomeStyle.container}> <h1>{text.hero_text}</h1> </main> </> );}
```

/pages/index.js

`useLocales`钩子自动检测当前区域设置的变化(您可以通过在 URL 的末尾添加“fr”或“de”来手动更改区域设置，例如:“localhost:3000/fr”)。

# 5.如何更改区域设置

现在你已经在你的网站上安装了你喜欢的语言环境，它们会自动切换，你需要能够在你的用户界面中切换它们。为此，您有两种解决方案:

**1。使用“链接”组件**

只需从“next/link”中导入“Link ”,并将其插入到您的代码中，用“href”参数链接到您想要的位置，用“locale”参数链接到您选择的区域(代码可在 nextjs.org 上找到)。

```
import Link from 'next/link'

export default function IndexPage(props) {
  **return** (
    <Link href="/another" locale="fr">
      <a>To /fr/another</a>
    </Link>
  )
}
```

**2。使用“下一个路由器”**

不用使用组件，您可以简单地从`next/router`导入路由器(就像我们之前做的那样)，并通过添加一个`locale`参数(代码可以在 nextjs.org 上找到)来使用`push`方法。

```
import { useRouter } from 'next/router'

export default function IndexPage(props) {
  const router = useRouter()

  return (
    <div
      onClick={() => {
        router.push('/another', '/another', { locale: 'fr' })
      }}
    >
      to /fr/another
    </div>
  )
}
```

有关如何操作的更多信息，请访问:[https://nextjs . org/docs/advanced-features/i18n-routing # transition-between-locales](https://nextjs.org/docs/advanced-features/i18n-routing#transition-between-locales)

您现在可以创建您的国际网站了！如果你对这个问题有任何疑问，请随时与我联系。反馈也总是受欢迎的！

## 来源

*   在[https://nextjs.org/docs/advanced-features/i18n-routing](https://nextjs.org/docs/advanced-features/i18n-routing)上找到的 i18n 个解释
*   如何在 react 网站的[https://reactjs.org/docs/hooks-custom.html](https://reactjs.org/docs/hooks-custom.html)下创建自定义 react 挂钩
*   图片来自 [Unsplash](https://unsplash.com/)
*   [碳](https://carbon.now.sh/)为代码嵌入

*更多内容请看*[***plain English . io***](http://plainenglish.io)