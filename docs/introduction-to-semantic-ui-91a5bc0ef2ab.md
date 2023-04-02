# 语义用户界面简介

> 原文：<https://javascript.plainenglish.io/introduction-to-semantic-ui-91a5bc0ef2ab?source=collection_archive---------5----------------------->

下一个 web 前端项目的另一个库

![](img/60f03465c661926b29a0ac8130f38ee3.png)

[website](http://ihatereading.in)

## 在后台

故事开始于我们为我们的网站创建一个介绍性的回购部分( [iHateReading](http://ihatereading.in) )。我们的目标是为我们的介绍库和架构提供一个单一的市场。

今天的故事将完成同样的任务，为语义 UI 库提供一个入门库。

## 概观

我不会花太多时间提供太多关于语义 UI 的信息。你可以通过下面的链接阅读我们的文档。

```
[https://semantic-ui.com/](https://semantic-ui.com/)
```

语义 UI 就像顺风 CSS 或者 bootstrap。它们用 CSS 提供组件类名，以相应地设计组件的样式。

如果你是内联 CSS 的粉丝，那么语义 UI 可能适合你，否则，如果你喜欢在 JSX 使用组件和 CSS，那么我的朋友可以试着阅读我的另一个关于材质 UI 或 React Bootstrap 的故事。

## 入门指南

您会惊讶地发现，在下一个 js 或 react 项目中安装语义 UI 只是一个两步过程。

*   第一步也是最重要的一步是安装所需的软件包
*   导入语义 UI 提供的所有 CSS 类。

```
yarn add semantic-ui-css
```

一旦安装了这个包，pages 目录中的内部`_app.js`文件将添加下面一行，为您导入所有的 CSS 类。

```
import 'semantic-ui-css/semantic.min.css';
```

完成安装步骤后，您现在需要做的就是使用 create components。

## 创建组件

**创建按钮**

```
<div *className*="ui segment">
  <button *class*="ui button">
    Button
  </button>
</div>
```

## 创建输入

```
<div *class*="ui left icon input loading">
  <input *type*="text" *placeholder*="Search..." />
  <i *class*="search icon"></i>
</div>
```

**创建卡片**

```
<div *class*="ui card four wide column">
 <div *class*="image">
  <img *src*="https://picsum.photos/200/300" />
 </div>
 <div *class*="content">
  <a *class*="header">Kristy</a>
 <div *class*="meta">
 <span *class*="date">Joined in 2013</span>
</div>
 <div *class*="description">
   Kristy is an art director living in New York.
 </div>
</div>
<div *class*="extra content">
 <a> <i *class*="user icon"></i>22 Friends</a>
</div>
</div>
```

## 结论

今天的故事到此结束，你可以在下面的链接中找到知识库。敬请关注，别忘了订阅。下次再见，祝大家愉快。

```
[http://ihatereading.in/createrepo?framework=Miscelleneous&repoId=-MqemZX-Vl91KVq0Y7qs](http://localhost:4001/createrepo?framework=Miscelleneous&repoId=-MqemZX-Vl91KVq0Y7qs)
```

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。在我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *获得独家获取写作机会和建议。***