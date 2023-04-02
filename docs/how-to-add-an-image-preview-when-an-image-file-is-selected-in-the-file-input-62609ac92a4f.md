# 在文件输入中选中一个图像文件，如何添加图像预览？

> 原文：<https://javascript.plainenglish.io/how-to-add-an-image-preview-when-an-image-file-is-selected-in-the-file-input-62609ac92a4f?source=collection_archive---------5----------------------->

![](img/5c727b2635d4d9fe927656c55cd090af.png)

Photo by [Marita Kavelashvili](https://unsplash.com/@maritafox?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

为选中的图片添加预览是我们在 JavaScript web 应用程序中经常要做的事情。

在本文中，我们将了解如何添加一个图像预览来显示用户选择的图像。

# 为文件输入添加图像预览

要为文件输入添加图像预览，首先，我们添加文件输入和`img`元素来显示图像预览:

```
<form>
  <input type='file' />
  <img src="#" alt="selected image" />
</form>
```

我们将`type`设置为`file`，使`input`成为一个文件输入。

接下来，我们需要添加一些 JavaScript 代码来将文件读入 base64 字符串。

然后我们可以将`img`元素的`src`属性设置为 base64 字符串。

为此，我们写道:

```
const imgInput = document.querySelector('input')
const imgEl = document.querySelector('img')imgInput.addEventListener('change', () => {
  if (imgInput.files && imgInput.files[0]) {
    const reader = new FileReader();
    reader.onload = (e) => {
      imgEl.src = e.target.result;
    }
    reader.readAsDataURL(imgInput.files[0]);
  }
})
```

我们用`document.querySelector`得到`input`和`img`元素。

然后我们用回调函数调用`imgInput`上的`addEventListener`，让我们观察文件选择。

我们传入`'change'`来观察当我们选择一个文件时触发的变更事件。

在回调中，我们检查`imgInput.files`是否存在。

`files`已经选中的文件。

我们得到索引为 0 的第一个文件。

然后我们创建`FileReader`实例来读取选择的文件。

我们还设置了选择文件时运行的`onload`方法。

我们使用`e.target.result`来获取文件结果。

该文件应该被读入一个 base64 字符串，这是一个`img`元素的`src`属性的有效值。

因此，我们可以直接将`img.src`属性设置为`e.target.result`。

为了触发文件的读取，我们用`imgInput.files[0]`调用`reader.readAsDataURL`方法，它有第一个选中的文件。

# `The createObjectURL Method`

我们还可以使用`createObjectURL`方法从选定的图像文件中创建 base64 字符串。

例如，我们可以写:

```
const imgInput = document.querySelector('input')
const imgEl = document.querySelector('img')imgInput.addEventListener('change', () => {
  if (imgInput.files && imgInput.files[0]) {
    imgEl.src = URL.createObjectURL(imgInput.files[0]);
    imgEl.onload = () => {
      URL.revokeObjectURL(imgEl.src)
    }
  }
})
```

并保持 HTML 代码不变。

我们用`imgInput.files[0]`调用`URL.createObjectURL`来从存储在`imgInput.files[0]`中的文件对象创建 base64 字符串。

然后我们设置`img`元素对象的`onload`方法，该方法在`img`元素的`src`属性改变时运行。

我们在那里调用`URL.revokeObjectURL`来从内存中释放图像对象。

# 结论

我们通过将选定的图像文件读入 base64 字符串并将其设置为`img`元素的`src`属性的值，将图像预览添加到 JavaScript 应用程序中。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)