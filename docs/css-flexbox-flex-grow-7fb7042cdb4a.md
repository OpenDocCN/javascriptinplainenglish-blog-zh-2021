# CSS Flexbox:伸缩增长

> 原文：<https://javascript.plainenglish.io/css-flexbox-flex-grow-7fb7042cdb4a?source=collection_archive---------17----------------------->

## flex-grow 是什么意思？

![](img/c3df9918fcf72ccca1c4cf4be67907e0.png)

Photo by [Maik Jonietz](https://unsplash.com/@der_maik_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在本文中，我们将讨论什么是 flex-grow。

Flex grow 指定该项相对于同一容器中的其他项增长多少。

最初，容器的宽度为 600 像素。

![](img/716edf0ba1b3a314e368ca9adbeadd49.png)

如果我们在红框处设置 flex-grow 等于 1，它将占据所有剩余的空间。

```
.red{background-color: red;flex-grow: 1;}
```

![](img/95f0b325bc69899dc8a34aeb2a47ac4e.png)

我们也可以用速记的方法来做。我们不使用 flex-grow，而是使用 flex。

```
.red{background-color: red;flex-grow: 1;}
```

## 所有项目都具有相同的弹性

如果所有项目的 flex-grow 值都设置为 1，那么所有的框在容器内都具有相同的宽度。这是因为它们都具有相同的伸缩性。

![](img/9066aff7ac530c6009a9213a5cf1cfa0.png)

All boxes take up equal width

## 其中一个框 flex-grow 设置为 2

如果我们将橙色盒子的伸缩设置为 2，那么它将占据两倍于其他盒子的空间。

![](img/82797eccfe932d04ac06436f5fa6ce8e.png)

width of orange box change from 100px to 250px

![](img/443f1fbf57eb1a90ae4cc89a6f28bcbe.png)

width of blue box change from 100px to 175px

橙色盒子增长 150 像素，是其他增长 75 像素的两倍。

关注我们: [YouTube](https://www.youtube.com/channel/UCu4-4FnutvSHVo9WHvq80Ww?sub_confirmation=1) ， [Medium](https://ckmobile.medium.com/) ， [Udemy](https://www.udemy.com/user/cyruschan2/) ， [Linkedin](https://www.linkedin.com/company/ckmobi/) ， [Twitter](https://twitter.com/ckmobilejavasc1)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)