# 如何使用 React 建立图像压缩网站

> 原文：<https://javascript.plainenglish.io/image-compressor-website-using-react-9c7e631147ac?source=collection_archive---------10----------------------->

近年来，图像在网站和应用程序中的使用呈指数级增长。此外，由于新型智能手机和相机的高相机质量，图像尺寸也随着它们的质量而增加。

如果你的图片太大，那么你的网站可能会花太多时间来加载。因此，优化不仅要考虑 SS 和 JavaScript，还要考虑图像。这将确保你的访客有一个良好的体验。

![](img/4c6393f94c49af15c380ba6169a4fe00.png)

# 如何用 React 搭建一个图像压缩网站？

在本文中，我将帮助您使用 React 模块创建自己的图像压缩网站。你可以看到并使用图像压缩网站，我们将从下面的链接建设。

 [## 图像压缩器

### 使用 React 构建图像压缩网站

imagecompressor.netlify.app](https://imagecompressor.netlify.app/) 

如果你在创建这个网站时遇到困难，你可以从知识库中获得帮助。

[](https://github.com/mechiragjain/Image-Compressor) [## mechiragjain/图像压缩器

### 这是一个使用 React.js 包 browser-image-compressor 开发的图像压缩应用程序。这张在线图片…

github.com](https://github.com/mechiragjain/Image-Compressor) 

# 创建 React 应用

通过运行 create-react-app 命令开始构建您的项目，如下所示。

```
npx create-react-app image-compressor
```

# 安装软件包

```
npm i browser-image-compression bootstrap react-bootstrap react-dom
```

*   browser-image-compression 是一个 JavaScript 模块，用于在 web 浏览器中压缩图像。
*   安装 bootstrap 和 react-bootstrap 是为了使用 Bootstrap 设计我们的网站。
*   react-dom:这个包充当 react 的 dom 和服务器呈现器的入口点。

# 密码

*   在“src”文件夹下创建“组件”和“图像”文件夹。
*   在“Components”文件夹中创建两个文件——“compressor . js”和“Compressor.css”。
*   下载两张在网站上显示上传和下载图标的图片— [从这里下载](https://github.com/mechiragjain/Image-Compressor/tree/master/src/Images)并移动到项目的“图片”文件夹中。

现在更新您的 **app.js** 文件，将 Compressor 组件包含在其中。

*app.js*

```
import React from 'react';
import './App.css';import Compressor from "./Components/Compressor";function App() {
  return (
    <Compressor />
  );
}export default App;
```

*Compressor.js*

导入我们将在 Compressor.js 文件中使用的依赖项和其他组件。

```
import React, {useState} from 'react';
import imageCompression from "browser-image-compression";
import './Compressor.css';
import Download from 'img/Download.png';
import Upload from 'img/Upload.png';
import {Navbar, Card} from "react-bootstrap";
import { FontAwesomeIcon } from '@fortawesome/react-fontawesome';
import { faImage } from '@fortawesome/free-solid-svg-icons';function Compressor(){
  return(
    <div></div>
  )
}export default Compressor;
```

*   如前所述，imageCompressor 是一个组件，我们将使用它来压缩上传到网站的图像。
*   在第 4 行和第 5 行，我们从 Images 文件夹中导入上传和下载图标。
*   在下一行，从 Bootstrap 包导入 NavBar 和 Card 组件。
*   导入该文件中使用的字体图标。

## 压缩机功能

这是我们从 Compressor.js 文件中导出的函数。在这个函数中，我们将写出压缩图像的逻辑。

因此，在创建子函数之前，让我们添加一些状态来管理压缩图像和原始图像的链接，存储文件名，并检查用户是否上传了图像或单击了压缩按钮。

在 Compressor()函数中，在 return 语句之前的顶部添加以下代码。

```
const [compressedLink, setCompressedLink] = useState("");
const [originalImage, setOriginalImage] = useState("");
const [originalLink, setOriginalLink] = useState("");
const [clicked, setClicked] = useState(false);
const [uploadImage, setUploadImage] = useState(false);
const [outputFileName, setOutputFileName] = useState("");
```

我们将在 Compressor 函数中创建的函数有:

*   uploadLink —处理 URL 的上传部分
*   单击—当用户单击压缩按钮时触发，压缩图像。

***uploadLink()函数***

在 Compressor()函数中创建此函数。一旦你上传一张图片到网站上，这个函数就会被触发。我们将上传图像的细节作为参数传递给这个函数。通过这个参数，我们将提取图像文件的细节。获得图像文件后，我们将创建一个 URL 来表示上传的图像。

```
function uploadLink(event){
  //To get the image file which user had uploaded in the input field
  const imageFile = event.target.files[0];

  // Create a DOMString containing a URL that represents the imageFile
  setOriginalLink(URL.createObjectURL(imageFile));

  //Now set the original image link, name of output file and upload image state
  setOriginalImage(imageFile);
  setOutputFileName(imageFile.name);
  setUploadImage(true);
}
```

***点击()功能***

在 *uploadLink()* 函数下添加该函数。当用户上传图像后按下压缩按钮时，这个函数将被调用。

在这个函数中，我们将使用从模块或包中导入的 *imageCompression* 组件来压缩原始图像。

```
function click(e){
  e.preventDefault(); //*You should provide one of maxSizeMB, maxWidthOrHeight in the options* that will be passed to imageCompression component.
const options = 
{ 
  maxSizeMB: 3, 
  maxWidthOrHeight: 800, 
  useWebWorker: true 
}; if (options.maxSizeMB >= originalImage.size / 1024) { 
  alert("Bring a bigger image"); 
  return 0; 
} //this code will compress the original image 
let output; 
imageCompression(originalImage, options).then(x => { 
output = x; 
const downloadLink = URL.createObjectURL(output); setCompressedLink(downloadLink); 
}); 
setClicked(true); return 1; };
```

您已经完成了压缩图像所需执行的逻辑。现在您必须在 *Compressor()* 函数的返回语句中添加几行代码。将添加到该语句中的代码将在用户的前端得到反映。

```
<div className="mainContainer">
      <Navbar className="navbar justify-content-center" bg="light" variant="light">
        <Navbar.Brand className="navbar-content" href="/">
          <FontAwesomeIcon className="social-icons changeOn" icon={faImage} size={1} />{' '}
          Image Compressor
        </Navbar.Brand>
      </Navbar> <div className="row mt-5">
          <div className="col-xl-4 col-lg-4 col-md-12 col-sm-12">
            {uploadImage ? (
              <Card.Img
                className="image"
                variant="top"
                src={originalLink}
              ></Card.Img>
            ) : (
              <Card.Img
                className="uploadCard"
                variant="top"
                src={Upload}
              ></Card.Img>
            )}
            <div className="d-flex justify-content-center upload-btn-wrapper">
            <button class="btn btn-dark">Upload a file</button>
              <input
                type="file"
                accept="image/*"
                className="mt-2 btn btn-dark w-75"
                onChange={event => uploadLink(event)}
              />
            </div>
          </div> <div className="col-xl-4 col-lg-4 col-md-12 mb-5 mt-4 col-sm-12 d-flex justify-content-center align-items-baseline">
            <br />
            {outputFileName ? (
              <button
                type="button"
                className=" btn btn-dark"
                onClick={e => click(e)}
              >
                Compress
              </button>
            ) : (
              <></>
            )}
          </div> <div className="col-xl-4 col-lg-4 col-md-12 col-sm-12 mt-3">
            <Card.Img className="image" variant="top" src={compressedLink}></Card.Img>
            {clicked ? (
              <div className="d-flex justify-content-center">
                <a
                  href={compressedLink}
                  download={outputFileName}
                  className="mt-2 btn btn-dark w-75"
                >
                  Download
                </a>
              </div>
            ) : (
              <Card.Img
                className="uploadCard"
                variant="top"
                src={Download}
              ></Card.Img>
            )}
        </div>
    </div>
</div>
```

# 设计你的网站

从资源库链接中复制 CSS 文件内容，并将其粘贴到您的 CSS 文件中，以设计您的网站。

[点击这里](https://github.com/mechiragjain/Image-Compressor/blob/master/src/Components/Compressor.css)查看 CSS 文件。

# 运行 React 应用

运行 React 应用程序来测试您的图像压缩器网站。您可以在终端的图像压缩目录中键入以下命令。

```
npm start
```

你会看到一个类似的网站，如下图所示。

> **注意** —如果你的代码不能正常工作，那么检查你是否错过了任何步骤。或者你可以通过下面的链接查看完整的代码。

[https://github.com/mechiragjain/Image-Compressor](https://github.com/mechiragjain/Image-Compressor)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)