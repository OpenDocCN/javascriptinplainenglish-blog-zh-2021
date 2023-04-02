# 如何遍历 JavaScript 文件列表中的每一项？

> 原文：<https://javascript.plainenglish.io/how-to-loop-through-each-item-in-a-javascript-filelist-469c2634ae39?source=collection_archive---------7----------------------->

![](img/dfb0cc1bc078a348b3478a3b4b5e4a7f.png)

Photo by [Travis Yewell](https://unsplash.com/@shutters_guild?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望遍历 JavaScript 文件列表中的每一项。

在本文中，我们将研究如何遍历 JavaScript 文件列表对象中的每一项。

# 使用 Array.from 方法转换 FileList 对象，并使用 Array.prototype.forEach 方法

让我们遍历文件列表对象中的每一项的一种方法是用`Array.from`方法将其转换成一个数组。

然后我们可以对它使用`forEach`方法来遍历文件列表条目。

例如，如果我们有以下文件输入:

```
<input type='file' multiple>
```

然后，我们可以获取输入并监听文件输入的更改事件，以在选定文件后获取选定的文件:

```
const input = document.querySelector('input');
input.addEventListener('change', () => {
  Array.from(input.files)
    .forEach(file => {
      console.log(file)
    });
})
```

文件输入具有`multiple`属性，这样我们可以选择多个文件。

我们调用`input`上的`addEventListener`来向它添加一个变更监听器。

我们调用`Array.from`方法将`input.files`文件列表转换为包含所选文件的数组。

`input.files`是包含所选文件的文件列表对象。

然后我们可以调用`forEach`方法来遍历每个文件。

# 使用 Spread 运算符转换 FileList 对象，并使用 Array.prototype.forEach 方法

将文件列表对象转换为数组的另一种方法是使用 spread 运算符。

这是可行的，因为文件列表是一个可迭代的对象。

例如，我们可以写:

```
const input = document.querySelector('input');
input.addEventListener('change', () => {
  [...input.files]
  .forEach(file => {
    console.log(file)
  });
})
```

将`input.files`条目分散到一个数组中。

然后我们可以像以前一样在上面调用`forEach`。

# 使用 for-of 循环

因为文件列表对象是一个 iterable 对象，所以我们也可以对它使用 for-of 循环来遍历每个文件列表条目。

例如，我们可以写:

```
const input = document.querySelector('input');
input.addEventListener('change', () => {
  for (const file of input.files) {
    console.log(file)
  }
})
```

用 for-of 循环遍历`input.files`的每个条目。

# 结论

我们可以将文件列表对象转换成一个数组，并使用`forEach`方法或使用 for-of 循环遍历文件列表中的每一项。

*更多内容请看*[***plain English . io***](http://plainenglish.io/)