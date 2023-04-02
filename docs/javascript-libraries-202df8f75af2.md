# 5 个很少使用但很有帮助的 JavaScript 库

> 原文：<https://javascript.plainenglish.io/javascript-libraries-202df8f75af2?source=collection_archive---------17----------------------->

![](img/921c088fc16321c87c34c557caad4ee8.png)

Photo by [Christopher Gower](https://unsplash.com/@cgower?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 是最流行的编程语言之一。它是网络的编程语言，有许多可以执行的库和函数。在这里，我将谈论 5 个很少使用的库，以及它们在网站建设中的作用。

1.  **Stretchy.js**

```
<script src="[stretchy.min.js](https://projects.verou.me/stretchy/stretchy.min.js)" async></script>
```

Stretchy.js 是一个 JavaScript 库，有助于自动调整表单元素的大小。它还作为 API 添加到网站中，以执行各种功能。

2.**捷达网**

```
<html>
  <head>
    <script src="https://unpkg.com/jete@0.9.3/index.js" crossorigin></script>
    <script src="https://unpkg.com/jeti@0.7.2/index.js" crossorigin></script>
    <script type="application/jet">
      import {render} from 'jete';
      render(
        <span>Hello!</span>,
        document.getElementById('app')
      );
    </script>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

Jet.js 是一个用于构建 web 应用程序的库。它是一个具有本地浏览器内 JSX 支持的 React 替代产品。JSX 是 JavaScript 的超集，在 JavaScript 文件中包含 HTML 标签。

JSX 提供了一个简单的声明性标记。HTML 标签位于 JavaScript 组件内部，当每个组件拥有自己的 UI 表示时，它使得分离关注点成为可能。

3. **Nipple.js**

```
<script src="./dist/nipplejs.min.js"></script>
<script>
    var dynamic = nipplejs.create({
        zone: document.getElementById('dynamic'),
        color: 'blue'
    });
</script>
```

js 是一个用于为触摸界面创建虚拟操纵杆的库。它以三种类型进行测试——动态、半动态和静态。

4. **loadjs**

```
*// define a dependency bundle with advanced options*loadjs(['/path/to/foo.js', '/path/to/bar.js'], 'foobar', {before**:** function(path, scriptEl) { */* execute code before fetch */* },async**:** true,  *// load files synchronously or asynchronously (default: true)*numRetries**:** 3  *// see caveats about using numRetries with async:false (default: 0),*returnPromise**:** false  *// return Promise object (default: false)*});loadjs.ready('foobar', {success**:** function() { */* foo.js & bar.js loaded */* },error**:** function(depsNotFound) { */* foobar bundle load failed */* },});
```

Loadjs 是一个现代 JavaScript 的异步加载库，它与最新的 web 浏览器版本和搜索引擎兼容。

5. **Bootbox.js:**

```
bootbox.alert("Hello world!");
```

> js 是一个小的 JavaScript 库，它允许你使用 [Bootstrap modals](https://getbootstrap.com/docs/4.3/components/modal/) 创建可编程的对话框，而不必担心创建、管理或删除任何必需的 DOM 元素或 JavaScript 事件处理程序。

来源:[http://bootboxjs.com/](http://bootboxjs.com/)

它提供了三个函数:alert、confirm 和 prompt，目的是模仿它们的本地 JavaScript 等价物。

这些是 JavaScript 开发人员很少使用的 JavaScript 库，但它们对构建动态网站仍然很有用。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)*。报名参加我们的* [***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。查看我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *加入我们的* [***人才集体***](https://inplainenglish.pallet.com/talent/welcome) *。*