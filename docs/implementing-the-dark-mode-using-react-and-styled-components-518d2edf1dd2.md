# 使用 React 和 Styled 组件实现黑暗模式

> 原文：<https://javascript.plainenglish.io/implementing-the-dark-mode-using-react-and-styled-components-518d2edf1dd2?source=collection_archive---------10----------------------->

## React 中的黑暗模式功能变得简单。

![](img/0ec5b971d1036e3fc91b5e119ddf879b.png)

Photo by [Jefferson Santos](https://unsplash.com/@jefflssantos?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在现代网络中，黑暗模式功能是非常有用和重要的。对用户体验也有好处。很多人更喜欢黑暗模式功能，因为它可以在晚上浏览网页时保护他们的眼睛。

在本文中，我们将学习使用 React 和 styled-components 轻松实现黑暗模式。所以让我们开始吧。

# 项目设置

因为我们要创建一个非常简单的黑暗模式功能，我们将使用 create-react-app 工具。因此，您需要做的第一件事是使用该工具建立一个 React 项目。

然后，转到项目目录，打开终端，使用下面的命令安装 styled-components 包:

```
npm install styled-components
```

如果您正在使用 Yarn，您可以键入以下命令:

```
yarn add styled-components
```

在软件包安装之后，您将能够毫无问题地在代码中导入样式化的组件。

# 项目代码

我们需要做的第一件事是为我们的主题创建一个文件。黑暗主题和光明主题。我们还将使用样式化组件在该文件中设置一些全局样式。

我们将该文件称为`theme.js`，它将包含两个具有深色主题和浅色主题属性的对象。除此之外，我们还将在样式组件中使用道具，根据我们所处的主题(暗/亮)来改变颜色和背景。

下面是代码示例:

```
*//theme.js***import {createGlobalStyle} from "styled-components"**export const **darkTheme** = {
  body: "#000",
  textColor: "#fff",
  headingColor: "lightblue"
}export const **lightTheme** = {
  body: "#fff",
  textColor: "#000",
  headingColor: "#d23669"
}export const **GlobalStyles** = createGlobalStyle`
 body {
  background: ${**props => props.theme.body**};
  color: ${**props => props.theme.textColor**};
  transition: .3s ease;
 }
 h2{
   color: ${**props => props.theme.headingColor**};
 }
`
```

这就是我们的主题。现在，在应用程序组件中，我们将有一个按钮在亮暗主题之间切换。我们将使用状态挂钩来切换主题。

我们根据状态在黑暗和光明之间切换。

下面是代码示例:

```
//App.jsimport React, { useState } from "react";
import "./styles.css";
import { **ThemeProvider** } from "styled-components";
import { darkTheme, lightTheme, GlobalStyles } from "./theme";function App() {
  **const [theme, setTheme] = useState("light");**const switchTheme = () => {
    **theme === "light" ? setTheme("dark") : setTheme("light");**
  };return (
    **<ThemeProvider** theme={theme === "light" ? lightTheme : darkTheme}**>**
      **<GlobalStyles />**
      <div className="App">
        <h1>Hello bro!</h1>
        <button onClick={**switchTheme**}>Switch Theme</button>
      </div>
    **</ThemeProvider>**
  );
}
export default App;
```

正如你在上面看到的，我们根据状态在主题之间切换。我们从 styled-components 导入了主题提供程序，以便根据状态值为我们的应用程序提供正确的主题。现在你可以通过点击按钮在深色和浅色主题之间切换。

如果你想看看源代码，这里有 [CodeSandbox](https://codesandbox.io/s/youthful-brown-3j9yl?file=/src/App.js) 。

# 结论

如您所见，使用样式化组件非常简单。如果你愿意，你甚至可以创建一个复杂的主题。因此，您可以在页面上为每种模式切换不同颜色的深色和浅色主题。

感谢您阅读这篇文章。希望你觉得有用。

**更多阅读:**

[](/the-difference-between-var-let-and-const-in-javascript-630b5a8bb1c5) [## JavaScript 中 var、let 和 const 的区别

### 用例子解释 JavaScript 中的变量声明关键字。

javascript.plainenglish.io](/the-difference-between-var-let-and-const-in-javascript-630b5a8bb1c5) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)