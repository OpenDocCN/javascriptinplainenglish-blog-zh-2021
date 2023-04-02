# 如何构建一个普通的 JavaScript 架子鼓

> 原文：<https://javascript.plainenglish.io/how-to-build-a-vanilla-javascript-drum-kit-23cab75b1ebc?source=collection_archive---------10----------------------->

## 了解如何使用普通 JavaScript 创建架子鼓

![](img/f47280107b58bc431a8097fe53ff5539.png)

Image by Cottonbro from Pexels

JavaScript 是一种非常通用和强大的语言，可以用来构建各种语言。在本文中，我们将构建一个类似于鼓形钻头的项目。

我们不会为此使用任何库或包，因为我们将用普通的 JavaScript 来构建它。

## **入门**

我们将有一个不同的数字键盘数字布局。当用户按下其中一个键时，我们将播放一些声音。

**你将学到什么**

*   DOM 操作
*   事件监听器
*   在 JavaScript 中处理音频

## **设置 HTML**

我们的 HTML 结构将采用以下形式。我们已经使用了 ***< kbd >*** 标签来定义输入。里面的内容以浏览器默认的等宽字体显示。

## **用户界面样式**

对于样式，我们将有如下所示的 CSS 样式。

## **架子鼓功能**

对于我们的 JavaScript drum 功能，我们将针对任何按下的键打开窗口。当给定的键被按下时，我们将获得它的键码，并将其与相关的音频同步。简单的权利。

为了提供一个漂亮的动画并通知用户他们按了哪个键，我们将使用 JavaScript 在给定的键部分添加和删除一个 playing 类。

这我们将使用 CSS 样式一个简单的动画。

您可以在 [***codepen 上查看给定的代码。***](https://codepen.io/developerphilo/pen/OJjEdRB)

## **结论**

这是一个简单的项目，您可以利用它来学习 JavaScript。感谢您花时间阅读这篇文章。

希望对你有帮助。

## 更多阅读

[](/5-ways-to-make-money-with-technical-writing-as-a-developer-fffd263a37ed) [## 作为开发人员，用技术写作赚钱的 5 种方法

### 作为一名开发人员，我对通过技术写作赚钱的真实体验

javascript.plainenglish.io](/5-ways-to-make-money-with-technical-writing-as-a-developer-fffd263a37ed) [](/how-to-optimize-your-website-for-speed-96b6b42857ed) [## 如何优化你的网站速度

### 加速您的网站以提高性能并实施最佳实践

javascript.plainenglish.io](/how-to-optimize-your-website-for-speed-96b6b42857ed) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)