# 如何使用 Excel 和 React

> 原文：<https://javascript.plainenglish.io/how-i-use-excel-with-react-js-c6b42f2ec3a1?source=collection_archive---------5----------------------->

我在 React 中使用 excel 的方式

![](img/4b9592c5f47fe0aeac48a6770d9b8502.png)

Excel 是一个强大的工具。由于许多人非常依赖它，Excel 已经成为一种行业标准，用于创建、操作和处理大量数据。

我在 React 中使用了几个库来生成报告。最简单的是 react-csv，它几乎不需要配置，就能为您提供一个 csv。

但是这些天我依赖的图书馆是 [exceljs](https://www.npmjs.com/package/exceljs) 。

## 使用 exceljs 的原因是:

对于 CSV(逗号分隔值)和普通 CSV 库，某种程度上限制了您对电子表格布局的控制。

CSV 只是一个简单的文本文件，但你可以生成。xlsx

因此，在使用可以生成。xlsx 文件，你可以控制每一个细胞。你决定页眉尺寸，你决定对齐方式；您可以决定如何以及在哪里更改字体大小。

在我们的一个应用程序中，我们有这样的需求，需要每个用户的数据。那个用户的名字有特定的元数据和独特的风格。

我们已经使用了 react-csv，但是由于 csv 的限制，我们无法在应用程序中找到 API 或控件来做同样的事情。这就是我们求助于 NPM，寻找我们能够以最快的方式达到这一要求的不同方法。

下面是一个简单的 excel js 编写器方法的例子。

```
const Excel = require('exceljs');async function exTest(){
  const workbook = new Excel.Workbook();
  const worksheet = workbook.addWorksheet("My Sheet");worksheet.columns = [
 {header: 'Id', key: 'id', width: 10},
 {header: 'Name', key: 'name', width: 32}, 
 {header: 'D.O.B.', key: 'dob', width: 15,}
];worksheet.addRow({id: 1, name: 'John Doe', dob: new Date(1970, 1, 1)});
worksheet.addRow({id: 2, name: 'Jane Doe', dob: new Date(1965, 1, 7)});// save under export.xlsx
await workbook.xlsx.writeFile('export.xlsx');//load a copy of export.xlsx
const newWorkbook = new Excel.Workbook();
await newWorkbook.xlsx.readFile('export.xlsx');const newworksheet = newWorkbook.getWorksheet('My Sheet');
newworksheet.columns = [
 {header: 'Id', key: 'id', width: 10},
 {header: 'Name', key: 'name', width: 32}, 
 {header: 'D.O.B.', key: 'dob', width: 15,}
];
await newworksheet.addRow({id: 3, name: 'New Guy', dob: new Date(2000, 1, 1)});await newWorkbook.xlsx.writeFile('export2.xlsx');console.log("File is written");};exTest();
```

这是一个针对每一行操作字体的例子。

```
let row = workSheet.addRow(rowValues);
            row.fill = {
                type: 'pattern',
                pattern:'solid',
                fgColor:{argb:'#000000'},
                bgColor:{argb:'#FF0000'}
            };
```

使用您的 UI，您可以将所有复杂的表格数据转换成非常有用的报告。

现在，我们可以将这项工作交给所有的专家来完成，只需很少的努力和人工干预，就可以提取尽可能多的数据来支持系统的发展。

## 一切听起来都很棒，但有一个问题

所有这些对我们来说都太顺利了，直到到了上线的时候，我们不得不投入生产。这是我们开始意识到在旧浏览器中对这个包的有限支持的一个缺点。

请继续关注我如何摆脱这种混乱的局面。

尽管如此，exceljs 是一个出色的库，就在今天，我在工作中使用了它。:D

快乐编码，不断学习。

和平！

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)