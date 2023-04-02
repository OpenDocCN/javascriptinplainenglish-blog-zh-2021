# 如何将 React 组件转换为图像

> 原文：<https://javascript.plainenglish.io/how-to-convert-a-react-component-to-an-image-dc081de0f431?source=collection_archive---------10----------------------->

![](img/6b4816617632144aa79a3dc6172bbe03.png)

有时，您想让用户能够以图像的形式下载 web 应用程序的一部分。在这种情况下，您需要一种将 React 组件转换为图像的方法。使用一个名为 html2canvas 的第三方 NPM 包可以很简单。让我们看看如何去做。

# 设置

我们希望首先在 HTML 标记中标记当用户点击下载按钮时要下载的 div。这可能是一个图表，用户数据，表格，或者任何我们想要的东西。我们将为该元素分配一个 id。

```
<div id="print">This will be downloaded as an image</div>
```

我们可以将它包装成一个 React 组件，并在下载按钮上附加一个事件处理程序:

```
const App = () => {
  const handleImageDownload = () => {
    // TODO: add logic here
  };
  return (
    <>
      <button type="button" onClick={handleImageDownload}>Download</button>
      <div id="print">This will be downloaded as an image</div>
    </>
  );
}
```

# 程序设计逻辑

正如我们前面讨论的，我们将安装 html2canvas NPM 包。

```
npm install html2canvas
```

然后，我们需要做的就是使用这个包获取我们想要转换成图像的相应的 div。然后，我们在内存中创建一个链接来下载图像，以编程方式单击它，然后从 DOM 中删除该链接。

```
const handleDownloadImage = () => {
    const element = document.getElementById('print'),
    canvas = await html2canvas(element),
    data = canvas.toDataURL('image/jpg'),
    link = document.createElement('a');

    link.href = data;
    link.download = 'downloaded-image.jpg';

    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
  };
```

这就是我们将 React 组件转换成图像所需要做的全部工作！希望这篇文章对你有用。

*原载于 2021 年 9 月 28 日*[*【https://www.wisdomgeek.com】*](https://www.wisdomgeek.com/development/web-development/react/how-to-convert-a-react-component-to-an-image/)*。*

*更多内容看* [***说白了。报名参加我们的***](https://plainenglish.io/) **[***免费周报***](http://newsletter.plainenglish.io/) *。关注我们关于* [***推特***](https://twitter.com/inPlainEngHQ) ，[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*，*[***YouTube***](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [***不和***](https://discord.gg/GtDtUAvyhW) *。***