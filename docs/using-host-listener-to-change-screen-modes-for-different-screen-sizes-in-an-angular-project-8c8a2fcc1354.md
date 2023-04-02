# 使用主机监听器更改角度项目中不同屏幕大小的屏幕模式

> 原文：<https://javascript.plainenglish.io/using-host-listener-to-change-screen-modes-for-different-screen-sizes-in-an-angular-project-8c8a2fcc1354?source=collection_archive---------7----------------------->

![](img/1d918ffbd4754a8fe42abf9682d78239.png)

Photo by [Annie Spratt](https://unsplash.com/@anniespratt?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

尤其是，使用 Angular 开发任何基于网络应用的项目，需要您假设您的用户不仅会在个人电脑的典型网络浏览器上浏览您的 Angular 项目，还可以在 iPad 或移动设备上查看。

在某些情况下，为了给用户提供最佳的用户界面/UX，当用户在移动设备上而不是在电脑上查看您的网站时，您可能需要隐藏某些细节。

虽然 Angular 被设计成动态的，但问题是，你可能想定制特定的观看体验，问题是你怎么知道网站是从哪里被观看的？

在加载 web 应用程序时，是否可以预先或动态地获得屏幕大小或浏览器大小，以确保用户获得最佳的 UI/UX 体验？无论他们在哪个设备或屏幕上查看您的 Angular web 应用程序？

如果您在基于角度的项目中也遇到了这个问题，答案是肯定的，这是可以实现的，我将向您展示如何使用主机侦听器动态地实现这一点。

## 0.准备好一个角度项目。角度 10+是优选的

这是一个速赢项目，如果你能让一个 Angular web 应用程序启动并运行，应该很容易实现。

## 1.通过@angular/core 向项目添加宿主侦听器

在页面的第一行，将以下内容添加到第 1 行的预制@angular/core 导入中(通常在典型的 angular 主页上)。见下文，我已经在**粗体**中设置了需要添加的属性

```
import { Component, OnInit, **HostListener** } from '@angular/core';
```

## 2.在您的班级中设置一个主机监听器来监听任何变化

这里的下一步是设置一个主机监听器来动态“监听”关于“窗口:调整大小”的任何变化。通过这样做，我们可以在每次浏览器改变大小时检查窗口大小，这就是我们将用来告诉我们的 web 应用如何反应的。但首先，设置主机侦听器:

在这种情况下，我已经设置了如果宽度超过 760 像素，我假设观众使用的是大屏幕。否则，我假设用户正在使用一个更小的设备。我还在`ngOnInit()`开始时(第 7-20 行)设置了`screenMode`的初始值

760 像素绝不是屏幕尺寸的默认指标。您可以根据自己的喜好进行设置，但根据我的经验，当用户在大宽屏或移动设备上时，这个值足以区分。

## 3.在你的 HTML 文件中添加`*ngIf`

最后，只需使用`*ngIf`来区分使用哪个屏幕来查看该 Angular web 应用程序，如下所示:

您可以在整个 HTML 页面中的任何地方使用`*ngIf`条件，以不同的屏幕大小显示不同的内容。

## 结论

我确信有更好的方法来适应不同的屏幕尺寸，但以上是我用来检查哪个屏幕被用来为我的用户和观众提供最佳 UI/UX 的方法。所以，概括一下:

1.  导入主机监听程序
2.  将主机侦听器添加到您的。ts 文件。这将决定屏幕大小。
3.  使用*ngIf 显示/隐藏不同屏幕尺寸的某些项目

*塞拉马特巨大的源泉*

*更多内容尽在*[plain English . io](http://plainenglish.io/)