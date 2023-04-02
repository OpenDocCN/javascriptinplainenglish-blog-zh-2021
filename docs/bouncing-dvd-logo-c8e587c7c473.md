# 如何用 p5.js 构建弹跳 DVD logo

> 原文：<https://javascript.plainenglish.io/bouncing-dvd-logo-c8e587c7c473?source=collection_archive---------10----------------------->

![](img/0a4290ef942a09d6b33f13820d138f4a.png)

如何建立一个跳动的 DVD 标志网站使用:

*   HTML/CSS/JS
*   [p5.js](https://p5js.org/)

# 密码

*   [Repl.it 演示](https://repl.it/@remarkablemark/Bouncing-DVD-Logo)
*   [GitHub 库](https://github.com/remarkablemark/Bouncing-DVD-Logo)

# 说明

初始化变量:

在`[preload()](https://p5js.org/reference/#/p5/preload)`期间，加载 DVD 图像:

> `dvd1.svg`到`dvd8.svg`都在`assets/`目录下。

在`[setup()](https://p5js.org/reference/#/p5/setup)`期间，创建一个与`[window](https://developer.mozilla.org/docs/Web/API/Window)`宽度和高度相同的画布:

在`[draw()](https://p5js.org/reference/#/p5/draw)`期间，将 DVD 移向其路径并检查边界碰撞:

下面是检查边界碰撞的方法:

[*本文原载于 2021 年 1 月 12 日《remarkablemark.org》。*](https://b.remarkabl.org/35BJAXb)