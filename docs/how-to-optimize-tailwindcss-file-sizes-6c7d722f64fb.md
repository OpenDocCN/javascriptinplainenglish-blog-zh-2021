# 如何优化 TailwindCSS 文件大小

> 原文：<https://javascript.plainenglish.io/how-to-optimize-tailwindcss-file-sizes-6c7d722f64fb?source=collection_archive---------12----------------------->

## *如果你不用所有的工具，你就不需要它们*

![](img/da3ec0b596ce44f3cbdcf2217568265e.png)

Photo by [𝓜o k a](https://unsplash.com/@bekoz?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/bird-flying?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

TailwindCSS 是一个非常流行的基于实用程序类的样式库，用于快速创建视觉上令人惊叹的原型或生产网站和 web 应用程序。它有一个缺点[(已经在慢慢修复)](https://www.youtube.com/watch?v=3O_3X7InOw8)，那就是它的文件大小。

Tailwind 拥有从零宽度边距到 flex fox 控件以及一系列颜色的 CSS 类。如你所料，这将大大增加 CSS 文件的大小。但值得庆幸的是，Tailwind 的创造者让我们可以轻松地删除所有未使用的类以进行生产。

根据自己的[文档](https://tailwindcss.com/docs/optimizing-for-production)显示，Tailwind 的一个默认开发配置大概有 3739Kb 大，在开发阶段没什么危害，但是在制作阶段对于 SEO 和 UX 来说就恐怖了。

当使用 Brotli 进行 gzip 或压缩时，它可以更小，只有 71Kb。但这是一个完整的顺风文件，为了便于开发，它被设计得很大。在生产中，我们希望将它变得更小，并删除所有我们不使用的资源。

# 采购

Tailwind 使用 PurgeCSS 作为减少生产文件大小的方法之一。它会读取你的代码，检查 CSS 文件并删除任何它看不到的东西。默认情况下，它将清除所有未使用的 Tailwind 类，以及任何其他未使用的并且包装在`@layer component{...}`指令中的类。

当你的`NODE_ENV`变量设置为`production`时，Tailwind 会自动这样做。也可以通过设置`tailwind.config.js`文件中的变量来手动启用。

```
// tailwind.config.js
module.exports = {
  purge: {
    enabled: true,
    content: ['./src/**/*.html'],
  },
  // ...
}
```

*注意:PurgeCSS 通过读取您编写的实际代码来工作。当您使用字符串连接作为类名时，它将无法正常工作。*

```
// Won't work
<div class="text-{{  error  ?  'red'  :  'green'  }}-600"></div>// Will work
<div class="{{  error  ?  'text-red-600'  :  'text-green-600'  }}"></div>
```

# 结论

我希望这能帮助一些担心文件大小的开发者。**如果配置得当，** **Tailwind 文件不会包含任何你不需要的东西。根据我最近所听到的，这是一些人对像 Tailwind 这样的库的担忧。**

感谢您的阅读，祝您度过美好的一天。

*阅读更多来自 M. Vissers 的文章:*

[](https://betterprogramming.pub/templating-languages-to-use-instead-of-html-eb3682443958) [## 5 种替代 HTML 的模板语言

### 不要重复自己。请改用模板

better 编程. pub](https://betterprogramming.pub/templating-languages-to-use-instead-of-html-eb3682443958) [](https://betterprogramming.pub/making-beautiful-charts-with-chartjs-46a045465c24) [## 用图表制作漂亮的图表

### 简单灵活的 JavaScript 图表

better 编程. pub](https://betterprogramming.pub/making-beautiful-charts-with-chartjs-46a045465c24)