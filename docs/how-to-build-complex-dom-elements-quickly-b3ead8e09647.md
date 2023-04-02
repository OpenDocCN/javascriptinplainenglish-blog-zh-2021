# 如何快速构建复杂的 DOM 元素

> 原文：<https://javascript.plainenglish.io/how-to-build-complex-dom-elements-quickly-b3ead8e09647?source=collection_archive---------4----------------------->

![](img/09ab4c4b3f61015cbf615644e7150164.png)

Photo by [Pankaj Patel](https://unsplash.com/@pankajpatel?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/html-tool?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

DOM，即文档对象模型，是 web 开发人员工作中不可或缺的一部分。因为它代表了网页中的元素树，所以它决定了浏览器向用户提供的底层结构。

虽然您可以用 JavaScript 添加和操作 DOM 元素，但是如果元素有许多属性，那么为它编写逻辑代码可能会很麻烦而且重复。在本教程中，我们将创建一个方法，让您更紧凑地添加复杂的元素。

# HTML DOM 结构示例

对于那些不熟悉 DOM 概念的人来说，它是网页上 HTML 元素的层次结构。下面是一个简单的例子。

A sample HTML DOM.

# 用 JavaScript 添加 DOM 元素

除了手工编写如上所示的页面或要求使用数据库的站点呈现 DOM 服务器端之外，我们还可以编写 JavaScript 来添加 DOM 元素并赋予其属性。让我们来看三种方法。

## 方法 1:没有其他方法

在下面的代码示例中，我们添加了一个`section`元素，并赋予它几个属性(`id`、`className`和`innerHTML`)以及三个属性(`data-foo`、`data-baz`和`onclick`)。

Creating an element with Vanilla JavaScript.

虽然这样做了，但是我们必须写六次`section`，我们必须写三次`setAttribute`。而更多的属性或性质将意味着更多的重复。

## 方法 2:调用实用方法

也就是说，我们可以通过编写一个定制的实用方法来消除重复，该方法允许我们以更紧凑的方式创建 DOM 元素:

Sample creatEl method call. Let’s make this possible!

在上面的例子中，我们调用了一个属于新的`dom_utils`对象的`createEl`方法。这样做时，我们传入一个对象，该对象具有应该在结果元素中显示的属性。

虽然属性直接在我们的对象上，但是属性在对应于`attrs`键的嵌套对象中。

```
attrs: { 
   dataFoo:'bar',
   dataBaz:'garply,
   onclick:'showModal()'
}
```

还要注意，这些属性使用的是 came case(`dataFoo`)而不是破折号语法(`data-foo`)。我稍后会解释原因。

## 方法 3:创建对象，然后调用方法

为了帮助我们区分传入的对象和方法，如果我们提前初始化对象，下面是我们的逻辑。

在涉及`dom_utils`的任一方法中，与方法 1 相比，重复较少。

在下一节中，我们将编写`dom_utils`和它的`createEl`方法。您可以使用包含 HTML 和 JavaScript 文件的本地目录，也可以使用 JSFiddle 或 CodePen 之类的编码沙箱。

# 起始代码

在我们的 HTML 中，让我们创建一个可以添加内容的元素。

```
<div id="root"></div>
```

使用 JavaScript，让我们创建一个空对象。

```
let utils = {};
```

现在让我们创建一个初始包装器，它将为我们的`utils`对象提供我们创建的方法。在本教程之后，您可以编写其他方法进入这个包装器。

```
(function(context) { // methods go here})(utils);
```

# 创建 HTML 元素

让我们首先为`createEl`方法写一个框架。它现在所做的就是将一个对象(`o`)作为参数，并返回一个 HTML DOM 元素。

```
let utils = {};(function(context) { **context.createEl = function(o) {** **let el = null;** // additional code will go here. **return el;**        
   };})(utils);
```

看起来很整齐，但是到目前为止，没用！

## 设置元素类型

为了创建我们的元素，我们将使用`document.createElement`。因为对象属性`type`是必需的，如果它不在对象中，我们设置一个默认值。

```
let utils = {};(function(context) { context.createEl = function(o) { **let type = o.type || 'div';** **let el = document.createElement(type);** return el;         
    };})(utils);
```

我使用一个`div`作为默认值，但是它可以是任何适合你需要的东西。

# 添加属性和特性

现在让我们添加一个添加属性和特性的方法。在 JavaScript 中，可以直接添加`id`、`className`等属性。

```
el.className = 'myClass';
el.id = 'myClass-2';
```

相比之下，必须通过`setAttribute`添加属性。

```
el.setAttribute('data-user','Nevin');
```

## 添加属性

让我们首先编写基于传入对象中的属性设置元素属性的逻辑(`o`)。为此，我们可以使用`Object.keys`方法获得对象键的数组，并使用`for...of`循环遍历它们。

```
let el = document.createElement(type);**for (const key of (Object.keys(o))) {

}**
```

这里有两个键我们不想处理:`type`和`attrs`。所以让我们添加逻辑来排除那些。

```
for (const key of (Object.keys(o))) { **if (key != 'attrs' && key != 'type') {

   }** }
```

现在让我们添加一行代码，为元素提供对象的当前键值对。

```
for (const key of (Object.keys(o))) {   if (key != 'attrs' && key != 'type') { **el[key] = o[key];**   }}
```

所以你可以检查你的工作，这是我们目前的 JavaScript。

## 添加属性

在我们添加属性之前，让我们首先检查一个`attrs`属性是否存在。我们将在`return el`之前添加它。

```
**if (o.attrs) {
}**
return el;
```

现在让我们浏览一下属性键。我们没有在`o`上使用`Object.keys`，而是钻入更深的一层，并在`o.attrs`上使用。

```
if (o.attrs) {
   for (let key of (Object.keys(o.attrs))) {

    }
}
```

需要注意的是:这里我用的是`let`而不是`const`。现在我想知道为什么会这样…

## dash 困境

需要注意的是，在 HTML 中，数据属性通常以破折号语法出现:

```
<div data-user="Nevin"></div>
```

因为 JavaScript 键中的破折号会抛出`Unexpected token`错误，所以需要用引号来设置这些属性名，而不要在`createEl`中出错。

```
let el = dom_utils.createEl({
    type:'div',
    attrs: {
       **'data-user':**'Nevin'
    }
});
```

现在我不喜欢那些引语。请记住，在展示了`createEl`应该如何工作的方法 2 和 3 中，我使用了 came case(`dataFoo`)而不是 dash 语法(`data-foo`)。

因此，我们可以在方法调用中编写 camelCase，让我们添加逻辑，将对象中的 camelCase 更改为元素的 dash 语法。首先，让我们使用逻辑 NOT ( `!`)运算符检查任何大写字母。

```
if (o.attrs) {
   for (let key of (Object.keys(o.attrs))) { ** if (key != key.toLowerCase()) {
  **      // coming soon **}**
   }
}
```

如果`key`不同于`key.toLowerCase`，那意味着我们至少有一个大写字母。让我们用下面的一行程序来处理大写字母。

```
if (key != key.toLowerCase()) {
 **key = key.replace(/[A-Z]/g, m => "-" + m.toLowerCase());**
}
```

下面是这一行代码的工作原理:

*   我们在`key`上调用`replace`方法，并使用正则表达式`/[A-Z]/g`来寻找所有大写字母的实例。
*   如果我们找到一个大写字母，我们在回调中将它赋给变量`m`。
*   我们使用`m => "-" + m.toLowerCase`将大写字母转换成破折号(`-`)，后跟小写字母。
*   例如，`dataFoo`变为`data-foo`，因为`F`被替换为`-f`。

*先不说:关于这种逻辑如何工作的更多细节，请查看我的文章* [*中关于它如何将 camelCase 转换为 dash 语法的内容。*](https://nevkatz.medium.com/from-camel-case-to-dash-syntax-in-javascript-c685206ee682?sk=26e6070335ec3db8ece2c49ac321b9f5)

在检查了 camelCase 并根据需要采取行动之后，我们通过一个`setAttribute`调用将属性-值对添加到元素中。

```
if (key != key.toLowerCase()) {
    key = key.replace(/[A-Z]/g, m => "-" + m.toLowerCase());
}**el.setAttribute(key, o.attrs[key]);**
```

下面是所有属性的逻辑组合:

attribute logic

回到前面提到的*注意*的一些东西:改变`key`到破折号语法的潜在需要是我们使用`let`而不是`const`来初始化它的原因——因为我们可以在键被创建后*改变*键。

# 终点线

万岁！现在我们可以用属性和特性来定义元素了。下面是完整的`createEl`方法。

# 演示

下面是一个非常基本的演示，所以你可以看到这个方法的工作原理。当你点击我的名字时，字体的颜色应该会改变。这是因为添加了一个带有值`changeColor()`的`onclick`属性，我在这里添加了一个额外的函数来证明添加了该属性。

此外，如果您研究 CSS，您还可以看到添加了另外两个`data-`属性和元素的类——显示了相应的 CSS 样式。

以防你好奇，我用的`changeColor()`函数如下。

```
function changeColor(el) {
  let color = Math.floor(Math.random()*16777215).toString(16);
  el.style.color = '#' + color;
}
```

非常感谢 CSS Tricks 的 Chris Coyier 提供的便利功能！

因此，只需一点点努力，您就可以编写自己的 DOM 实用方法迷你库，这将消除一些重复，并使在 JavaScript 中添加元素更加高效。感谢阅读！

# 在别处

这是我对 camelCase/dash 语法转换逻辑的深入研究。

[](/from-camel-case-to-dash-syntax-in-javascript-c685206ee682) [## JavaScript 中从骆驼大小写到破折号的语法

### 仔细看看一个概念丰富的代码片段。

javascript.plainenglish.io](/from-camel-case-to-dash-syntax-in-javascript-c685206ee682) 

而`changeColor`方法来自于这个 CSS 窍门。

[](https://css-tricks.com/snippets/javascript/random-hex-color/) [## 如何在 JavaScript 中生成随机颜色

### 这里有一个 quicky(也有 PHP 版本):var random color = math . floor(math . random()* 16777215)。toString(16)；看…

css-tricks.com](https://css-tricks.com/snippets/javascript/random-hex-color/) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)