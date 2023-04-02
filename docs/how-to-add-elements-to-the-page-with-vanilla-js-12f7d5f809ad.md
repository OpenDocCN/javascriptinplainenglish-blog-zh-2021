# 如何用普通的 JavaScript 向页面添加元素

> 原文：<https://javascript.plainenglish.io/how-to-add-elements-to-the-page-with-vanilla-js-12f7d5f809ad?source=collection_archive---------14----------------------->

## 您需要的所有方法都在一个地方！

![](img/f87e6821e973415b3c1da611c6ad7314.png)

这里有谁因为记不住确切的语法而每六个月就厌倦了谷歌“如何用 JS 向 page 添加元素”和“如何通过 X 找到元素”？这篇文章基本上只是试图通过把我们需要的所有东西放在一个方便的地方来节省未来你(和我)的时间。

# 助手功能

下面是用一个方便的函数向页面添加内容的完整过程:

```
***const*** **makeTag** = (**tagName**, **parentOrSelector**, **id**, **className**, **text**) => {
  ***const*** **tag** = document.createElement(**tagName**);
  if (**id**) **tag**.id = **id**;
  if (**className**) **tag**.classList.add(**className**);
  if (**text**) **tag**.append(**text**);
  const **parentElement** = (typeof **parentOrSelector** === '*object*')
    ? **parentOrSelector**
    : **document**.querySelector(**parentOrSelector**);
  **parentElement**.append(**tag**);
  ***return*** **tag**;
}const **addDataset** = (**tag**, **dataAttrs**) => {
 *// remember camelCase: val -> data-camel-case="val"*
  ***for*** (**key** in **dataAttrs**) {
    **tag**.dataset[**key**] = **dataAttrs**[**key**];
  }
}
```

我们走吧！一个方便的助手方法，也是另一个用于数据集的方法，因为我也经常忘记这些。此外，这里甚至还有针对最常见元素的*更多*便捷方法。

```
const **makeDiv** = (**parentOrSelector**, **id**, **className**) => (
  makeTag('*div*', **parentOrSelector**, **id**, **className**)
);const **makeP** = (text, parentOrSelector, id, className) => (
  **makeTag**('*p*', **parentOrSelector**, **id**, **className**, **text**)
);const **makeH1** = (text, parentOrSelector, id, className) => (
  **makeTag**('*h1*', **parentOrSelector**, **id**, **className**, **text**)
);
```

这样做的主要目的是节省更多的击键次数，并在实际需要时将`text`参数上移。

# 分解它们

添加元素的大致模式当然是:

1.  创建元素
2.  修改它
3.  将其附加到父级

这里添加的唯一“漂亮”的东西是 main helper 可以确定您是传入一个选择器(`#my-div`)还是一个实际元素。它还返回刚刚创建的元素；我发现这对创造孩子很有帮助:

```
const **myDiv** = **makeDiv**('*body*', '*newer*', '*wow*');
**makeH1**('*Test*!!!', **myDiv**, '', '*well-ok*');
**makeP**('*Test*', **myDiv**);
**addDataset**(**myDiv**, {test: '*neat*', anotherOne: '*cool*'});
```

# 随意使用和修改！

这正是我想用的，但请合并或复制任何对你有用的东西。例如，我使用了位置参数，但是也许你会喜欢传入一个具有`id, className`和`text`属性的对象。就像我之前说的，这篇文章只是把几个谷歌搜索压缩到一个书签里。

# 一些方便的查询

因为我在创建元素后谷歌的下一件事似乎是*寻找*元素，这里是最常见的方法:

```
***/* Get a single HTML Element */***
document.**getElementById**('example')
returns an HTML Elementdocument.**querySelector**('#example')
Returns an HTML Element***/* Get Multiple HTML Elements */***
document.**getElementsByClassName**('*more*')
Returns an HTMLCollection of Elementsdocument.**querySelectorAll**('.*more*') 
Returns a NodeList of Elementselement**.children**()
Returns HTMLCollection of elementselement.**childNodes**()
Returns NodeList of all child nodes***/* Get all elements by data attribute */***
.**querySelectorAll**('*[data-foo]*');
.**querySelectorAll**("*[data-foo='1']*");***/* special properties */***
document.**body** 
Returns the body elementdocument.**title**
Returns the title string***/* Special properties that return HTMLCollections */***
document.**embeds** 
document.**images** 
document.**head**
document.**links**
document.**scripts**
document.**anchors**
document.**forms** ***/* Access via indexes or ids */***
document.**forms**[0]
document.**forms**['some-id']***/* SPECIAL: Access a form's inputs via `elements` */***
document.**forms**[0].**elements**
document.**forms**[0].**elements**[0]
document.**forms**[0].**elements**['another-id']
```

如果您对 HTMLCollections 和 NodeLists 之间的区别感到困惑，那么*TL；dr:* HTMLCollections 只是 HTML 元素，NodeLists 也有这些元素，但也包括像文本和注释节点这样的东西。有一个很棒的 [Web Dev 简化视频解释了两种类型的列表](https://www.youtube.com/watch?v=rhvec8cXLlo&t=2s)。

不管怎样，给你！希望这个列表和函数能加快您下一个普通 JavaScript 项目的进度。

大家编码快乐，

麦克风

*更多内容请看*[***plain English . io***](http://plainenglish.io/)