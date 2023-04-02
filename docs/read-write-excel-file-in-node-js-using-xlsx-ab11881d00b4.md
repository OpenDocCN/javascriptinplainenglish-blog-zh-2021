# 使用 XLSX 在 Node.js 中读/写 Excel 文件

> 原文：<https://javascript.plainenglish.io/read-write-excel-file-in-node-js-using-xlsx-ab11881d00b4?source=collection_archive---------2----------------------->

![](img/8720e68233c0a374902000e725ab90b3.png)

Source: Image by Esa Riutta from Pixabay

不管我们作为开发人员喜欢与否，Excel 表格作为事实上的标准在商业世界中很受欢迎。有时，客户要求我们上传 excel 表格，所有的数据都应该存储在数据库中。XLSX 就是解决这个问题的节点包。在这篇文章中，我们将使用 busboy 来处理表单数据。

## 这篇文章包含两个部分:

1.  如何将 excel 表格解析成 JSON 格式？
2.  如何使用 JSON 数据创建 excel 表格？

步骤 1:使用 npm 或 bower 安装 XLSX 包

```
npm i --save xlsx 
//or
bower install js-xlsx
```

步骤 2:导入 multer 或 busboy

```
npm install --save multer
```

Multer 是一个用于处理 **multipart/form-data** 的 node.js 中间件，主要用于上传文件。它写在[勤杂工](https://github.com/mscdex/busboy)的顶部，以获得最大效率。

Busboy 是一个 Node.js 模块，用于解析传入的 HTML 表单数据。

步骤 2:在 index.js 中导入 XLSX

```
const XLSX = require('xlsx')
```

## 解析 Excel 数据

```
req.busboy.on('file', (fieldname, file, fname) => {
 if (fieldname === 'file') {
  const buffers = []
  file.on('data', (data) => {
   buffers.push(data)
  })
  file.on('end', () => {
   buffer = Buffer.concat(buffers)
   workbook = XLSX.read(buffer, {
    type: 'buffer',
   })
  })
 }
})req.busboy.on('finish', () => {
 try {
  const excelProducts =      XLSX.utils.sheet_to_json(workbook.Sheets[workbook.SheetNames[0]], {
   raw: false,
   header: 1,
   dateNF: 'yyyy-mm-dd',
   blankrows: false,
  })
 } catch (err) {
  console.log(err)
 }
})
req.pipe(req.busboy)
```

1.  使用缓冲区读取 excel 文件。我们使用 busboy 是因为这个文件是用户上传的。如果文件已经下载，可以使用 XLSX.readFile(文件名:string，opts？:ParsingOptions)。
2.  XLSX.utils.sheet_to_json()用于将工作表数据读入数组对象。传递其他选项以指定不同的参数，如使用原始值(true)或格式化字符串(false)，在输出中包含空行，默认日期格式，如果指定了标题，则第一行被视为数据行，否则第一行是标题行，而不被视为数据。

`XLSX.utils`中的一些辅助功能生成不同的表单视图:

*   `XLSX.utils.sheet_to_csv`生成 CSV
*   `XLSX.utils.sheet_to_txt`生成 UTF16 格式的文本
*   `XLSX.utils.sheet_to_html`生成 HTML
*   `XLSX.utils.sheet_to_json`生成一个对象数组
*   `XLSX.utils.sheet_to_formulae`生成公式列表

**创建 Excel 表**

```
data = [{
 firstName: 'John',
 lastName: 'Doe'
}, {
 firstName: 'Smith',
 lastName: 'Peters'
}, {
 firstName: 'Alice',
 lastName: 'Lee'
}]const ws = XLSX.utils.json_to_sheet(data)
const wb = XLSX.utils.book_new()
XLSX.utils.book_append_sheet(wb, ws, 'Responses')
XLSX.writeFile(wb, 'sampleData.export.xlsx')
```

1.  **json_to_sheet** 将 JavaScript 对象的数组转换成工作表。还有其他方法可以将数据转换成工作表，如 aoa_to_sheet、table_to_sheet。sheet_add_json 用于将一组 JavaScript 对象添加到现有的工作表中。
2.  在工作表中创建新的工作簿。
3.  **book_append_sheet** 将工作表附加到名为“响应”的工作簿。
4.  **XLSX.writeFile** (wb，' sampleData.export.xlsx ')**试图将 wb 写入' sampledata . export . xlsx '。**

**您还可以指定每列的宽度&也可以合并单元格。**

**一些帮助功能`XLSX.utils`用于将不同的数据导入工作表:**

*   **`XLSX.utils.aoa_to_sheet`将 JavaScript 数据数组转换为工作表。**
*   **`XLSX.utils.json_to_sheet`将 JavaScript 对象数组转换为工作表。**
*   **`XLSX.utils.table_to_sheet`将 DOM TABLE 元素转换为工作表。**
*   **`XLSX.utils.sheet_add_aoa`将 JavaScript 数据数组的数组添加到工作表中。**
*   **`XLSX.utils.sheet_add_json`将 JavaScript 对象数组添加到工作表中。**

## **结论:**

**使用 XLSX 软件包，您可以读取任何 excel 文件，也可以创建一个 excel 文件。**

*****感谢阅读。*****

***更多内容参见* [***通俗易懂***](http://plainenglish.io/)**