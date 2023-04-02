# 在 React 中上传之前压缩图像

> 原文：<https://javascript.plainenglish.io/compression-images-before-upload-in-a-react-app-with-react-image-file-resizer-c1870c9bcf47?source=collection_archive---------2----------------------->

![](img/ce3af98c453f958a848c53022692e903.png)

Photo by [Viktor Talashuk](https://unsplash.com/@viktortalashuk?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

React 图像文件 Resizer 允许我们在上传图像之前对其进行压缩和操作。

在本文中，我们将看看如何在上传到 React 应用程序之前处理我们的图像。

# 装置

我们可以通过运行以下命令来安装该软件包:

```
npm i react-image-file-resizer
```

或者

```
yarn add react-image-file-resizer
```

# 压缩和处理图像

我们可以压缩和操作我们从文件输入中选择的图像。

为此，我们写道:

```
import React from "react";
import Resizer from "react-image-file-resizer";const resizeFile = (file) =>
  new Promise((resolve) => {
    Resizer.imageFileResizer(
      file,
      300,
      400,
      "JPEG",
      80,
      0,
      (uri) => {
        resolve(uri);
      },
      "base64"
    );
  });export default function App() {
  const onChange = async (event) => {
    const file = event.target.files[0];
    const image = await resizeFile(file);
    console.log(image);
  }; return (
    <div className="App">
      <input onChange={onChange} type="file" />
    </div>
  );
}
```

我们有`resizeFile`函数，它获取图像文件并返回调整文件大小和压缩文件的承诺。

第一个参数是 file 对象。

第二个和第三个是宽度和高度。

第四个是要转换的格式。

5 是图像质量从 0 到 100。

第六是图像的旋转。

第七个是用于获得新图像 URI 的函数。

8 号是格式。

最小宽度和高度需要两个以上的参数。

在`onChange`处理程序中，我们从文件输入中获取文件。

一旦我们做到了这一点，我们就可以进行上传。

# 上传文件

为了上传文件，我们编写:

```
import React from "react";
import Resizer from "react-image-file-resizer";const resizeFile = (file) =>
  new Promise((resolve) => {
    Resizer.imageFileResizer(
      file,
      300,
      400,
      "JPEG",
      80,
      0,
      (uri) => {
        resolve(uri);
      },
      "base64"
    );
  });const dataURIToBlob = (dataURI) => {
  const splitDataURI = dataURI.split(",");
  const byteString =
    splitDataURI[0].indexOf("base64") >= 0
      ? atob(splitDataURI[1])
      : decodeURI(splitDataURI[1]);
  const mimeString = splitDataURI[0].split(":")[1].split(";")[0]; const ia = new Uint8Array(byteString.length);
  for (let i = 0; i < byteString.length; i++) ia[i] = byteString.charCodeAt(i); return new Blob([ia], { type: mimeString });
};export default function App() {
  const onChange = async (event) => {
    const file = event.target.files[0];
    const image = await resizeFile(file);
    console.log(image);
    const newFile = dataURIToBlob(image);
    const formData = new FormData();
    formData.append("image", newFile);
    const res = await fetch(
      "https://run.mocky.io/v3/c5189845-2a93-49aa-85c7-70bc64e8af90",
      {
        method: "POST",
        body: formData
      }
    );
    const data = await res.text();
    console.log(data);
  }; return (
    <div className="App">
      <input onChange={onChange} type="file" />
    </div>
  );
}
```

我们添加了`dataURItoBlob`函数来将 base64 字符串转换回文件。

它遍历从 base64 字符串创建的字节字符串，并将其放入 Uint8Array 中。

然后放在`Blob`构造函数中返回文件对象。

一旦我们这样做了，我们就把它放在`FormData`构造函数中。

然后我们用`fetch`功能上传。

# 结论

我们可以在用 React 图像文件 Resizer 包将图像上传到 React 应用程序之前对其进行压缩和调整大小。