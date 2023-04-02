# JavaScript 中的 innerText vs innerHTML vs text content

> 原文：<https://javascript.plainenglish.io/innertext-vs-innerhtml-vs-textcontent-b8e92526e0c8?source=collection_archive---------4----------------------->

![](img/ac582d34cfa5d9e1133b18d2e1bf0091.png)

Photo by [Walkator](https://unsplash.com/@walkator?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

几周前，我正在做某件事，突然听到一声**“啊哈！”**某件事意义深远的时刻，我告诉自己应该探索它并写下来。

不幸的是，我不记得我在做什么，也不记得那个**“啊哈！”**一瞬即逝。所以，我要潜进去，看看能不能重新发现它。

# 内部文本

在普通 JavaScript 中，innerText 只获取 HTML 元素的呈现文本。本质上，浏览器中可见的文本就是 innerText 所获取的。

**HTML**

`<p id=“example”>This is an <span> example </span>.</p>`

**JavaScript**

```
var x = document.getElementById(“example”).innerText;
```

结果是“x”代表“这是一个例子”的内部文本

一些需要记住的事情:

*   如果元素被 CSS 隐藏(通过使用类似“显示”或“可见性”的属性), innerText 就不能访问它们
*   innerText 不会返回

[](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText) [## html element . innertext-Web API | MDN

### HTMLElement 接口的 innerText 属性表示节点的“呈现”文本内容及其…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/innerText) [](https://www.w3schools.com/jsref/prop_node_innertext.asp) [## HTML DOM innerText 属性

### 元素对象获取一个元素的内部文本:亲自尝试"更多"亲自尝试"的例子如下。内部文本…

www.w3schools.com](https://www.w3schools.com/jsref/prop_node_innertext.asp) 

# innerHTML

这将实际获取或设置一个 HTML 元素的内部内容。

当它检索内部内容时，它还将包括任何间距和内部元素标签，如

*   或等。

**HTML**

```
<p id=“example”>This is an <span> example </span>.</p>
```

**JavaScript**

```
var x = document.getElementById(“example”).innerHTML;
```

结果是‘x’表示‘这是一个示例’的 innerHTML

要更改 HTML 元素的内容:

```
document.getElementById(“example”).innerHTML = “And <strong> NOW </strong> the contents have been changed!”;
```

我想这可能是**‘啊哈！’先前我发现的瞬间。**

* * *由于 innerHTML 可用于更改页面内容，危险的

* * *所以不建议使用 innerHTML。***

相反，尝试使用 textContent。

[](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) [## element . innerhtml-Web API | MDN

### 注意:如果、或节点的子文本节点包含字符(&)、( )，innerHTML 将返回这些字符…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) [](https://www.w3schools.com/jsref/prop_html_innerhtml.asp) [## HTML DOM innerHTML 属性

### ❮元素对象改变 HTML 内容的一个元素与 id= "演示":尝试一下自己"更多"尝试一下自己"的例子…

www.w3schools.com](https://www.w3schools.com/jsref/prop_html_innerhtml.asp) [](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting) [## 跨站点脚本- MDN Web 文档词汇表:Web 相关术语的定义| MDN

### 跨站点脚本(XSS)是一种安全漏洞，它允许攻击者向网站注入恶意…

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting) 

# 文本内容

这将返回带有空格的文本内容(类似于 innerHTML)，但没有任何内部元素标记。

要检索文本内容:

**HTML**

```
<p id=“example”>This is an <span> example </span>.</p>
```

**JavaScript**

```
var x = document.getElementById(“example”).textContent;
```

结果是“x”表示“这是一个例子”的文本内容

要设置 textContent，就像上面的 innerHTML 例子一样。

```
document.getElementById(“example”).textContent = “And <strong> NOW </strong> the contents have been changed!”;
```

一些需要记住的事情:

*   将返回所有元素的文本内容，包括
*   将返回隐藏在 CSS 中的元素的文本

[](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) [## node . text content-Web API | MDN

### 接口的 textContent 属性表示节点及其后代的文本内容。的价值

developer.mozilla.org](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) [](https://www.w3schools.com/jsref/prop_node_textcontent.asp) [## HTML DOM textContent 属性

### 元素对象获取一个元素的文本内容:自己尝试“更多“自己尝试”的例子如下。的…

www.w3schools.com](https://www.w3schools.com/jsref/prop_node_textcontent.asp) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)