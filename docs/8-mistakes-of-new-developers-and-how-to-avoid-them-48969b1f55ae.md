# 我在学习 Web 开发时犯的 8 个错误

> 原文：<https://javascript.plainenglish.io/8-mistakes-of-new-developers-and-how-to-avoid-them-48969b1f55ae?source=collection_archive---------2----------------------->

## 新开发人员的错误以及如何避免这些错误。

![](img/c21865047145c056dfbda4c2912182eb.png)

Photo by [heylagostechie](https://unsplash.com/@heylagostechie?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们都是从某个地方开始的，而且大部分是从一个对 web 开发世界一无所知的地方开始的。那么怎么学呢？你当然是一头扎进去的！

学习新事物的最好方法总是去尝试。然而，去做它必须需要学习一些最佳实践和适当的技术，否则最终，你只会踢你自己。

我绝不是专家，但我也不是 web 开发的新手。在有幸帮助许多刚刚起步的人之后，我开始注意到一种趋势，即有些领域真的需要更多的解释来帮助那些刚刚起步的人。其他人避免了糟糕代码和不当实践的陷阱。

这篇文章旨在为新开发人员提供指导和帮助，我希望你能找到一些有用的东西。所以让我们开始学习吧！

# 1.过度使用浏览器

浏览器已经做了很多了，所以不要通过调整图片大小来做更多的事情。当您明确说明尺寸时，您的图像应该是内联的，例如:

```
<img src="img/img.png" alt="My Image" waidth="32" height="32" />
```

您告诉浏览器将图像的大小调整为 32px x 32px，无论它有多大。相反，请确保您在标记中使用的图像是它们需要启动的大小，或者使用 CSS。

# 2.过多的服务器请求

关于图像的话题，尽可能使用相对路径。相对路径意味着您指向与当前位置相关的资源。例如，如果您有一个目录，您从 index.html 调用一个图像，并试图访问名为 images 的文件夹中的图像，您可以使用:

```
<img src="images/img.png" alt="My Image" />
```

不是像这样调用完整路径，

```
<img src="http://mydomain.com/images/img.png" alt="My Image" />
```

每次浏览器必须发出 HTTP 请求时，您都会降低页面呈现的速度。这可能不明显，但每一点都有帮助，你应该总是努力将请求减少到最低限度。

# 3.不必要的 JavaScript

曾经有一段时间，需要 JavaScript 来实现页面上的任何交互性或用户反馈。虽然这对于某些事情来说是正确的，但是对于一些简单的方面来说，使用 JavaScript 是不必要的，而且显然是多余的。例子；翻车。

为用户提供良好的视觉反馈是为链接提供一个翻转阶段，如果你碰巧使用图像，这可能意味着在悬停或活动时用一个新的图像替换图像。这可以通过 CSS 很容易地实现，因此您不需要使用 JavaScript 和事件处理程序来交换图像。我的意思的一个例子:

HTML

```
<a href="#" title="My Link" id="my-link">My Link</a>
```

CSS

```
#my-link{
    **width**:40px;
    **height**:20px;
    **display**:block;
    **background**:url(*img/link-off.png*) no-repeat;
    **text-indent**:-9999px;
}
#my-link:hover{
    **background**:url(*img/link-on.png*) no-repeat;
}
```

现在链接在不活动时会显示一个图像，当鼠标悬停在上面时会显示一个新的图像，使用 JavaScript 没有额外的开销。

# 4 更进一步

虽然这种技术比使用 JavaScript 更好，但我们仍然可以使用 sprites 做得更好。sprite 获取多个图像，将它们组合成一个更大的图像，并用 CSS 定位它，以显示主图像所需的部分。这减少了加载到服务器上的图像，并提高了站点的响应能力。

要创建一个 sprite，您需要收集多个图像并创建一个社交链接列表，并且希望每个图像都有一个图像和一个翻转图像。对于四个链接的列表，这通常需要八个图像！使用雪碧，我们可以把它变成一个巨大的节约。让我们来看看设置它的一种方法。这个设置假设创建的 sprite 有两行四个图标，正常状态在顶部，悬停状态在底部，

HTML

```
<ul id="social-list">
    <li><a href="#" title="Twitter Link" id="twitter">Twitter</a></li>
    <li><a href="#" title="Facebook Link" id="facebook">Facebook</a></li>
    <li><a href="#" title="Google+ Link" id="google">Google +</a></li>
    <li><a href="#" title="LinkedIn Link" id="linkedin">LinkedIn</a></li>
</ul>
```

CSS

```
#social-list{**float**:**left**;**margin**:0;}
#social-list li{**float**:**left**;**width**:32px;**height**:32px;**margin**:0 4px;}
#social-list li a{**width**:100%;**height**:100%;**display**:block;**text-indent**:-9999px;**background**:url(*img/social-sprite.png*) no-repeat 0px 0px;}
#twitter{**background-position**:0px 0px;}
#facebook{**background-position**:0px -32px;}
#google{**background-position**:0px -64px;}
#linkedin{**background-position**:0px -96px;}

#twitter:hover{**background-position**:-32px 0px;}
#facebook:hover{**background-position**:-32px -32px;}
#google:hover{**background-position**:-32px -64px;}
#linkedin:hover{**background-position**:-32px -96px;}
```

你可以看到，通过使用一个图像，并根据我们使用它的位置简单地改变它的位置，我们可以操纵它为各种目的服务，并节省我们使用八个不同的图像。

# 5.类别和 Id

这可能是一个艰难的开始，所以让我们一步一步来。类和 id 之间的区别主要在于它们的特异性水平。可以说，分配给 ID 的任何 CSS 值都将覆盖分配给类中相同元素的相同值。下面是一个简单的例子:

HTML

```
<h1 class="big-blue" id="bigger-red">I Am A Title!</h1>
```

CSS

```
#bigger-red{**color**:red;}
.big-blue{**color**:**blue**;}
```

即使 big-blue 类是在 bigger-red 类之后声明的，h1 文本也将是红色的，因为 ID 将以这种方式压倒类。

类和 id 的第二个普遍问题是标记的使用。基本上，一个 ID 意味着每页使用一次*而一个类可以被重用。如果你有一个 header 标签，比如一个 h2，你总是希望它的高度为 20px，并且是绿色的，你应该给它分配一个 CSS 值来处理它，一个常见的错误是使用 ID 来完成这个。*

从语义上来说，这是不正确的，因为这个标签会在一个页面上多次使用，所以这需要使用一个类。例如，如果您有一个 h2 标签，它总是被用作页面的标题，那么它通常只被使用一次，因为页面只需要一个标题，因此可以用一个 ID 来代替。

一个广泛使用的例子是设置一些列。看看下面的示例代码。

HTML

```
<h4 id="title">My Column Title</h4>

<div class="column">
    <p>Hi I am a column!</p>
</div>

<div class="column">
    <p>Hi I am a column also.</p>
</div>

<div class="column">
    <p>Hi I must be a column too!</p>
</div>
```

假设页面上只有一个 ID，您会看到 ID 的使用为我提供了一种样式化本专栏标题的方法。每一列都有相同的类，因为每一列都有可能有相同的样式，比如宽度和浮动。

# 6.绝对定位

这是一个棘手的问题，但却经常出错。我看到的新人会大量使用元素定位来*强制*标记到他们想要的布局中。这样做的问题是，如果你碰巧让它排成一行，你是幸运的，而且，这根本不是正确的做事方法。让我解释一下。

经验法则；不要使用绝对定位。当然，除非你不得不。通过告诉一个元素在哪里是绝对的，你把它从标准的页面流中拿出来，这意味着如果你在容器的左边有一个你想要的图像，在它的右边有一些文本，你可以尝试使用*position:absolute；*但这样做实际上会迫使图像成为背景的一部分，这意味着它通常放入页面布局的宽度和高度变得没有意义，右边的文本将放在它的上面。

当这种情况发生时，大多数会通过再次使用绝对定位或一个大的边距来补偿，将文本块一直推到右边，这样它看起来就正确了。

使用如此严格和强制的布局对于代码的兼容性和未来维护来说是一场噩梦，所以，相反，尽量避免像那样强制容器，并使用适当的阻塞和浮动。下面是正确完成的上述示例的一些代码。

HTML

```
<div id="container">
    <img src="img/myimg.jpg" alt="myimg" />
    <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p>
</div>
```

CSS

```
#container{**width**:500px;}
#container img{**float**:**left**;}
#container p{**float**:**right**;}
```

一个非常简单的例子，但是你明白了。

# 7.无关标记

有时被称为*div tis，*我看到许多人变得过度依赖使用 div 来划分部分。例如，许多人会使用 div 来包围 nav 部分，

```
<div id="nav">
    <ul>
        <li><a href="#">Home</a></li>
        <li><a href="#">Blog</a></li>
        <li><a href="#">Contact</a></li>
    </ul>
</div>
```

虽然这没有什么错，但是您可以通过简单地将 nav ID 直接分配给 UL 来消除额外的 div。一个更详细的例子如下:

```
<div id="container">
    <div>
        <div>
            <img src="img.jpg" />
        </div>
        <div>
            <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p>
        </div>
    </div>
</div>
```

是的，我见过这个，还有更糟的！这么多的 div，但实际上有多少是必要的呢？也许是一个外部容器，记住你可以使用 CSS 来定位元素并告诉它们如何行为。所以如果你想，这将做什么，有一个图像和文本，文本出现在图像下，你可以做到这一点。

HTML

```
<div id="container">
    <img src="img.jpg" />
    <p>Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas.</p>
</div>
```

CSS

```
#container{**width**:400px;**margin**: 0 auto;}
#container img{**display**:block;**float**:**left**;}
#container p{**clear**:**left**;}
```

开始在你的标记中寻找方法，你可以删除一些额外的 div 和精简你的代码。

# 8.先跑步后走路

PHP、WordPress、jQuery 这些术语我相信你已经听说过，甚至可能玩过。我认为一个大问题是，新来者在掌握基础知识之前，试图处理更深入的部分。是的，我知道你喜欢 WordPress 并且想用它。

然而，如果你还不能构建一个静态的 HTML 页面，在 WP 及其相关的 PHP 中瞎折腾将会导致最终的灾难。当出了问题，而你在不确定输出是什么的情况下试图诊断*循环*时，会发生什么？

我绝不是说不要学习和使用新的库；这就是我如何通过拆开已经建立的东西并在此基础上进行推断而学到很多东西的。

然而，我确实暗示，我建议在你尝试深入 PHP 和其他框架之前，至少要有一个坚实的 HTML 和 CSS 基础。你肯定会省去一个头疼的问题。

希望您在这里找到了一些有用的东西，我敦促您作为一名新的开发人员继续在您的领域中进行试验和成长。享受你的工作！