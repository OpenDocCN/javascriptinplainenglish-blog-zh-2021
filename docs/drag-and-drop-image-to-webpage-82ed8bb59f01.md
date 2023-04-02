# 创建一个网站拖放图像上传

> 原文：<https://javascript.plainenglish.io/drag-and-drop-image-to-webpage-82ed8bb59f01?source=collection_archive---------8----------------------->

# 概观

创建一个 dropzone 元素(我使用了一个`[<main>](https://developer.mozilla.org/docs/Web/HTML/Element/main)`元素，但是您可以创建一个不同的元素):

给 dropzone 一个虚线[边框样式](https://developer.mozilla.org/docs/Web/CSS/border):

当触发`[dragenter](https://developer.mozilla.org/docs/Web/API/Document/dragenter_event)`事件时突出显示 dropzone(图像被拖动到 dropzone 上):

> `[event.preventDefault()](https://developer.mozilla.org/docs/Web/API/Event/preventDefault)`是必要的，否则图像将从您的本地文件浏览器打开。

当触发`[dragleave](https://developer.mozilla.org/docs/Web/API/Document/dragleave_event)`事件时，移除 dropzone 高亮显示(图像不再被拖动到 dropzone 上):

有必要在`drop`发生之前处理好`[dragover](https://developer.mozilla.org/docs/Web/API/Document/dragover_event)`事件:

现在处理`[drop](https://developer.mozilla.org/docs/Web/API/Document/drop_event)`事件(当图像在 dropzone 中释放时):

下面是正在发生的事情的分类:

1.  调用`event.preventDefault()`以确保文件没有在本地文件浏览器中打开(*行 4* )。
2.  dropzone 高亮显示被移除(*第 5 行*)。
3.  图像从`[event.dataTransfer.files](https://developer.mozilla.org/docs/Web/API/DataTransfer/files)` ( *行 7* )中检索。
4.  使用`[FileReader](https://developer.mozilla.org/docs/Web/API/FileReader)` ( *第 8–9 行*)将图像读取为数据 URL。
5.  当图像被加载时，[会将](https://developer.mozilla.org/docs/Web/API/ParentNode/append)附加到 dropzone 中(*第 11–15 行*)。

## 注意

拖放操作不需要`dragenter`和`dragleave`事件。它们只是为了改善用户体验。

# 链接

*   [Repl.it](https://repl.it/@remarkablemark/HTML-drag-and-drop-image)
*   [YouTube 视频](https://youtu.be/UsaXP2f0zYQ?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ)

在我的[2021–01–23 live stream](https://youtu.be/UsaXP2f0zYQ?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ)中，我讲述了如何将图像拖放到网页上:

[*本文原载于 2021 年 1 月 23 日《remarkablemark.org》。*](https://b.remarkabl.org/3o9R3TP)