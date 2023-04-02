# Javascript 中的原型

> 原文：<https://javascript.plainenglish.io/deep-understanding-of-prototypes-in-javascript-367a81f98847?source=collection_archive---------9----------------------->

# 获得深刻而清晰的理解

![](img/cf5da62608c72b82bea9e0625879b80f.png)

到这个故事结束时，你会对 JavaScript 中的 __proto__ 和原型有很好的理解。

我们都知道函数是 JavaScript 中的对象。当你创建一个函数时，你得到了函数和函数的对象。我们将该函数称为“构造函数”。所以，当你创建一个函数时，有两件事需要考虑:

1.  函数(构造函数)
2.  该对象

![](img/8e7696032e0571424daee9c004fc2b64.png)

Image 1

当你声明一个如“图 1”所示的函数时，你会得到如下结果:

![](img/de437201c838dd078417965e0e821414.png)

Image 2

在该对象圆中，有一个名为“原型”的属性，如下图所示:

![](img/30b976f824cad8b3973d5768b3c1171d.png)

Image 3

现在，让我们看看用“new”关键字实例化 Circle 会发生什么。当实例化一个函数时,“new”关键字做三件事:

**1。**创建一个空对象，并将该空对象分配给“this”

这={}

**2。**将已创建对象的“__proto__”属性链接到“原型”

**3。**返回“本”

让我们看一个例子。

![](img/34218141fb8359f000ba028b8ab4f3a1.png)

Image 4

当您运行“图 4”中给出的上述代码时，会发生以下情况:

![](img/ff1d85599dea50847764a3c8dcf832e4.png)

Image 5

“new”关键字执行以下操作:

![](img/94597423d8077d3e2e7ece797f403e19.png)

1st step

然后:

![](img/1f2de0907168c914dddba1e60b97d5b6.png)

2nd step

然后:

![](img/d72e503bc33fc313c4d2111d495b405f.png)

3rd Step

现在您可以访问该对象了。您将在 c1 对象的 __proto_ property 内的“Image 4”中显示“location”。

![](img/e14560a9e4c9712034de9ab4e8b97858.png)

Image 5

就是这样。我希望这让您对 JavaScript 中的原型有了清晰的理解。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)