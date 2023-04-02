# 如何用 JavaScript 检查选中图片的宽度和高度？

> 原文：<https://javascript.plainenglish.io/how-to-check-a-selected-images-width-and-height-with-javascript-342a88bf0bab?source=collection_archive---------6----------------------->

![](img/781ca100b565d08803b012d555be5fa3.png)

Photo by [Sergei Akulich](https://unsplash.com/@sakulich?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望检查用 JavaScript 输入的文件选择的选定图像的宽度和高度。

在本文中，我们将看看如何用 JavaScript 检查选定图像的宽度和高度。

# 使用 FileReader 和 Image 构造函数

我们可以使用`FileReader`构造函数创建一个对象来读取文件。

然后我们可以使用`Image`构造函数创建一个以读取的文件为内容的图像。

例如，如果我们有以下文件输入:

```
<input type='file'>
```

然后，我们可以通过写入以下内容将文件读入图像:

```
const fileUpload = document.querySelector('input')
const reader = new FileReader();
fileUpload.addEventListener('change', () => {
  reader.readAsDataURL(fileUpload.files[0]);
  reader.onload = (e) => {
    const image = new Image();
    image.src = e.target.result;
    image.onload = () => {
      const {
        height,
        width
      } = image;
      if (height > 100 || width > 100) {
        alert("Height and Width must not exceed 100px.");
        return false;
      }
      alert("Uploaded image has valid Height and Width.");
      return true;
    };
  };})
```

我们用`document.querySelector`选择文件输入。

然后我们创建一个`FileReader`实例。

然后我们用`addEventListener`向文件输入添加一个变更事件监听器。

在事件监听器中，我们调用`reader.readAsDataURL`来读取文件。

文件存储在`fileUpload.files`对象中。

索引 0 选择了第一个文件。

然后我们将`reader.onload`属性设置为创建`Image`实例的函数。

我们将`image.src`设置为`e.target.result`，将读取的文件设置为创建的`img`元素的内容。

然后我们将`image.onload`属性设置为获取图像的`width`和`height`的函数。

我们用`if`语句检查`width`和`height`是否是我们想要的。

现在，如果我们选择一个图像文件，我们应该看到根据图像大小弹出的警告框。

# 结论

我们可以使用`FileReader`构造函数创建一个对象来读取文件。

然后我们可以使用`Image`构造函数创建一个以读取的文件为内容的图像来检查所选图像文件的宽度和高度。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)