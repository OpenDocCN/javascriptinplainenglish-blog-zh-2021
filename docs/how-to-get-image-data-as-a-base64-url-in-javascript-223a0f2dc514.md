# 如何在 JavaScript 中获取 Base64 URL 形式的图像数据？

> 原文：<https://javascript.plainenglish.io/how-to-get-image-data-as-a-base64-url-in-javascript-223a0f2dc514?source=collection_archive---------9----------------------->

![](img/1a781974e7b8ce9e198d926a66c945df.png)

Photo by [Sandie Clarke](https://unsplash.com/@honeypoppet?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 web 应用程序中获得 base64 URL 格式的图像数据。

在本文中，我们将了解如何在 JavaScript 中获取 base64 URL 形式的图像数据。

# 将图像放入上下文中，并将画布数据转换为 Base64

将图像文件转换为 base64 字符串的一种方法是将其放入画布。

然后我们可以调用 canvas 的`toDataURL`方法将其转换成 base64 字符串。

例如，我们可以写:

```
const getBase64Image = (url) => {
  const img = new Image();
  img.setAttribute('crossOrigin', 'anonymous');
  img.onload = () => {
    const canvas = document.createElement("canvas");
    canvas.width = img.width;
    canvas.height = img.height;
    const ctx = canvas.getContext("2d");
    ctx.drawImage(img, 0, 0);
    const dataURL = canvas.toDataURL("image/png");
    console.log(dataURL)
  }
  img.src = url
}getBase64Image('https://uploads.sitepoint.com/wp-content/uploads/2015/12/1450377118cors3.png')
```

我们创建了`getBase64Image`函数，它将`url`字符串作为图像的 URL。

然后我们用`Image`构造函数创建一个`img`ek element。

接下来，我们调用`seAttribute`来将`crossOrigin`属性设置为`anonymous`，这样我们就可以得到与我们所拥有的域不同的图像。

接下来，我们创建用`document.createElement`创建画布元素的`img.onload`方法。

然后我们将画布的宽度和高度设置为`img`元素的宽度和高度。

接下来，我们用`getContext`获得画布上下文。

然后我们调用`drawImage`在画布上绘制图像。

第二个和第三个参数是左上角的 x 和 y 坐标。

然后，我们用我们想要成像的 MIME 类型调用`toDataURL`,将它转换成图像的 base64 字符串版本。

然后`console.log`应该记录 base64 URL。

然后我们将`img.src`设置为`url`来触发`onload`方法运行。

因此，当我们用一个图像 URL 运行`getBase64Image`时，我们将看到它的 base64 字符串版本被记录。

# 结论

我们可以通过将带有给定 URL 的图像加载到画布中，然后调用`toDataURL`将其转换为 base64 URL。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)