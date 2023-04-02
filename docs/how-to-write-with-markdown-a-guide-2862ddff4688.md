# 如何用 Markdown 写作:指南

> 原文：<https://javascript.plainenglish.io/how-to-write-with-markdown-a-guide-2862ddff4688?source=collection_archive---------18----------------------->

## Markdown 是一种具有纯文本格式语法的轻量级标记语言，由约翰·格鲁伯和艾伦·施瓦茨于 2004 年创建。

![](img/b969279007fe23be2a44f0c46d707746.png)

Photo by [Brad Neathery](https://unsplash.com/@bradneathery?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

减价现在几乎无处不在。从在 GitHub 中实现到驱动最常见的博客网站，都清楚地表明理解它的基础知识是至关重要的。

Markdown 是一种具有纯文本格式语法的轻量级标记语言，由约翰·格鲁伯和艾伦·施瓦茨于 2004 年创建。Markdown 通常用于格式化自述文件，在在线论坛中撰写消息，以及使用 Markdown 中的纯文本编辑器创建富文本。

在这篇文章中，我们将看看让你开始编写 markdown 文件的各种方法。

Markdown 允许您使用易读、易写的纯文本格式编写，然后将其转换为结构有效的 XHTML(或 HTML)。

从记录自述文件到运行博客页面，Markdown 到目前为止发挥着至关重要的作用。降价文件的扩展名总是. md。

# 标题

markdown 中的标题非常类似于 HTML 标签。在 markdown 中，我们将用标签# precede 替换 h1。

请记住提供如下指定的标签和标题名称。##航向二。

在 markdown 中，标题可以写成如下形式。

# H1 由(#)代表

# H2 由(##)代表

# H3 由(###)代表

## H4 由(####)代表

H5 由(#####)代表

H6 由(######)代表

# 段落、分隔符和水平线

段落可以通过使用纯文本来实现。为了在段落中获得间隔，我们需要留出空白。

为了换到另一行，我们使用

标签。

在 markdown 中，水平线也可以通过在单独的一行上使用三个破折号或下划线来实现。

# 强调:粗体和斜体

为了在 markdown 中强调这一点，我们将用一个双星号**将世界括起来。

结果

。**加粗**。

为了提供斜体字，我们用一个星号*将该词包装成斜体字。

结果

*斜体*

# 链接

我们可以在 markdown 文件中包含引用链接，如下所示。

[文本链接此处](链接此处)

[链接正文](https://www.linkedin.com/in/amjohnphilip/)

# Mailto 链接

Mailto 链接与链接非常相似，为了包含 mailto:链接，我们用尖括号将它们括起来。

\ [example@domain.com\](mailto:example@domain.com\) 。

[example@domain.com](mailto:example@domain.com)。

# 列表

Markdown 支持列表。它支持有序列表和无序列表。

# 有序列表

markdown 中的有序列表由编号标记指定:

1.  第一
2.  第二
3.  第三

# 无序列表

无序列表可以用加号(+)或减号(-)来指定。星号(*)也可以。

例子

*   第一
*   第二
*   第三

## **图像**

我们可以实现图像的使用，如下例所示。

下面的例子:

！[Pexelry 图像查找器]([shutterstock.com/blog/wp-content/uploads/si..](https://www.shutterstock.com/blog/wp-content/uploads/sites/5/2020/05/Image-Files-Blog-Icons-2.jpg?w=750)“图像 alt here”)

## **代码块**

markdown 中的代码块使用三个反勾号(```)包装，这三个反勾号用于代码块中的开始标记和结束标记。

例子

` ` mounted: function() { this。$ http . get([Facebook-log in/API/get _ customers . PHP '](http://facebook-login/api/get_customers.php'))。然后(response =>{ return response . data；}) .然后(data =>{ store . commit(' add customer '，{ id: '2 '，name:' User 2 ' })})；} ```

结果

```
 mounted: function() {this.$http.get(‘http://pexelry/api').then(response => {return response.data;}) .then(data => {store.commit(‘addImage’, { id: ‘2’, name: ‘User 2’})});}
```

**区块报价**

块引号可以通过在文本前面加上大于号(>)来实现。任何写在大于号之后的文本都将被转换成块引号。

结果

> 趣闻:“人生有三件事很重要。首先是要善良。第二是要善良。第三是要善良。”

**走之前**

简单回顾一下，我们已经学会了如何将以下内容纳入降价:

**标题、图片、块引号、代码块、列表【有序和无序列表、链接、段落和强调(粗体和斜体)。**

感谢您阅读本文到目前为止；如果你觉得它有帮助，请在评论区告诉我，不要犹豫分享。

**更多阅读:**

[](/all-you-need-to-know-about-the-css-position-property-c329b2882613) [## 关于 CSS 位置属性，您只需要知道

### CSS 位置属性总是很难去神秘化，并且很难理解它是如何在…

javascript.plainenglish.io](/all-you-need-to-know-about-the-css-position-property-c329b2882613) [](/why-you-should-be-part-of-a-developer-community-f3e28bc13c88) [## 为什么你应该成为开发者社区的一员

### 开发者社区组织者的故事。

javascript.plainenglish.io](/why-you-should-be-part-of-a-developer-community-f3e28bc13c88) 

*更多内容请看*[*plain English . io*](http://plainenglish.io/)