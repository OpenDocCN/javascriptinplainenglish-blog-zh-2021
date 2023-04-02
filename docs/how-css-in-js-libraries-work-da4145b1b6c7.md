# CSS-in-JS 库如何工作

> 原文：<https://javascript.plainenglish.io/how-css-in-js-libraries-work-da4145b1b6c7?source=collection_archive---------6----------------------->

## 用样式化组件描述的 CSS-in-JS 库的内部

![](img/1fbe141e22ff128ef3c2260922251246.png)

Photo by [KOBU Agency](https://unsplash.com/@kobuagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

让我们看一个如何用样式化组件来样式化`div`的例子。

```
import styled from 'styled-components'; const AwesomeStyledDiv = styled.div`  
    width: 20px;  
    height: 10px;  
    background-color: blue; 
`
```

在上面的例子中，我们已经:

1.  从名为`styled`的样式组件中导入了一些东西。
2.  定义了 HTML 元素的样式，在这里是一个`div`。
3.  给这个`div`增加了一些造型。

`AwesomeStyledDiv`现在可以像项目中定义的任何其他 React 组件一样使用。

如果您曾经使用过样式化组件，那么您可能已经写了几百遍这样的东西，但是您是否想过这个语法是如何被翻译成样式化的`div`？

# 那些逆记号是关于什么的？

您很可能只在 ES6 中使用模板文字时使用反斜线，比如:

```
const greeting = `hello ${name}!`;
```

还有一种更高级的模板文字形式，称为“标记模板文字”。标记模板允许你用模板文本调用一个函数。以这种方式调用时，函数被称为“标记函数”。

大多数情况下，您会像这样调用函数:

```
const logFirstArgument = (arg1) => {   
    console.log(arg1); 
} logFirstArgument('call me');  // output: 'call me'
```

但是你知道你也可以不用花括号调用这个函数，而是用一个模板文字吗？(在你的 chrome 主机上试试这个)。

```
logFirstArgument`call me`; // output: [ 'call me' ]
```

这两种调用函数的方式之间唯一的区别是参数如何传递给函数。注意，对于带标签的模板，我们的第一个参数被包装在一个数组中！这里有一点很重要，这里没有什么 babel/webpack 魔法，这个语法是 ES6 的一部分。

# 当用模板文字调用函数时，参数是如何解释的？

在上面的例子中，我们注意到当我们用一个模板文本调用一个函数时，传递给函数的字符串被包装到一个数组中(很快会有更多的介绍)。

当我们试图用一个有“插值”的模板文字调用一个函数时，事情变得更加有趣了(正如我们在上面看到的，类似于``hello ${name}``)。

```
const readerName = 'reader';const logFirstAndSecondArguments = (arg1, arg2) => {
  console.log(arg1);
  console.log(arg2);
}logFirstAndSecondArguments`call me ${readerName}`// output:
// [ 'call me ', '' ]
// 'reader'
```

这看起来可能有点吓人，但事实是:

1.  第一个参数是我们的`readerName`占位符周围的一个数组‘split’。
2.  第二个参数是`readerName`占位符中的表达式，在本例中，它是一个解析为`'reader'`的变量。

你添加到字符串中的任何额外的插值都会做同样的事情:

1.  第一个参数将围绕**所有占位符“拆分”。**
2.  后续参数将接收传递给每个附加占位符的表达式。

```
const firstName = 'reader';
const lastName = 'readerHead';const logFirstSecondThirdArguments = (arg1, arg2, arg3) => {
  console.log(arg1);
  console.log(arg2);
  console.log(arg3);
}logFirstSecondThirdArguments`first name: ${firstName}, lastname: ${lastName}`// output:
// [ 'first name: ', ', lastname: ', '' ]
// 'reader'
// 'readerHead'
```

# 如果我们的占位符包含一个函数会发生什么？

既然我们可以在占位符中传递任何表达式，那么让我们看看当我们传递一个函数时会发生什么；

```
const readerName = 'reader';
const logFirstAndSecondArguments = (arg1, arg2) => {
  console.log(arg1);
  console.log(arg2);
  console.log(arg2());
}const returnHello = () => 'hello'logFirstAndSecondArguments`call me ${returnHello}`// output
// [ 'call me ', '' ]
// ƒ returnHello()
// 'hello'
```

这里真正酷的事情是我们可以在`logFirstAndSecondArguments`函数中访问`returnHello`函数(并且它可以被调用)!这种学习对于如何设计组件和工作是至关重要的。

# 这很好，但是为什么我们要再次讨论这个问题，它对样式化组件有什么帮助？

让我们回到第一个带有样式化组件的样式化`div`的例子:

```
import styled from 'styled-components';const AwesomeStyledDiv = styled.div`  
    width: 20px;  
    height: 10px;  
    background-color: blue; 
`
```

在研究了标记的模板文字之后，这里发生的事情应该更清楚了:

1.  `styled.div`只是我们导入的一个函数。
2.  当我们用模板文本调用这个函数时，这个函数以我们刚刚讨论过的相同方式接收参数。在这种情况下，它将是作为第一个参数的**整个样式字符串，包装在一个数组中。**

如果我们定义的 styled-component 根据传递的属性改变了 CSS 属性，我们也可以根据我们刚刚了解到的情况进行推理:

```
import styled from 'styled-components';const AwesomeStyledDiv = styled.div`  
    width: 20px;  
    height: 10px;  
    background-color: ${props => props.isRed ? 'red' : 'blue'}; 
`
```

我们可以假设`styled.div`函数将接收两个参数:

1.  它的第一个参数是一个字符串数组，围绕`${props => props.isRed ? 'red' : 'blue'}`分开。大概是:`['width:20px;height:10px;background-color: ', '']`
2.  它的第二个参数将包含占位符中的表达式，在本例中是函数`props => props.isRed ? 'red' : 'blue'`。

# 有了这些知识，让我们构建一个简化版本的样式化组件！

让我们仔细分析一下这个片段中到底发生了什么:

1.  我们创建了一个名为`styledComponentFactory`的工厂函数(如果你不知道工厂函数是什么，它只是一个用于创建东西的设计模式)。
2.  这个函数可以用一个`Component`调用，在这个例子中，它是一个 HTML `div`。它返回另一个函数。
3.  第二个函数是我们的标签函数(用一个模板文本调用)并返回一个 React 组件(`ReturnedComponent`)，我们将在应用程序中的任何地方使用它。
4.  在第一次渲染之后(比如在挂载时，通过`React.useEffect`)，我们在`Component`上设置样式属性。

***注意*** :这个代码片段只对没有插值的模板文字有效。

# 让我们更进一步

你可能会问，创建一个样式化组件克隆的目的是什么？如果它不允许你根据你传递的属性来改变 CSS 属性，让我们来编辑我们的克隆，让它工作。

这里没有太大的变化，区别都在`useEffect`块。

1.  我们移除了依赖数组`[]`，以便`useEffect`块在每次渲染后运行(在装载和更新时，考虑到改变属性值)。
2.  我们使用 reduce 将样式字符串与调用模板文本中的每个函数(或获取表达式的值)的结果连接起来。请记住，当使用模板文本调用函数时:第一个参数是占位符周围的数组**，所有其他参数是占位符**中的**表达式。**
3.  元素的样式属性设置为该样式字符串。

# 这与样式化组件的实际实现有何不同？

本文讨论的是 styled-components 内部工作的简化版本。一个主要的区别是，我们的组件将`style`属性中的所有样式直接放在 HTML 元素上。不需要太多的细节，还有几件事情正在发生:

1.  如上所述，它不内嵌样式。
2.  还会进行一些 CSS 预处理(允许嵌套样式和基于浏览器的前缀样式)。
3.  创建一个唯一的散列并作为类名。这个散列类接收我们传递的自定义样式。然后在我们的 HTML 文档中的`<head />`的末尾注入一个`<style>`标签。

# 结论

1.  styled-components 使用带标签的模板文字来构建您的样式组件。
2.  没有巴别塔魔术使这一工作，这是所有的 ES6 和风格化的组件内部逻辑！
3.  用模板文字调用函数时:第一个参数是占位符周围拆分的数组**，所有附加参数都是占位符**中的**表达式。**
4.  构建一个简单的样式组件克隆非常简单。

非常感谢阅读，我希望这是有帮助的！

参考资料和进一步阅读:

1.  [https://MX stbr . blog/2016/11/styled-components-magic-explained/](https://mxstbr.blog/2016/11/styled-components-magic-explained/)
2.  [https://medium . com/styled-components/how-styled-components-works-618 a 69970421](https://medium.com/styled-components/how-styled-components-works-618a69970421)