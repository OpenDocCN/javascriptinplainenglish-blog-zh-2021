# 7 个有趣的反应钩⚛️

> 原文：<https://javascript.plainenglish.io/7-interesting-react-hooks-%EF%B8%8F-d7f686811044?source=collection_archive---------5----------------------->

## 钩子的引入增强了我们为状态、组件生命周期和 reducer 编写 React 代码的方式。

![](img/be293619338c3176fc797065d40c6c7a.png)

Photo by [Jan Zinnbauer](https://unsplash.com/@jan_zinnbauer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/link-chain?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

在本文中，我介绍了 7 个有趣的 React 挂钩，值得在 React 项目中尝试。

## 1.使用声音

useSound 挂钩是我发现的最有趣的挂钩之一。我在我的[博客](https://chetanraj.in/blog/)中使用过这个钩子——当点击标题右上角的切换主题【亮/暗】图标时。它会发出开关声🔊这个挂钩将网站提升了一个级别🔥。这个钩子可以用来通知新来的消息，也可以用来滚动。😂

**用途**

安装库— `npm install use-sound --save`并导入— `import useSound from 'use-sound';`

**示例**

## 2.使用标记模式

useDarkMode 是[反应配方](https://github.com/craig1123/react-recipes)的挂钩之一😋这个钩子可以在亮☀️和暗之间切换🌙网站主题的模式。切换模式后，它将选择的值存储在本地存储器中。用户的首选模式将被保存在浏览器中，直到用户明确删除它。

**用法**

安装库— `npm install react-recipes --save`并导入— `import { useDarkMode } from "react-recipes";`

**示例**

基本上，`**useDarkMode()**`返回两件事。

*   **黑暗模式**:当黑暗模式激活时，布尔值为真。
*   **setDarkMode** :在亮暗模式之间切换。

## 3.使用语音识别

[useSpeechRecognition](https://github.com/JamesBrill/react-speech-recognition) 挂钩允许从用户的麦克风访问讲话的抄本。它使用幕后的网络语音 API🙌这个钩子可以用来构建你自己的语音助手🤖

**用法**

安装库— `npm install react-speech-recognition --save`并导入— `import SpeechRecognition, { useSpeechRecognition } from 'react-speech-recognition';`

**示例**

## 4.useWhyDidYouUpdate

使用 [useWhyDidYouUpdate](https://usehooks.com/useWhyDidYouUpdate/) 可以很容易地看到哪个道具发生了变化🤔这导致组件重新呈现🔁

**用法**

**🔗挂钩**

**例子**

## 5.使用以前的

[usePrevious](https://usehooks.com/usePrevious/) 钩子使用 refs 在内部存储以前的值。这个钩子可以用在有撤销按钮的用例中。

**用途**

**🔗挂钩**

**示例**

## 6.使用点击外部

[useOnClickOutside](https://github.com/Andarist/use-onclickoutside/) 钩子用于检测一个元素外部的点击，这个钩子对于当在一个模态之外点击时关闭这个模态，当下拉菜单打开时关闭它是非常有用的。

**用法**

安装库 **—** `npm install use-onclickoutside --save`导入— `import useOnClickOutside from 'use-onclickoutside';`

**示例**

## 7.使用主题

useTheme 挂钩使得使用 CSS 变量动态改变应用程序的外观变得容易。这是样式化组件或任何其他 CSS-in-JS 框架的轻量级替代方案。在这个钩子中，只需传入一个包含需要更新的 CSS 变量的键/值对的对象，钩子就会更新文档根元素中的每个变量。查看 [CodeSandbox 演示](https://codesandbox.io/s/15mko9187?file=/src/index.js)中更有趣的例子，也可以查看样式表。

**用途**

**🔗挂钩**

**示例**

感谢您花时间阅读这篇文章！🙏

*更多内容请看*[*plain English . io*](http://plainenglish.io/)