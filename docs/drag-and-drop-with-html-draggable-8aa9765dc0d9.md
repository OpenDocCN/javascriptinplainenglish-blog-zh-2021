# 使用 HTML draggable 拖放

> 原文：<https://javascript.plainenglish.io/drag-and-drop-with-html-draggable-8aa9765dc0d9?source=collection_archive---------14----------------------->

我在我的[2021–01–18 live stream](https://youtu.be/hCsuyZHlUtY?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ)中学习了使用 HTML5 [draggable](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#draggableattribute) 属性的[拖放](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API):

# 我学到了什么

## 可拖动的

将 [draggable](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#draggableattribute) 设置为`true`以使元素可拖动:

## 拖拽启动

使用`[dragstart](https://developer.mozilla.org/en-US/docs/Web/API/Document/dragstart_event)`事件属性设置[拖动数据](https://developer.mozilla.org/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations#dragdata):

或者使用 JavaScript 添加事件监听器:

## 德拉戈夫

使用`[dragover](https://developer.mozilla.org/docs/Web/API/Document/dragover_event)`事件属性来阻止默认动作:

或者使用 JavaScript 添加事件监听器:

## 滴

使用`[drop](https://developer.mozilla.org/docs/Web/API/Document/drop_event)`事件属性来阻止默认动作:

或者使用 JavaScript 添加事件监听器:

# 链接

*   [Repl.it](https://repl.it/@remarkablemark/HTML-draggable)
*   [YouTube 视频](https://youtu.be/hCsuyZHlUtY?list=PLVgOtoUBG2mdLpj6qT5DXfg5_pGPTDrJZ)
*   [W3docs](https://www.w3docs.com/learn-html/html-draggable-attribute.html)
*   [MDN 网络文档](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API/Drag_operations)

[*本文原载于 2021 年 1 月 18 日《remarkablemark.org》。*](https://b.remarkabl.org/2M7oTM8)