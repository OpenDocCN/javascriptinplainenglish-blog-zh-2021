# 如何将 HTML 画布的内容捕获为图像文件？

> 原文：<https://javascript.plainenglish.io/how-to-capture-the-content-of-an-html-canvas-as-an-image-file-d753712bb056?source=collection_archive---------8----------------------->

![](img/35a5c8bd494fac3d676ef399ee94fcf9.png)

Photo by [Jan Kopřiva](https://unsplash.com/@jxk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望将 HTML 画布的内容捕获为图像文件。

在本文中，我们将看看如何用 JavaScript 实现这一点。

# 捕捉画布

我们可以通过使用 canvas 元素对象附带的`toDataURL`方法来捕获画布。

例如，我们可以编写以下 HTML:

```
<canvas></canvas>
```

然后我们可以编写以下 JavaScript 来绘制一些内容，并将其捕获为图像文件:

```
const canvas = document.querySelector("canvas");
const context = canvas.getContext("2d");
context.fillStyle = "lightblue";
context.fillRect(50, 50, 100, 100);
window.location = canvas.toDataURL("image/png");
```

我们用`querySelector`得到画布元素。

然后我们用`getContext`得到画布的上下文。

然后我们用`fillStyle`设置填充样式。

我们用`fillRect`画一个长方形。

然后，我们只需在画布上调用我们想要生成的 MIME 类型文件的`toDataURL`来捕获画布，并将其转换为 base64 字符串。

# 将画布捕捉到 PDF

要捕获画布并将其转换为 PDF，我们可以使用 jaPDF 库。

为了使用它，我们编写以下 HTML:

```
<script src="https://unpkg.com/jspdf@latest/dist/jspdf.umd.min.js"></script>
<canvas></canvas>
```

然后，我们可以通过编写以下代码添加 JavaScript 代码来进行捕获:

```
const { jsPDF } = window.jspdf;
const canvas = document.querySelector("canvas");
const context = canvas.getContext("2d");
context.fillStyle = "lightblue";
context.fillRect(50, 50, 100, 100);
const imgData = canvas.toDataURL("image/png");
const doc = new jsPDF('p', 'mm');
doc.addImage(imgData, 'PNG', 10, 10);
doc.save('sample.pdf');
```

首先，我们从脚本标签添加的`jspdf`全局变量中获取`jsPDF`对象。

然后接下来的 4 行和前面的例子一样。

然后我们调用`canvs.toDataURL`并将返回的 base64 字符串赋给`imgData`。

接下来，我们用`jsPDF`构造函数创建一个新的 jsPDF 文档对象。

第一个参数是文档的方向。`p`表示门。

第二个参数是单位，`mm`是毫米。

然后我们用`imgData`调用`addImage`将图像添加到我们的文档中。

第二个参数是格式。

第三和第四个参数是图像相对于页面上边缘的 x 和 y 坐标。

然后我们用文件名和扩展名调用`doc.save`来保存 PDF。

# 结论

我们可以用`toDataURL`方法将画布的内容捕捉到图像中。

我们可以用 jsPDF 库把图像放入 PDF 中。