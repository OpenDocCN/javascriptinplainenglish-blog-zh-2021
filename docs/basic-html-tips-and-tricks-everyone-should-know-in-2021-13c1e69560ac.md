# 2021 年每个人都应该知道的基本 HTML 技巧和窍门

> 原文：<https://javascript.plainenglish.io/basic-html-tips-and-tricks-everyone-should-know-in-2021-13c1e69560ac?source=collection_archive---------16----------------------->

## 关键的 HTML 技巧，窍门，以及破解面试所必需的知识。

![](img/88831fb303b69ddbc569661f5946afe7.png)

Photo by [JESHOOTS.COM](https://unsplash.com/@jeshoots?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

众所周知，使用前端技术的趋势正日益蓬勃发展。因此，最好了解一些基本的面试问题，这样可以让你在面试中一目了然。

在这里，我整理了一些基本的 HTML 面试问题，你必须在面试前做好准备。

# 如何在 div 中将一个元素水平居中？

随着`flexbox`的引入，设计元素的位置变得非常容易。

```
#element{  
  border: 5px solid black;
}#centerDiv{
  border: 1px solid blue;
  display: flex;
  width:100%; 
  justify-content: center;
}<div id="centerDiv">
  <div id="element">Center Me</div>
</div>
```

或者我们可以将 div 作为 inline box 并使用 align-text 属性。

```
#element{
  width: 100%;
  text-align: center;
}

#centerDiv{
  display: inline-block;
}<div id="centerDiv">  
    <div id="element">Center Me</div>
</div>
```

# 如何在 HTML5 中使用本地存储来存储对象？

localstorage 提供了 setItem 和 getItem 方法来存储值，在存储任何对象之前，我们需要使用 JSON.stringify 和 JSON.parse 来检索它们。

```
var data= { 'name': 'sheetal', 'surname': 'patel'};

// you can use setitem to store any object
localStorage.setItem('data', JSON.stringify(data));

// get item will give data back, you need to parse JSON
var obj = localStorage.getItem('data'); 
```

# 如何获得没有要点的无序列表？

bootstrap 4 提供了一个特定的类来实现这个设置`list-style-type: none;`

```
<ul class="list-unstyled">
   <li>...</li>
</ul>
```

# 如何使用 CSS 将一个元素垂直居中？

我们可以使用 flexbox 来实现同样的目标。

```
.container{
  display: flex;
  justify-content: center;
  flex-direction: column; 
  /* align */
  align-items: center;
}<div class="container">
  Center me
</div>
```

# 如何制作一个固定大小的 div，使其在文本变大时不会增加？

*   通过增加`display: inline-block`我们可以做到这一点。

```
<div>
    Contents
</div>
```

*   display inline-flex 也可以使它们固定大小。

```
div {
    display: inline-flex;
}
```

# 如何禁用表单或输入标签中的自动完成功能？

```
<form name="form" autocomplete="off">
```

或者

```
<input type="text" name="input" autocomplete="off" />
```

# 如何禁用文本区域的 resizable 属性？

添加这个 CSS 就可以了。

```
textarea {
  resize: none;
}
```

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)