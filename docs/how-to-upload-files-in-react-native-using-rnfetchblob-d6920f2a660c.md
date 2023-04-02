# 如何在 React Native 中上传文件

> 原文：<https://javascript.plainenglish.io/how-to-upload-files-in-react-native-using-rnfetchblob-d6920f2a660c?source=collection_archive---------5----------------------->

## 关于如何在 React Native 中处理多部分请求的完整指南

![](img/ebcecf1904acf17a821ca65bb14f97f8.png)

Photo by [Fotis Fotopoulos](https://unsplash.com/@ffstop?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

RNFetchBlob 是一个库，它的目的是让 React 本地开发人员在处理二进制数据传输时更加轻松。

为了安装它，运行

```
npm install --save rn-fetch-blob
```

或者

```
yarn add rn-fetch-blob
```

在你的终端里。

然后转到您的`ios`目录并运行`pod install`。

在这篇文章中，我们将研究上传文件。别担心，会有一个[不同的](https://bianca-dragomir.medium.com/downloading-files-in-react-native-with-rnfetchblob-f78b18b46a36)将文件下载到设备上。

`record`对象包含了将要上传的文件的基本信息:

```
export interface MedicalRecord {
  description: string;
  file: File;
}export interface PatientFile {
  name: string;
  url: string; // the path to the local file
  size: number;
}
```

很简单，对吧？

让我们来分解这个片段:

您的后端可能需要某种形式的授权。您将通过 headers 参数来提供它。在上面的代码片段中，`defaultHeaders`构建了一个地图，该地图将包含例如`Authorization`字段(Bearer …)。通知您的后端这个请求是多部分的也是非常重要的。这就是第 8 行的目的:

```
headers[‘Content-Type’] = ‘multipart/form-data’;
```

2.根据平台的不同，需要以不同的方式构建路径。Android 将能够理解文件选择库返回的路径，但 iOS 增加了一点趣味:

```
decodeURIComponent(record.file.url.replace('file://', ''))
```

3.您的`multipartParams`列表将包含 2 个对象:

*   第一个将提供文件本身:

```
{
  name: "file",
  filename: record.file.name,
  data: RNFetchBlob.wrap(realPath),
},
```

将使用 RNFetchBlob 包装数据路径。该字段的默认名称是“文件”。在这里，你必须考虑到你的后端将期待什么。例如，正如您在要点中看到的，我们的后端需要“files.file”命名。我花了一段时间来找出为什么它不工作，我不想你在这上面浪费时间。

*   第二个对象将包含您希望随文件一起发送的附加数据。

```
{
  name: "data",
  data: JSON.stringify({
    date: date,
    description: description,
  }),
},
```

再次提醒，小心你的`name`领域。将其命名为`data`向库发出信号，这确实是将要上传的额外数据。不然它就不知道怎么解读了。

4.这个`fetch`电话很容易掌握。第一个参数将是请求的类型(在代码片段中，如果我们向函数提供一个现有的 recordId，我们将执行一个`put`请求；如果没有提供 Id，我们将执行一个基本的`post`请求。第二个参数应该是 API URL，第三个包含标题，第四个包含`multipartParams`列表。

## 结论

让我们感谢这个图书馆的创建者。他们卸下了我们肩上的重担，创建了一个强大的库，为我们节省了很多时间。

请继续关注我向您承诺的内容:如何在 React Native 上挑选文件，以及如何使用 RNFetchBlob 下载文件。

*更多内容看*[***plain English . io***](https://plainenglish.io/)