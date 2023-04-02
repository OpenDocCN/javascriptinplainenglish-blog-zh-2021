# 如何在 React 中创建页面加载动画加载器

> 原文：<https://javascript.plainenglish.io/how-to-create-a-page-load-animated-loader-in-react-793d42411fd5?source=collection_archive---------3----------------------->

![](img/62f73df7bc2689c34332e998bbf7aa59.png)

Create a react page load loader

我们将看到如何在页面加载时创建一个动画加载器。

基本上，它相当于 JavaScript 的`load`事件。当加载了整个页面，包括所有依赖的资源，如样式表和图像时，会触发`load`事件。

```
window.addEventListener('load', (event) => {
  console.log('page is fully loaded');
});
```

我们需要在`public`目录中的`index.html`文件中添加我们的**加载器** HTML 和 CSS。

由于反应应用程序安装在**根** div 中，所以我们需要在**根** div 中添加我们的加载器 HTML 部分。

然后，我们可以将 CSS 部分添加到同一个文件中，在`<style>`标签中。

就这样，它将为您的 React 应用程序创建一个页面加载器，只有当网站首次打开时才会出现。

它与我们在`React.lazy`和`Suspense`情况下使用的非常不同，因为它使用了`Suspense`的`fallback`属性，该属性在我们页面的**路线**每次改变时都可见，并且是一个新的**路线**。

应用程序的源代码— [反应-页面加载器](https://github.com/GermaVinsmoke/react-page-loader)。

*更内容见于* [***中***](http://plainenglish.io/)