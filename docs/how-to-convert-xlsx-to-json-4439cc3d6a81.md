# 如何将 XLSX 转换成 JSON

> 原文：<https://javascript.plainenglish.io/how-to-convert-xlsx-to-json-4439cc3d6a81?source=collection_archive---------3----------------------->

![](img/596e6595a8eb55546b823921e3a92ec9.png)

Photo by [Mika Baumeister](https://unsplash.com/@mbaumi?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/)

## 你需要从电子表格中获取数据并将其转换成 JSON 吗？那不是🚀科学，我要证明它！

首先，安装 **xlsx** 包。

使用 npm:

```
// NPM
npm  install  xlsx// Yarn
yarn  add  xlsx
```

在 **app.js** 文件中，导入 xlsx 和 fs 读取 excel 文件，并声明一个我们后面会用到的变量。

```
const XLSX = require('xlsx');
const fs = require('fs');
const finalObject = {};
```

要读取和获取缓冲区类型的文件内容:

```
const data = XLSX.read(myFile, { type: 'buffer' });
```

*注意:不同的类型是“字符串”、“缓冲区”、“base64”、“二进制”、“文件”、“数组”*

如果你写 **console.log(数据。您将看到您的电子表格和单元格的内容。**

然后，您必须为每个电子表格的每一行编写流程。

```
data.SheetNames.forEach(sheetName => {
  let rowObject = XLSX.utils.sheet_to_json(data.Sheets[sheetName]); finalObject[sheetName] = rowObject;
});
```

函数允许你将一个电子表格转换成一个对象数组。

它采用不同的可选参数，你可以在这里找到

在这里我们什么都不需要。

如果您执行 console.log( **rowObject** )，您将看到它包含一个数组，并且电子表格的每一行都被转换成一个对象，如下所示:

```
[
  { "ID": 1, "Last name": "Doe", "First name": "John" }, { "ID": 2, "Last Name": "Doe", "First name": "Jane" }
]
```

还记得我们一开始声明的变量吗？是时候使用它了。我们将为每个电子表格创建一个键，并将 **rowObject** 分配给它:

```
data.SheetNames.forEach(sheetName => {
  let rowObject = XLSX.utils.sheet_to_json(data.Sheets[sheetName]); finalObject[sheetName] = rowObject;
});
```

如果你**console . log(final object)**:

```
"Utilisateurs": [
{ "ID": 1, "Last name": "Doe", "First name": "John" },
{ "ID": 2, "Last name": "Doe", "First name": "Jane" }
]
```

如果您想将输出写入一个文件，只需添加这一行:

```
fs.writeFileSync('./target.json', JSON.stringify(dataObject));
```

瞧啊。🎉

现在您知道如何将 Excel 电子表格转换成 JSON 了！

最初发布于[我的博客](https://blog.ludivineachouri.com)。

*更多内容请看**[***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。****