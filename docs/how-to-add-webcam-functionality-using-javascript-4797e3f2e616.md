# 如何使用 JavaScript 添加网络摄像头功能

> 原文：<https://javascript.plainenglish.io/how-to-add-webcam-functionality-using-javascript-4797e3f2e616?source=collection_archive---------6----------------------->

## 让我们使用 JavaScript 将网络摄像头集成到网页中。

![](img/b166bd17920c1c659f3394141b5d9294.png)

Photo by [Chris Montgomery](https://unsplash.com/@cwmonty?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如今，许多网站都集成了实时网络摄像头，用于个人资料图片上传、验证、在线通话或流媒体等用途。所以这是一个很好的功能，可以放在你的网站或网络应用上。

在本文中，我们将学习如何使用普通 JavaScript 将网络摄像头集成到网页中。所以让我们开始吧。

# HTML 结构

为了使用 JavaScript 访问网页中的用户摄像头，我们首先需要使用 HTML 标签`<video>`。这是我们将显示网络摄像头输出的地方。

```
**<video autoplay></video>**
```

因此，让我们创建一个简单的 HTML 结构，其中包含标签`<video>`和两个按钮(开始和停止)，这将允许我们停止和启动网络摄像头。

```
<body>
  <div class="container">
    **<video autoplay></video>**

    <div class="buttons">
      <button **onclick="startWebCam()"**>Start</button>
      <button **onclick="StopWebCam()"**>Stop</button>
    </div></div>
</body>
```

如你所见，这是一个简单的 HTML 结构。现在我们需要在 JavaScript 中创建两个函数`startWebCam`和`stopWebCam`。

# JavaScript 部分

为了访问网络摄像头，我们将使用 [navigator](https://developer.mozilla.org/en-US/docs/Web/API/Navigator) web API。

这个 API 有很多功能，比如访问网络摄像头、音频、设备屏幕、设备内存等等。

首先，我们需要选择视频元素:

```
const video = document.querySelector('video');
```

现在，让我们创建函数`startWebCam`来访问和显示视频标签中的摄像头输出。

下面是代码示例:

```
const startWebCam = () =>{

if (**navigator.mediaDevices.getUserMedia**) {     **navigator.mediaDevices.getUserMedia**({ **video: true** })
  .**then**(stream => video.srcObject = stream)
  .**catch**(error => console.log(error));
 }
}
startWebCam();
```

正如你在上面看到的，我们使用了`navigator.mediaDevices.getUserMedia`来获得用户访问带有视频轨道选项的网络摄像头的许可。这就是为什么我们通过`{video: true}`来告诉我们想要访问网络摄像头，而不是音频。

方法`getUserMedia()`返回一个承诺，当用户允许访问网络摄像头时解决，当用户拒绝权限时拒绝。这就是为什么我们使用`.then`和`.catch`来处理承诺。

现在让我们创建一个函数`stopWebCam()`,当点击*停止*按钮时，停止视频轨道并关闭网络摄像头。

下面是代码示例:

```
// Stop the webcam.
const StopWebCam = ()=>{
  let stream = video.srcObject;
  let tracks = stream.getTracks();
  **tracks.forEach(track => track.stop());**
  video.srcObject = null;
}
```

就是这样，这就是我们如何将网络摄像头集成到网页中。现在我们只需要添加一些 CSS。

# 基本 CSS

让我们添加一个简单的样式表来设置 HTML 元素的样式。看看下面的 CSS:

```
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body{
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-top: 25px;
}
video{
    max-width: 600px;
    height: auto;
    border: 5px solid black;
}
.buttons{
    display: flex;
    justify-content: center;
}
button{
    padding: 12px 25px;
    margin: 0 10px;
    cursor: pointer;
    font-size: 16.5px;
    font-weight: bold;
    background: cyan;
    outline: none;
    border: 1px solid black;
}
```

如果您有网络摄像头，您可以在下面的代码栏中查看该项目:

Codepen by author.

如果网络摄像头功能不工作，只需点击上方的*在 Codepen 上编辑*即可在 Codepen 上查看项目。

# 结论

如您所见，这只是一个使用香草 JavaScript 将网络摄像头集成到网页中的简单示例。如果你感兴趣，你可以了解更多。

谢谢你阅读这篇文章。我希望你发现它有用。

**更多读数**

[](/6-useful-pure-css-tips-that-you-should-know-647ccaff201e) [## 6 个您应该知道的有用的纯 CSS 技巧

### 非常有用的 CSS 技巧，你可能不知道

javascript.plainenglish.io](/6-useful-pure-css-tips-that-you-should-know-647ccaff201e) 

*更内容于* [***通俗地说就是***](https://plainenglish.io/)