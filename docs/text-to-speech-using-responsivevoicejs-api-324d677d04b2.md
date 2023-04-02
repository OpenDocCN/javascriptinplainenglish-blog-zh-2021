# 使用 ResponsiveVoiceJS API 的文本到语音转换

> 原文：<https://javascript.plainenglish.io/text-to-speech-using-responsivevoicejs-api-324d677d04b2?source=collection_archive---------14----------------------->

## 如何在只有 HTML 的网站上添加文本到语音转换

![](img/6252907acc7ece7e40c955b038185e35.png)

Photo by [Namroud Gorguis](https://unsplash.com/@namroud?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/old-cassette?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

大家好，九月好，

这一次，我们将在本教程中使用一个 HTML 文件，将文本到语音转换技术添加到您的网站中，让事情变得简单而有趣。

**我在这里使用的技术:**

*   TailwindCSS(我在另一个帖子里也写过关于 Tailwind 的内容，你可以在这里阅读快速浏览 TailwindCSS)。
*   API-responsive voice js。这是关于这项技术的[文档](https://responsivevoice.org/api/)。

好了，我们开始吧！

首先，通过 CDN 在 HTML 文件的 *< head >* 部分添加 tailwindCSS 配置，如下所示:

```
<head><meta charset="UTF-8" /><meta name="viewport" content="width=device-width, initial-scale=1.0" /><meta http-equiv="X-UA-Compatible" content="ie=edge" /><title>Text-To-Speech</title>**<link****href="https://unpkg.com/tailwindcss@^2/dist/tailwind.min.css"****rel="stylesheet"****/>**</head>
```

现在，在 HTML 文件的 *<正文>* 部分中实现 *<脚本>* 标记，如下所示:

```
<script src="https://code.responsivevoice.org/responsivevoice.js"></script><script src="https://code.jquery.com/jquery-2.1.4.min.js"></script>
```

然后按照以下步骤对**文本到语音转换**操作进行简短演示:

1.  **创建如下介绍语音按钮:**

```
***<!-- Introduction Speech Button-->***<div class="m-2"><buttonclass="component w-full border border-transparent rounded font-semibold tracking-wide text-sm px-5 py-2 focus:outline-none focus:shadow-outline bg-blue-500 text-gray-100 hover:bg-blue-600 hover:text-gray-200"onclick="responsiveVoice.speak('hello there, welcome to my digital garden!');">Play Here for Welcome Speech!</button></div>
```

对于介绍性发言，您可以更改为您希望观众在点击介绍按钮时听到的任何文本，只需更改 onclick 函数*responsive voice . peak(" some text here…")*中的文本

**2。创建带有背景音乐的文本到语音转换，如下:**

```
***<!--Speech Button with Background Music-->***<audioloop="false"width="0"height="0"id="sound"src="https://audionautix.com/Music/CryinInMyBeer.mp3"type="audio/mp3"></audio><div class="m-2"><buttonclass="component w-full border border-transparent rounded font-semibold tracking-wide text-sm px-5 py-2 focus:outline-none focus:shadow-outline bg-blue-500 text-gray-100 hover:bg-blue-600 hover:text-gray-200"onclick="responsiveVoice.speak('This example shows how to have audio play as a background while text-to-speech is active'); document.getElementById('sound').play();">Play With Background Music</button></div>
```

同样，您可以更改 onclick 函数*responsive voice . peak(" some text here…)*中的文本以及音频源。

**3。创建如下高亮文本到语音转换:**

```
***<!--Highlight Text to Speech Demo-->***<div class="m-8"><div class="bg-gray-100 shadow-sm rounded-lg p-8"><h4 class="text-center font-semibold">Highlight this text below to hear:</h4><p class="text-center">Dear Mother <br />Dear mother, <br />your love is special, <br />I cannot help but show. <br />Like flowers in a garden, <br />Your love makes me grow. <br />— Author Unknown</p></div></div>
```

***重要提示:**要使该部分工作，您需要**在<正文>结束标记**之前添加这个<脚本>标记:

```
***<!--Highligh Text to Speech Script-->***<script>function getSelectionText() {var text = "";if (window.getSelection) {text = window.getSelection().toString();} else if (document.selection && document.selection.type != "Control") {text = document.selection.createRange().text;}return text;}$(document).ready(function () {$(document).mouseup(function (e) {setTimeout(function () {responsiveVoice.cancel(); *// stop anything currently being spoken*responsiveVoice.speak(getSelectionText());}, 1);});});</script>
```

**4。创建一个小部件来编写文本到语音转换，如下所示:**

在执行此代码之前，注册并登录 ResponsiveVoice 网站获取密钥。

```
***<!--Write Text to Speech-->***<script src="[https://code.responsivevoice.org/responsivevoice.js?key=](https://code.responsivevoice.org/responsivevoice.js?key=1RVmdLT1)YOUR-KEY"></script><script src="https://code.jquery.com/jquery-2.1.4.min.js"></script><div class="m-4 text-center"><div class="m-2"><textareaclass="component w-full border bg-gray-100 px-4 py-2 text-sm tracking-wide focus:outline-none focus:shadow-outline rounded"id="text"cols="45"rows="3">Hello world</textarea></div><div class="m-2"><selectclass="component w-full border bg-gray-100 px-4 py-2 text-sm tracking-wide focus:outline-none focus:shadow-outline rounded"id="voiceselection"></select></div><div class="m-2"><inputclass="component w-full border border-transparent rounded font-semibold tracking-wide text-sm px-5 py-2 focus:outline-none focus:shadow-outline bg-blue-500 text-gray-100 hover:bg-blue-600 hover:text-gray-200"onclick="responsiveVoice.speak($('#text').val(),$('#voiceselection').val());"type="button"value="Play"/></div></div><script>var voicelist = responsiveVoice.getVoices();var vselect = $("#voiceselection");$.each(voicelist, function () {vselect.append($("<option />").val(this.name).text(this.name));});</script>
```

现在，一切都完成了，放松，坐下来享受你的工作。你也可以在这里测试一下:

他们还在开发和改进其他很酷的 SDK(软件开发工具包),你可以在这里查看他们的网站:

[](https://responsivevoice.org/) [## 响应语音文本到语音-响应语音。JS 文本到语音

### 为您的网站提供智能文本到语音转换插件。吸引观众的创造性方法！超过 51 种不同的声音和…

responsivevoice.org](https://responsivevoice.org/) 

这个简短的教程到此为止。希望你喜欢它，并发现它有用。感谢阅读！