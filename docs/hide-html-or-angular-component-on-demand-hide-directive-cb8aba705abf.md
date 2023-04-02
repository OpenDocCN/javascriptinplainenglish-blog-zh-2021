# 按需隐藏 HTML 或角度组件:Hide 指令

> 原文：<https://javascript.plainenglish.io/hide-html-or-angular-component-on-demand-hide-directive-cb8aba705abf?source=collection_archive---------8----------------------->

![](img/48f3369c6141c72aa9adab11e8fc9a49.png)

Photo by [Tatiana Syrikova](https://www.pexels.com/@tatianasyrikova?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/little-kid-covering-face-with-hands-while-chilling-in-hanging-chair-3932935/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

有时候你需要在你的模板中隐藏一些 HTML 元素或者有角度的组件。一个示例场景是您有一个显示大量信息的 UI。您希望为用户提供一个在完整模式和精简模式之间切换的开关。

您可以在切换时想要隐藏的块/元素上使用`*ngIf`。`*ngIf`的问题是，当你赋值`false`时，它会将元素从 DOM 中完全移除。这可能会破坏你的用户界面，尤其是当你使用 flexbox 的时候。同样，切换到`true`时，所有组件/元素将被重新渲染，这虽然很小，但仍然是一个性能问题。如果你的组件有很多事情要做，比如调用 API，重计算等。，频繁地将它们移除并重新呈现到 DOM 并不是一个好主意。

另一个选项，`[hidden]`输入可用于 HTML Div 元素中的 Angular。所以你可以根据切换状态隐藏它们。但是它只对有限的元素集起作用，而对角度分量不起作用。

在这种情况下，下面的指令就派上了用场。它的工作方式类似于`[hidden]`输入，其中通过使用 CSS 属性`visibility`来呈现但隐藏一个元素。所以它不是`*ngIf`的替代品。与`[hidden]`输入不同，它也适用于角度分量。

现在在您的模板中使用它:

```
<app-my-component [appHide]="toggled"></app-my-component>
```

感谢阅读！

*更多内容请看*[*plain English . io*](http://plainenglish.io/)