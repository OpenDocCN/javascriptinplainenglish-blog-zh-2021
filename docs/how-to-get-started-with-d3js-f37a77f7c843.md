# D3.js 如何入门

> 原文：<https://javascript.plainenglish.io/how-to-get-started-with-d3js-f37a77f7c843?source=collection_archive---------22----------------------->

![](img/6f9a9a02749bb6484c2a0c09cdadff3a.png)

D3 代表*数据驱动文档*是一组 JavaScript 库，利用 web 标准创建数据的可视化表示。它由许多单独的库组成，不仅用于可视化，还用于数据处理、获取、事件处理、动画等等。

D3.js 不难学，不需要很深的 JavaScript 知识，但是因为你可以用它做很多事情，所以你需要一些耐心和练习。

下面的小教程将帮助你对它的工作方式有一个基本的了解，并且更有信心使用它。您可以从创建一个空白的 HTML 文件开始，然后在执行这些步骤时粘贴代码。

1.  **了解 SVG**

SVG 以 XML 格式定义了基于矢量的图形。它基本上是用“HTML like”标签和属性来绘制图形。D3Js 将动态生成 SVG，并使用属性操纵它们。

SVG 图形是可调整大小和缩放的，没有质量损失，因为没有像素，只有位置、长度和命令

。svg 文件可以用图像编辑器和文本编辑器打开，允许查看它们的“代码”。

创建自己的 SVG 只需要几分钟，这是一个很好的起点。

[](https://www.w3schools.com/graphics/svg_reference.asp) [## SVG 参考

www.w3schools.com](https://www.w3schools.com/graphics/svg_reference.asp) 

**2。基本语法**

让我们从用于选择、创建和修改节点的 DOM 操作命令开始。在我们开始使用它们之前，我们首先需要加载 D3 库，将脚本文件的链接放在网页的 head 部分:

```
<script src="https://d3js.org/d3.v7.min.js"></script>
```

语法非常简单:

*   [*选择*](https://github.com/d3/d3-selection) *:* 我们的起点，这里是单据体
*   *Append:* 添加一个子元素，这里的主体添加了一个 SVG 文档，然后在这个 SVG 里面添加一个圆圈。
*   *属性:*设置或修改先前选择或创建的元素的属性

让我们将以下脚本放在网页的正文部分:

```
<script> d3.select("body") .append("svg") .attr("width", 960) .attr("height", 500) .append("circle") .attr("r", 50) .attr("cx", 350) .attr("cy", 150)</script>
```

如果您使用 web 浏览器打开 HTML 文件，它应该显示一个黑色磁盘，如果没有，请检查库的链接是否存在，以及脚本是否位于正确的部分。

现在让我们添加另一个不同半径的圆。首先，我们需要为每个圆圈创建一个单独的容器:

```
<div id="data1"></div>
<div id="data2"></div>
```

我们需要复制代码，用 d3.select("#data1 ")和 d3.select("#data2 ")替换 d3.select("body ")。属性“r”的值也应该不同，以便我们获得两个不同大小的磁盘。

在这一点上，我们可以说我们已经创建了一个数据可视化，它只是不是很有用，因为这里的数据仅限于两个值。

**3。数据连接**

在大型数据集的情况下，我们不能为每个值创建一个容器。

```
let hdata = [34,19,63,12,46,14,87,11]
```

[加入](https://observablehq.com/@d3/selection-join)将允许我们在同一个容器中，用同一段代码为数据中的每个值创建一个图形元素。

让我们为 *hdata* 数组创建一个“类似直方图”的可视化效果。首先，我们在主体部分添加一个新的 div，id 为 *histo* 。然后，我们将下面的代码放在我们之前使用的另外两个脚本之后:

```
d3.select("#histo").append("svg") .attr("width", 760) .attr("height", 500).append("g") .attr("fill", "#6D3A7E") .attr("transform", "translate(200, 0)").selectAll("rect").data(hdata).join("rect") .attr("x", (d,i) => i * 40) .attr("width", 20) .attr("y", 1) .attr("height", d => d);
```

这段代码是做什么的？

*   选择 id 为“histo”的目标容器
*   创建一个 SVG，然后创建一个分组“g ”,并在 200 的右边为它包含的所有元素分配一个颜色和一个翻译。
*   选择 All "rect ":在创建元素之前选择元素
*   *数据(hdata)* :分配数据
*   *join*:join 语句后的命令将应用于每个创建的“rect”元素:

>“x”值(水平位置)是数组索引* 40

>“高度”是数组中的当前值

>每个矩形的“宽度”是 20

>所有矩形的“y”(垂直位置)都相同。

**4。挑选例子并开始破解**

你很可能不需要从头开始编写所有的代码，一旦你掌握了基础知识，你就可以从例子中借鉴，做一些修改，看看效果如何。感谢您的阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)