# 如何用 JavaScript 检查选中文件的大小？

> 原文：<https://javascript.plainenglish.io/how-to-check-the-size-of-a-selected-file-with-javascript-43f48c5a218b?source=collection_archive---------7----------------------->

![](img/009005b89736cac57e94780732ea8ad6.png)

Photo by [Jem Sahagun](https://unsplash.com/@jemsahagun?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能想用 JavaScript 检查所选文件的大小。

在本文中，我们将看看如何用 JavaScript 检查选定文件的大小。

# 使用 FileReader API

几乎所有现代浏览器都应该支持 FileReader API。

例如，我们可以通过编写以下 HTML 来使用它:

```
<form action='#'>
  <input type='file' id='fileinput'>
  <input type='button' id='btnLoad' value='Load'>
</form>
```

然后我们可以编写下面的 JavaScript 代码:

```
const addPara = (text) => {
  const p = document.createElement("p");
  p.textContent = text;
  document.body.appendChild(p);
}document
  .getElementById("btnLoad")
  .addEventListener("click", () => {
    const input = document.getElementById('fileinput');
    if (!input.files[0]) {
      addPara("Please select a file before clicking 'Load'");
    } else {
      const file = input.files[0];
      addPara(`File ${file.name} is ${file.size} bytes in size`);
    }
  });
```

在 HTML 代码中，我们有一个输入类型为`file`的表单。

我们有一个按钮，让我们点击它时显示文件信息。

在 JavaScript 代码中，我们使用了`addPara`函数来创建一个 p 元素，并将`text`设置为其内容。

然后我们调用`getElementById`来获取按钮输入元素。

然后我们调用`addEventListener`来添加一个点击监听器。

在点击监听器中，我们用`getElementById`得到文件输入。

然后我们检查`input.files[0]`是否存在。

`input.files[0]`选择第一个文件。

如果没有文件，我们调用`addPara`来显示一条消息。

否则，我们调用`addPara`来显示文件信息。

`file.name`有所选文件的文件名。

`file.size`以字节表示所选文件的大小。

当我们选择一个文件并点击 Load，我们应该会看到所选文件的文件信息。

# 结论

我们可以使用 FileReader API 轻松检查所选文件的信息。

*更多内容看**[***说白了. io***](http://plainenglish.io/)*