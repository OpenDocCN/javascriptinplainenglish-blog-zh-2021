# 在 React 中下载 PDF 格式的 HTML

> 原文：<https://javascript.plainenglish.io/download-html-as-a-pdf-in-react-fc86114c9095?source=collection_archive---------2----------------------->

## 比你想象的容易！

![](img/66752b1daad1087cc50dfc812bd7f3c8.png)

Credit: Google

下载 PDF 是现代前端应用中的常见用例。但是在客户端构建 PDF 可能会很痛苦。在 React 中，我们有一些很棒的库，比如`[react-pdf/renderer](https://www.npmjs.com/package/@react-pdf/renderer)`来帮助我们。

## 传统图书馆的问题

`react-pdf/renderer`是一个很棒的库，提供了很多定制。但是它有自己的成本。例如

*   您必须为您的 PDF 文档设计一个单独的组件
*   如果你没有正确处理边缘情况，有时渲染会失败
*   你必须根据他们的规格分别设计。

如果您想构建一个数据量大的定制 PDF，所有这些都没问题。但是如果你想要更简单的呢？

> 如果您只想按原样打印正在呈现的组件，该怎么办？

让我们看看如何使用一个巧妙的技巧和一些 JavaScript 知识下载 PDF 格式的组件。

# 概观

我们要遵循的过程是将 HTML 元素转换成图像，然后将图像放入另一个强大的 PDF 库中。

> HTML 文档->图像-> PDF

为此，我们需要两个库。

1.  `[html2canvas](https://www.npmjs.com/package/html2canvas)` - >将我们的 HTML 文档转换成图像
2.  `[jspdf](https://www.npmjs.com/package/jspdf)` - >将生成的图像插入 PDF 文件

*完整代码在底部。如果你只对那个感兴趣，直接去那里。否则请原谅我。用不了多久*

## 第一步。安装依赖项

首先，安装所需的依赖项。

```
yarn add jspdf html2canvas
```

## 第二步:添加下载器功能

现在要么为您的`GenericPdfdownloader`创建一个单独的组件，要么将下面的代码放入您想要下载的组件中。

# 代码在做什么

*   `Input` - >该功能以`rootElementId`为输入。这将是可下载组件的 id。我们可以像下面这样定义任何元素的 id

因此，如果我们想用`id=”divToDownload”`下载`div`中的组件，那么我们必须将`”divToDownload”`传递给函数

## `1\. Getting the HTML Element`

在下一步中，我们将使用传递的 Id 获取 HTML 元素。

```
const input = document.getElementById(rootElementId);
```

## `2\. Converting HTML to Image`

接下来，我们将该元素传递给`html2canvas`,它会返回一个图像

```
***html2canvas***(input)
    .then((canvas) => {
        const imgData = canvas.toDataURL('image/png');
    })
```

## `3\. Putting The Image into PDF`

接下来，我们创建一个新的 PDF 文档，并将图像放入其中。

```
const pdf = new jsPDF();
pdf.addImage(imgData, 'JPEG', 0, 0);
pdf.save("download.pdf");
```

这里的两个零是生成的 PDF 文档的`padding`。你可以随意改变它们。

此外，您可以修改可下载的文件名。

## 完全码

下面是一个自定义 PDF 下载器的完整代码，它有两个参数:

1.  根元素标识为`rootElementId`
2.  下载文件名`downloadFileName`

现在，您可以将该组件放在项目中的任何位置，如下所示:

## 结论

这就对了。现在你有了你的自定义 PDF 下载器，可以在你的项目中的任何地方使用。感谢您的阅读！

**有什么话要说？**

**通过**[**LinkedIn**](https://www.linkedin.com/in/56faisal/)**或我的** [**个人网站**](https://www.mohammadfaisal.dev/) **与我取得联系。**

## 资源:

*   [https://stack overflow . com/questions/44989119/generating-a-pdf-file-from-react-components](https://stackoverflow.com/questions/44989119/generating-a-pdf-file-from-react-components)