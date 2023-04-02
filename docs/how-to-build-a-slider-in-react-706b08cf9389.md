# 如何在 React 中构建滑块

> 原文：<https://javascript.plainenglish.io/how-to-build-a-slider-in-react-706b08cf9389?source=collection_archive---------15----------------------->

*提高你的反应斩&使用反应斩来斩去。*

![](img/8bf491db6afbd191804253aa564f1d88.png)

Photo by [Aleisha Kalina](https://unsplash.com/@desertroseco?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

不，不是上图中的那种滑块，而是一个真正的滑块，你可以从幻灯片 0-3 中导航。那些看起来确实很好吃。

# 我们正在建造的东西(你不能吃这些滑块):

![](img/7f1080cf05ec7e90ccf13e02b2b7759f.png)

# 让我们来看一下这些步骤:

## 第一步)

下载`create-react-app`开始新项目。

## 第二步)

再来看`app.js`:

第 1-5 行是简单的导入，很容易理解。我们导入我们的 CSS 样式表，我们的 3 个滑块组件和 1 个控件组件，按钮将驻留在其中。

转到第 9 行，我们初始化一个名为`currentComponent`的状态变量，我们将使用它来跟踪一个计数变量。我们一会儿就来谈这个。

在第 11 行，我们看到一个名为`slidesArr`的数组，在其中我们转储了 3 个滑块组件。现在有意义了，是吗？

第 13 行给了我们一个名为`countTracker`的常量，它只是一个回调函数，接受一个计数值并将该值设置为 state。

在第 17 行，我们呈现了一个 react-fragment，它为我们保存了一个额外的 DOM 节点，在这个节点中，我们调用我们的`slidesArr`数组，引用我们在第 13 行设置为 state 的计数。

在第 18 行，我们看到一个标记为`Count`的道具被传递到我们的`<Controls />`组件中。这个道具的值就是我们在第 13 行声明的回调函数。我们将在包含两个按钮——上一个和下一个——的控件组件中调用这个回调。

如果您不熟悉将数据从 react 子组件传递回父组件，您可以在本文中深入阅读:

[](/how-to-pass-props-from-child-to-parent-component-in-react-d90752ff4d01) [## 如何在 React 中将道具从子组件传递到父组件

### 学习这个简洁的小技巧，将大块的道具传递回组件树！

javascript.plainenglish.io](/how-to-pass-props-from-child-to-parent-component-in-react-d90752ff4d01) 

## 第三步)

让我们创建 3 个滑块组件(它们都有相同的代码):

## 第四步)

创建将容纳我们的两个按钮——上一个和下一个——的控件组件:

在第 1 行，我们为`useEffect`和`useState`做了标准导入，但是请注意，我们还导入了一个名为`useRef`的钩子。这个钩子将允许我们在 react 中定位 DOM 节点。由于 react 使用虚拟 DOM，使用`document.getElementsByClassName`定位 HTML 元素有时会有点棘手，而且 react 文档鼓励使用`refs`。

在某些情况下，你可以使用`ReactDOM.findDOMNode(component)`，所以你应该好好研究一下。在本文中，我们使用的是`refs`,所以我们现在就坚持使用它。继续前进。

在第 5 行，我们为`count`设置了初始状态变量，从第 6–7 行，我们创建了 2 个 refs——一个用于我们的增量，另一个用于我们的减量按钮。

从第 9 行到第 15 行，每次组件安装和/或计数更新时，我们都会计算一些逻辑。通过将`count`变量传入第 15 行的依赖数组，我们告诉 react 在每次`count`变量的值改变时重新计算 useEffect 内部的逻辑。

***我们的逻辑如下:***

如果我们的计数大于或等于 0 **和**如果我们的计数值小于 3:

*   第 11 行——从 props 调用回调函数并传入`count`,以便我们的`App.js`可以继承计数值。
*   第 12 行—如果`count`大于 0，我们启用递减按钮，因为此时计数为 1 或 2。否则，禁用减量按钮。
*   第 13 行—如果我们的`count`变量的值是 2，(我们在最后一张幻灯片)，禁用增量按钮，否则启用它。

转到第 17 & 18 行，我们看到两个隐式的返回函数，它们或者递减或者递增，并将值设置为 state。

在第 22 & 23 行，我们看到两个`onClick`处理程序连接到每个元素。**上一个**按钮有来自 17 号线的功能`handleDecrement`与之相连&下一个**按钮有来自 18 号线的功能`handleIncrement`与之相连。**

最后，这里是 CSS:

[https://gist . github . com/pjcodesjs/EC 954 f 89 FD 83468586 EC 9 b 17d 0d 3236 e](https://gist.github.com/pjcodesjs/ec954f89fd83468586ec9b17d0d3236e)

## 现在，当我们递增或递减时，我们会看到以下内容:

![](img/7f1080cf05ec7e90ccf13e02b2b7759f.png)

## 紫色啊。

我们甚至可以使用`setInterval`自动增加。

我希望这有助于你更好地理解 react，如果你正在为面试而学习，我建议你也看看这个全面的网络开发面试问题列表，这些问题是你在面试中最有可能被问到的:

[](/web-development-interview-questions-cheatsheet-2021-65eed8bbc1b2) [## 网络开发面试问题备忘单，2021

### 133 个你肯定会被问到的网络开发面试问题。

javascript.plainenglish.io](/web-development-interview-questions-cheatsheet-2021-65eed8bbc1b2) 

此外，如果你需要帮助练习面试，写简历或求职信，请随时联系我在 pjcodesjs@gmail.com。此外，看看这篇文章，我向你展示了我用来获得亚马逊、苹果和许多其他大型科技公司的前端开发人员面试的简历——希望它能帮助你:

[](/how-to-prepare-a-technical-resume-explained-w-examples-for-freshers-experienced-professionals-442d6ab427aa) [## 我通过这份简历获得了亚马逊、苹果和其他公司的技术面试

### 在一页上向大人物展示经验和技能是……可能的。

javascript.plainenglish.io](/how-to-prepare-a-technical-resume-explained-w-examples-for-freshers-experienced-professionals-442d6ab427aa) ![](img/7751922943f2adba4babf29b7c9ec5a5.png)

Meme belongs to PJ Codes.

感谢阅读！

**在**——【Pjcodes.com 来找我。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)