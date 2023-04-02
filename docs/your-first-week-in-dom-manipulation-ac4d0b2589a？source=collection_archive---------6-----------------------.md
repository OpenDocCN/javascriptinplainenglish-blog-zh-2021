# 理解 DOM 操作的初学者指南

> 原文：<https://javascript.plainenglish.io/your-first-week-in-dom-manipulation-ac4d0b2589a?source=collection_archive---------6----------------------->

*给不知所措的前端新手的一个简短的 JavaScript 初级读本。*

![](img/29198f4113ff8cd278b727c0716bf453.png)

Image by [Hatice](https://pixabay.com/users/haticeerol-14967706/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=5752322) from [Pixabay](https://pixabay.com/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=5752322)

我的训练营的结构让我们先学习了 Ruby on Rails 的后端，然后我们直接进入了 JavaScript。对于 Ruby，我们花了几个月的时间做基础的跑腿工作，而对于 JavaScript，大概是一个周末，接下来是一个星期。

当我的大脑还在适应`[for](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for)` vs `[for…in](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...in)` vs `[for…of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)` vs `[forEach](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach)` 的细微差别时，我们也很快开始将 JavaScript 应用到 [DOM](https://www.w3schools.com/js/js_htmldom.asp) 操作中(非常快，按照相同的顺序:创建一个循环，通过对象属性创建一个循环，通过数组元素创建一个循环，通过一个整洁的回调函数遍历数组元素)。

熟能生巧(或者至少是敷衍了事)，这里是 JavaScript DOM 操作的备忘单，我希望一开始就有。这可能是我们训练营课程的一部分，但希望它也能帮助你！

![](img/697eb07a47f10cd3e7871113ccb8e930.png)

## **重新认识 CSS 选择器**

在讨论 JavaScript 本身之前，要知道用普通 JavaScript 完成的大多数操作都涉及到[选择器](https://www.w3schools.com/cssref/css_selectors.asp)指向 DOM 中的特定元素(一种节点)。如果你以前没怎么用过 CSS，那会有很多东西要理解，所以把你选择的参考资料放在手边。这将帮助你理解更大的部分:

*   `element`:你可以使用 html 标签本身作为选择器
    ，例如`div`、`p`、`img`、`ul`
*   `.className`:通过在名称前加“.”按类别选择
    例如，使用`.profile-pic`选择`<img class=“profile-pic” alt="demo profile photo" src="photo.jpg"/>`
*   `#idName`:通过 id 前加一个“#”
    按 id 选择，如`#log-out-button`选择`<button id=“log-out-button”></button>`
*   `element[attribute=“value”]`:按特定属性选择，而不是按类别或 id
    选择，如`li[data-id=“3”]`选择`<li data-id=“3”></li>`
*   `outerElement innerElement`:在选择器之间使用一个空格来选择 outerElement 之内/之下的所有 innerElement(无论如何嵌套)
*   `outerElement > childElement`:用>表示子元素的*直接*父元素是 outerElement(不能进一步嵌套)

## 开始识别 DOM 树的各个部分

在`Document`上，你将首先使用一些方法来弄湿你的脚。根据 [MDN Web 文档](https://developer.mozilla.org/en-US/docs/Web/API/Document)的定义:

> `**Document**`接口代表浏览器中加载的任何网页，并作为网页内容的入口点，即 [DOM 树](https://developer.mozilla.org/en-US/docs/Web/API/Document_object_model/Using_the_W3C_DOM_Level_1_Core)。

我们进入网络魔法的界面！要开始抓取或制作这些树枝，我们可以使用以下方法。

*   `[document.querySelector](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelector)(“selector”)`:这将返回 DOM 中满足指定选择器的第一个元素。如果您想全部退回，可以使用`[document.querySelectorAll()](https://developer.mozilla.org/en-US/docs/Web/API/Document/querySelectorAll)`。
*   `[document.createElement](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement)(“tagName”)`:这将返回一个全新的空元素，HTML 标签为`tagName`，例如`div`、`p`、`img`、`ul`

为了以后更容易使用，最好开始将它们分配给变量名。

```
const profilePic = document.querySelector("img.profile-pic")
// assigns the first <img> element with class of "profile-pic"const newProfileDiv = document.createElement("div")
// assigns to a brand new <div> for future use
```

## 扩展和修剪🪴

在上面的两种方法中，我们能够找到元素并创建元素。但是现在它们只是存储在变量中等待，我们还没有对它们做任何事情。

以下是实现这一点的一些基本方法:

*   `[parentElement.append](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild)(childElement)`:这将把 childElement 放在父节点中最后一个子节点的后面(有一个非常相似的函数叫做 [appendChild()](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild) ，它适用于所有节点，只有很小的差别)。

```
newProfileDiv.append(profilePic) console.log(newProfileDiv)/*
   <div>
      <h3>Some stuff already in the div</h3>
**<img class=“profile-pic” alt="demo profile photo" src="photo.jpg"/>**
   <div>
*/
```

*   `[parentElement.prepend](https://developer.mozilla.org/en-US/docs/Web/API/Element/prepend)(childElement)`:这将把子元素放在父元素中其他子元素之前。

```
newProfileDiv.append(profilePic) console.log(newProfileDiv)/*
   <div>
**<img class=“profile-pic” alt="demo profile photo" src="photo.jpg"/>**
      <h3>Some stuff already in the div</h3>
   <div>
*/
```

*   您还可以调用子元素上的方法，比如`[before()](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/before)`和`[after()](https://developer.mozilla.org/en-US/docs/Web/API/ChildNode/after)`来获得类似的结果

```
const existingChildElement = newProfileDiv.querySelector("h3")existingChildElement.before(profilePic)
console.log(newProfileDiv)/*
   <div>
**<img class=“profile-pic” alt="demo profile photo" src="photo.jpg"/>
**      <h3>Some stuff already in the div</h3>
   <div>
*/---
OR
---existingChildElement.after(profilePic)
console.log(newProfileDiv)/*
   <div>
      <h3>Some stuff already in the div</h3>
**<img class=“profile-pic” alt="demo profile photo" src="photo.jpg"/>**
   <div>
*/
```

*   `profilePic.remove()`:你可以给予也可以取走——这将从 DOM 中移除个人资料图片`<img>`

## 进入主要事件(实际上是许多其他事件)

JS 提供的交互性主要来自于[事件监听器](https://developer.mozilla.org/en-US/docs/Web/API/EventListener)。当被点击、鼠标悬停或按键等事件触发时，侦听器将执行回调函数。这些是 [addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) 函数中的主要参数。如果我们想在点击现有的`<h3>`文本时插入个人资料图片，它可能看起来像这样:

```
existingChildElement.addEventListener("click", (event) => event.target.after(profilePic))
```

一旦指定的事件类型发生，就创建`Event`对象，在本例中是`click`。它有很多属性(用`console.dir(event)`查看)，最直接有用的是`target`，由事件通知的元素。在这种情况下，`event.target`就是简单的`existingChildElement`，但是一旦你开始使用[事件委托](https://dmitripavlutin.com/javascript-event-delegation/)或者表单，目标可能就不那么明显了。

## 认识你的朋友，数据集

元素的`[dataset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLOrForeignElement/dataset)`是一个通用属性，它提供对`[data-*](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/data-*)`自定义数据属性的访问，这些属性允许通过脚本在 [HTML](https://developer.mozilla.org/en-US/docs/Web/HTML) 和它的 [DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model) 表示之间交换信息。好吧，这是一个口。让我重新开始。

之前，在给出一个自定义属性由选择器选择的例子时，我使用了`li[data-id=“3”]`来选择`<li data-id=“3”></li>`。以“data-”开头的属性实际上存储在“*数据集*”属性中。您可以方便地存储一个`id`数字或任何属性，遵循下面演示的语法约定:

```
const exampleLi = document.querySelector('li[data-id=“3”]') exampleLi.dataset.id // "3"
exampleLi.dataset.id = 51 
console.log(exampleLi) = <li data-id=“51”></li>exampleLi.dataset.fosterCat = "Cocoa" 
console.log(exampleLi) = <li data-id=“51” data-foster-cat = "Cocoa"></li>
```

![](img/d5b4fe1e6c5706990a1b2c82a99345a2.png)

Rub that belly. Cocoa was my first foster from [King Street Cats](https://www.kingstreetcats.org/).

JS 中访问的“数据集”中的属性在 HTML 中显示为“数据-”。此外，属性的名称遵循它们各自的命名约定并被自动转换:对于 JS 是 camelCase，对于 HTML 是 kebab-case/dash-style。

```
element.dataset.camelCaseName = "not a camelCase name"
// [data-camel-case-name = "not a camelCase name"]
```

您不需要一开始就了解`.dataset`，但是了解属性名称将如何变化会有所帮助。

## 了解一下医生

你可能想了解`.classList`、`.innerHTML`、`.textContent`以及更多。互联网现在是朋友也是敌人。但主要是你的朋友。答案就在那里(可能在 MDN 上的[JS](https://developer.mozilla.org/en-US/docs/Web/JavaScript)T15[DOM](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction))。哦，还要学会使用你的浏览器开发工具！(这是 Chrome 的指南。)

好吧，越过我(和现在的你)，继续学习 JavaScript。如果我需要改变什么，请告诉我。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)