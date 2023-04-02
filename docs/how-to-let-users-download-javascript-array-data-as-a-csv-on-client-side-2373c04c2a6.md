# 如何让用户在客户端下载 JavaScript 数组数据为 CSV？

> 原文：<https://javascript.plainenglish.io/how-to-let-users-download-javascript-array-data-as-a-csv-on-client-side-2373c04c2a6?source=collection_archive---------7----------------------->

![](img/d84c87c51b0c193b0bb82411e64dda6c.png)

Photo by [Erik Karits](https://unsplash.com/@erik_karits?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们可能希望让用户下载一个嵌套数组，其中的数据是一个 CSV 文本文件。

在本文中，我们将研究如何让用户在客户端以 CSV 格式下载 JavaScript 数组的数据。

# 使用 window.open 方法

我们可以使用`window.open`方法打开一个 URL 编码的字符串，让用户下载到他们的计算机上。

例如，我们可以写:

```
const rows = [
  ["name1", "new york", "abc"],
  ["name2", "san francisco", "def"]
];let csvContent = "data:text/csv;charset=utf-8,";for (const rowArray of rows) {
  const row = rowArray.join(",");
  csvContent += `${row}\r\n`;
}
const encodedUri = encodeURI(csvContent);
window.open(encodedUri);
```

我们有`rows`嵌套数组，我们想把它转换成 CSV 字符串，让用户下载。

为了进行转换，我们首先定义了指定 MIME 类型和字符集的`csvContent`字符串的开头。

然后我们循环遍历`rows`条目，连接每一行的条目，并用换行符将它们添加到`csvContent`字符串中。

然后我们用`csvContent`字符串调用`encodeURI`，将其编码成 URL 编码的字符串。

最后，我们可以用`window.open`下载字符串作为文件。

我们也可以用`map`方法缩短 for-of:

```
const rows = [
  ["name1", "new york", "abc"],
  ["name2", "san francisco", "def"]
];const csvContent = `data:text/csv;charset=utf-8,${rows
  .map((e) => e.join(","))
  .join("\n")}`;const encodedUri = encodeURI(csvContent);
window.open(encodedUri);
```

我们只需调用`rows`上的`map`，用`join`将每一行映射到一个逗号分隔的字符串。

然后我们在映射的字符串上调用`join`。

以这种方式下载文件不允许我们设置文件名。

为了让我们设置文件名，我们可以创建一个不可见的链接，并以编程方式单击它。

为此，我们呼吁:

```
const rows = [
  ["name1", "new york", "abc"],
  ["name2", "san francisco", "def"]
];
const csvContent = `data:text/csv;charset=utf-8,${rows
  .map((e) => e.join(","))
  .join("\n")}`;
const encodedUri = encodeURI(csvContent);
const link = document.createElement("a");
link.setAttribute("href", encodedUri);
link.setAttribute("download", "data.csv");
document.body.appendChild(link);
link.click()
```

我们调用`createElement`来创建一个`a`元素。

然后我们将`href`设置为`encodedUri`。

然后我们将`download`属性设置为带有`setAttribute`的文件名。

接下来，我们用`link`调用`appendChild`将其附加到主体上。

然后我们点击它上面的`click`，开始下载。

# 将数据保存为 Blob

我们可以通过重写上面的例子将数据保存为 blob。

例如，我们可以写:

```
const rows = [
  ["name1", "new york", "abc"],
  ["name2", "san francisco", "def"]
];
const csvContent = rows
  .map((e) => e.join(","))
  .join("\n");
const blob = new Blob([csvContent], {
  type: 'text/csv;charset=utf-8;'
});
const url = URL.createObjectURL(blob);
const link = document.createElement("a");
link.setAttribute("href", url);
link.setAttribute("download", "data.csv");
document.body.appendChild(link);
link.click()
URL.revokeObjectURL(link.href)
```

我们有只包含 CSV 字符串内容的`csvContent`字符串。

然后我们用`Blob`构造函数创建一个 blob。

在它的第二个参数中，我们将`type`设置为 blob 的数据类型。

接下来，我们调用`URL.createObjectURL`来创建一个可以下载的编码 URL。

我们用和以前一样的方法创建链接元素，但是用从`URL.createObjectURL`创建的`url`代替。

此外，下载完成后，我们必须调用`URL.revokeObjectURL`来释放资源。

# 结论

我们可以让从客户端的嵌套数组生成 CSV，并让用户下载一些 JavaScript 代码。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)