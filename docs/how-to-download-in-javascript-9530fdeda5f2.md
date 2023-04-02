# 如何用 JavaScript 下载文件？

> 原文：<https://javascript.plainenglish.io/how-to-download-in-javascript-9530fdeda5f2?source=collection_archive---------4----------------------->

在 Javascript 中，您是否想过如何下载从 API 发送的文件？更有趣的是，有没有想过如何下载多个文件？

让我们学习如何！

![](img/57c0387738fa9b080102627a7574d297.png)

## 先决条件

1.  在本文中，我们将考虑以下 API:“https://getmy file . com/<file id="">”</file>
2.  上面的 API 将返回一个八位字节流，它必须由客户端下载。

## 用 JavaScript 下载一个文件

**API 调用**

让我们使用**获取**来进行所需的 API 调用。我们的代码将如下所示。

```
export const downloadSignedFile = (fileId) => {return **fetch**("https://getmyfile.com/"+fileId, requestOptions)}
```

这里，我们传递要下载的文件的文件 id。而且，上面的 API 将返回文件，该文件需要下载到客户机系统中。

**响应**

我们调用上面的 **API 调用**，传递所需的文件 id。同样，这段代码是为满足我的需求和 API 设计而编写的。您当然可以修改 API 的调用方式，以适应您的应用程序。

同样，我们的 API 的响应是一个 **blob** 。因此，我使用**。blob()** 从响应中提取内容。如果您的回复是文本，您可以使用**。text()** ，提取内容，同样如此。

一旦从响应中提取出 blob/text，您需要一个下载函数来完成操作。

```
downloadSignedFile(fileId).then(response => response.blob()).then(blob => {downloadFile(blob, name)}).catch(error => console.log('error', error))
```

**下载**

我们的下载功能听起来可能有点过时。主要是因为我们没有选择任何第三方库。我们试图在没有任何第三方库的帮助下实现下载。这意味着您可以使用这段代码，而不用担心 EcmaScript 的版本。

```
export const downloadFile = (blob, name="download") => {const url = window.URL.createObjectURL(blob)const a = document.createElement('a')a.style.display = 'none'a.href = urla.download = name+".pdf"document.body.appendChild(a)a.click()window.URL.revokeObjectURL(url)setTimeout(() => {window.close()}, 5000)}
```

上面的代码接受 **blob** 并将其作为 pdf 下载到客户端。

这看起来不是很容易吗？我们可以循环运行上面的函数，一个接一个地下载任意多的文件。这里有一个如何完成循环的大纲。

```
for(let file of selectedAttachments){const fileId = file[id];
const name = file[name];downloadSignedFile(fileId).then(response => response.blob()).then(blob => {downloadFile(blob, name)}).catch(error => console.log('error', error))}
```

上面的代码在 selectedAttachments 的数组上循环。它获取 fileId，执行 API 调用，并最终下载文件。

## 用 JavaScript 下载多个文件

现在，我们希望下载多个文件并保存为**。在客户端压缩**文件。从积极的方面来说，这听起来像是一个用例，您正在努力实现它。因为，将> 2 个文件一个接一个地下载到客户的系统中是不成熟的(除非这是你的需求陈述)。

为了下载多个文件，并将它们保存为 zip 文件，我们将使用两个有趣的库。

1.  JSZip
2.  文件保存器

**安装**

首先，你必须安装 JSZip 和 FileSaver。

```
npm install jszip
npm i file-saver@1.3.2
```

**API 调用**

为了支持多个文件的下载，我们必须修改 API 调用。为什么？在压缩和下载之前，我们必须等待所有的 API 调用完成。这将是整个行动中最棘手的部分。

```
export const downloadSignedFiles = async (fileId) => {return new **Promise**((resolve) => {**fetch**("https://getmyfile.com/"+fileId, requestOptions).then((response) => response.blob()).then((blob) => {**resolve**(blob)})})}
```

这里，我们利用了 JavaScript 中“承诺”这个有趣的概念。

根据定义，**承诺在执行下一行代码之前，**可以用来等待所有的**异步**调用完成。它有两个属性:**状态**和**结果。承诺仍然是热切的，为了行动的成功完成。它总是有一个操作没有完成的原因。或者说，为什么这次行动，成功地完成了。**

修改后的 app 调用返回一个**承诺**。一旦接收到 blob 响应，它就得到**解析**。然后，将承诺返回给调用方。

**响应**

在下载多个文件的逻辑中，响应被推送到一个数组中。这个数组将存储所有的承诺，这些承诺将包含要下载的 blob。

一旦所有的承诺都被接收并存储在***download requests***中，我们必须在完成下载之前完成更多的步骤。

```
const getAllBlobs = async (downloadArray = selectedAttachments) => {let **downloadRequests** = []**;**for(let file of downloadArray){const fileId = file[id];let name = file[name];downloadRequests.push({name:name, blob:downloadSignedFiles(fileId)})}return **downloadRequests**}
```

**下载**

现在，我们需要完成下载。为此，我们必须处理存储在 downloadRequest 数组中的所有承诺。

```
const **getMegatronZip** = async (downloadArray) => {var zip = new **JSZip**();var **folder** = zip.**folder**("download");let downloadRequests = **getAllBlobs**(downloadArray);**Promise**.**all**(downloadRequests).then((response) => {response.forEach((item) => {**folder**.**file**(item.name, item.blob);})})return zip;}
```

Promise.all 的作用是接受一组承诺，处理它们，并返回一个承诺。最终的承诺将是一个数组，其中包含它处理的每个承诺的结果。如果任何一个承诺被拒绝，Promise.all 将拒绝整个操作。

在我们的例子中，downloadRequests 中的每个承诺都有下载的 blob。因此，如果您选择三个文件，将有三个已解决的承诺，有三个 blobs。我们现在要做的是将 blob 存储在一个文件中，在 zip 文件夹中。这是第一步，我们为所有要下载的文件创建一个 zip 文件。并且，我们使用 **JSZip** ，来实现这一点。

作为一名开发人员，我坚信不要重新发明轮子。当然，您可以编写自己的库来创建 zip，但是，为什么要这样做呢？当您已经有了 JSZip 来做必要的事情时。

```
**import { saveAs } from 'file-saver';**const downloadAll = async () => {let megatronBlob = await **getMegatronZip**();megatronBlob.**generateAsync**({type:"blob"}).then(function(content) {**saveAs**(content, "download.zip");});}
```

最后，我们利用**文件保护程序**，在系统中保存 zip 文件。请记住，您也可以使用同一个库在客户端保存单个文件。不过，我们正在尝试所有可能的实现方式，**用 JavaScript 下载。我想让你试试，如何使用文件保护程序下载一个文件，并在这篇文章中分享你的评论。**

**generatesync**，是 JSZip 中的一个函数，创建所需的 Zip 文件。

**saveAs** ，是一个函数，使用来自 JSZip 的 Zip 内容，并将 zip 保存在客户端。

# 下载愉快！

现在，我们已经学习了两种下载文件到客户端的方法。您可以下载单个文件，或压缩多个文件并保存。上述功能可以在任何 React、普通 JS 或 Angular 项目中实现，没有任何麻烦或争论。

*如果你喜欢这个帖子，请关注并分享，继续学习！*

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)