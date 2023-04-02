# 如何在浏览器中将 SVG 转换成图像？

> 原文：<https://javascript.plainenglish.io/how-to-convert-an-svg-to-an-image-in-the-browser-eec3d6298c07?source=collection_archive---------4----------------------->

![](img/0299f52b95a599cf193ecd49c836607f.png)

Photo by [Clem Onojeghuo](https://unsplash.com/@clemono?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想在 web 应用程序中将 SVG 图像转换成另一种图像格式，如 JPEG 和 PNG。

我们可以完全从客户端完成这项工作。

在本文中，我们将研究如何完全从客户端将 SVG 转换成另一种图像格式。

# 将 SVG 转换为图像

我们可以用客户端 JavaScript 代码将 SVG 完全转换成图像。

为此，我们写道:

```
const svg = `
<svg  version="1.1" baseProfile="full" width="300" height="200">
   <rect width="100%" height="100%" fill="red" />
   <circle cx="150" cy="100" r="80" fill="green" />
   <text x="150" y="125" font-size="60" text-anchor="middle" fill="white">SVG</text>
</svg>
`
svgToPng(svg, (imgData) => {
  const pngImage = document.createElement('img');
  document.body.appendChild(pngImage);
  pngImage.src = imgData;
});function svgToPng(svg, callback) {
  const url = getSvgUrl(svg);
  svgUrlToPng(url, (imgData) => {
    callback(imgData);
    URL.revokeObjectURL(url);
  });
}function getSvgUrl(svg) {
  return URL.createObjectURL(new Blob([svg], {
    type: 'image/svg+xml'
  }));
}function svgUrlToPng(svgUrl, callback) {
  const svgImage = document.createElement('img');
  document.body.appendChild(svgImage);
  svgImage.onload = () => {
    const canvas = document.createElement('canvas');
    canvas.width = svgImage.clientWidth;
    canvas.height = svgImage.clientHeight;
    const canvasCtx = canvas.getContext('2d');
    canvasCtx.drawImage(svgImage, 0, 0);
    const imgData = canvas.toDataURL('image/png');
    callback(imgData);
    document.body.removeChild(imgPreview);
  };
  svgImage.src = svgUrl;
}
```

我们有带 SVG 字符串的`svg`变量。

首先，我们用`svg`字符串和`callback`调用`svgToPng`。

然后我们用`document.createElement`创建一个`img`元素，并把它赋给`pngImage`。

然后我们调用`document.body.appendChild`将`img`元素附加到主体上。

然后我们将`pngImage.src`设置为我们将从回调`imgData`参数中获得的 URL。

然后我们创建一个`svgToPng`函数，它接受一个`svg`字符串和`callback`函数。

接下来，我们创建接受`svg`和`callback`的`svgToPng`函数。

它调用`getSvgUrl`函数从`svg`获取 base64 URL。

然后我们调用`svgUrlToPng`函数，用`url`和回调函数进行转换以获取图像数据。

为了创建`getSvgUrl`函数，我们只需调用`URL.createObjectURL`并将`svg`字符串转换为`Blob`实例，以返回 base64 版本的 SVG。

然后我们创建`svgUrlToPng`函数，将 SVG 放入画布。

我们这样做是为了以后可以将画布内容提取为图像二进制文件。

在`svgUrlToPng`函数中，我们创建了一个`img`元素。

然后我们用`document.body.appendChild`将创建的元素附加到主体上。

然后我们从`svgImage`尺寸中设置画布的宽度和高度。

然后我们调用画布上下文中的`drawImage`将 SVG base64 URL 绘制到画布中。

接下来，我们用要转换成的图像格式的 MIME 类型调用`toDataURL`。

然后我们调用`callback`,以便回调运行时将`imgData`图像数据传递给它。

然后我们调用`documen.body.removeChild`来移除预览。

我们还将`svgImage.src`设置为`svgURL`来添加预览。

# 结论

我们可以用 JavaScript 将 SVG 转换成另一种图像格式。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)