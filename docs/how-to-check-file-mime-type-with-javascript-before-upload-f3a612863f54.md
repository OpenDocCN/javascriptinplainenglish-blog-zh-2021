# 上传前如何用 JavaScript 检查文件 MIME 类型？

> 原文：<https://javascript.plainenglish.io/how-to-check-file-mime-type-with-javascript-before-upload-f3a612863f54?source=collection_archive---------10----------------------->

![](img/a63e36999af1b5e621593206b8322ae6.png)

Photo by [SARAJ PIXNAPPER](https://unsplash.com/@pixnapper?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望在 web 应用程序中添加文件上传功能。

有时在上传之前，我们必须检查文件的类型。

在本文中，我们将看看如何在上传之前用 JavaScript 检查所选文件的 MIME 类型。

# 观察文件输入的变化事件

为了在上传文件之前用 JavaScript 检查文件的 MIME 类型，我们可以监听文件输入的`change`事件。

例如，我们可以编写以下 HTML:

```
<input type="file"  multiple>
```

和下面的 JavaScript 代码来观察选定的文件:

```
const control = document.querySelector("input");
control.addEventListener("change", (event) => {
  const {
    files
  } = control;
  for (const file of files) {
    console.log("Filename: ", file.name);
    console.log("Type: ", file.type);
    console.log("Size: ", file.size, " bytes");
  }
}, false);
```

我们有一个设置了`multiple`属性的文件输入来支持多个文件选择。

然后在 JavaScript 代码中，我们用`document.querySelector`得到文件输入。

然后我们用`'change'`参数调用`addEventListener`来观察文件输入中文件选择的变化。

在事件监听器中，我们从文件输入`control`中获取`files`。

然后我们循环遍历`files`并获得每个条目的`name`、`type`和`size`属性。

`name`有所选文件的文件名字符串。

`type`具有所选文件的 MIME 类型字符串。

并且`size`具有以字节为单位的文件大小数。

# 结论

我们可以通过监听`change`事件得到文件输入所选择的文件的 MIME 类型。

然后我们可以从元素的`files`属性中获取所选文件的内容。