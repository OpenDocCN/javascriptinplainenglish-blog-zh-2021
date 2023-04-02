# 如何在 React 中进行简单的自定义拖动以移动组件

> 原文：<https://javascript.plainenglish.io/how-to-make-a-simple-custom-drag-to-move-component-in-react-f67d5c99f925?source=collection_archive---------0----------------------->

React 组件，允许用户拖动和移动常规 DOM 元素和 SVG 元素。

![](img/7b23a4038da2baf3137bd9ca5ed240b5.png)

Your move.

我喜欢制作有趣的交互式 web 东西，最近我写了一篇关于在 React 中创建一个挂钩的文章。正如我在那篇文章中提到的，有大量的拖放库，无论是专门用于 React 还是其他。例如，`[react-beautiful-dnd](https://github.com/atlassian/react-beautiful-dnd)`是一个漂亮的拖放实现，用于在列表间移动，很像 [Trello](https://trello.com/) 。也就是说，有时你并不需要所有的火力，你只需要一些小的东西，或者你只是喜欢修补和编写自己的代码！

同样，我的另一篇[文章](https://medium.com/javascript-in-plain-english/how-to-make-a-simple-custom-usedrag-react-hook-6b606d45d353)讨论了使用 React 钩子拖动组件，这有它的优点和缺点；这一个将集中在包装元素和使用 React 内置事件处理程序的容器组件上。我们还将介绍如何升级我们的组件以允许它拖动一个`svg`元素。

# 反应事件处理程序

您可能已经知道，React 元素的事件处理方式与 DOM 元素略有不同。对于 React 元素，我们使用`camelCase`而不是`lowercase`作为事件名称，并传递一个函数作为事件处理程序而不是一个字符串，如这里概述的。有大量不同的处理程序类型可以用来满足我们最疯狂的拖动幻想，其中一些包括**拖动**处理程序、**鼠标**处理程序和**指针**处理程序。除其他外。

## 拖动处理程序

如果我们的目的是将一个元素拖动到一个特定的拖放区，那么我们绝对希望使用这组处理程序。通常，在这种情况下，我们实际上并不*移动*元素本身，而是我们拖动*数据*，然后当我们放下它时执行一个动作。例如，我们可以从一个列表中拖动一个`li`项到另一个列表上，然后当我们放下`li`时，它会从原来的列表中移除并呈现在新列表中。

*   `onDrag` —拖动元素时调用
*   `onDragStart` —拖动开始时调用
*   `onDragEnd` —拖动结束时调用
*   `onDragEnter` —当被拖动的元素进入有效的放置目标时调用
*   `onDragLeave` —当被拖动的元素离开有效的放置目标时调用
*   `onDragOver` —当元素被拖动到有效的放置目标上时调用

> 使用这些拖动处理程序还需要元素具有`draggable`属性。

## 鼠标处理程序

这些都是不言而喻的，并且通常与鼠标交互。我们可以使用这些来实现拖动行为，跟踪移动的像素并为元素分配新的坐标，从而实际上是*移动*或*平移*元素到一个新的位置。

*   `onMouseDown` —按下鼠标时调用
*   `onMouseUp` —释放鼠标时调用
*   `onMouseMove` —鼠标移动时调用

## 指针处理程序

指针处理程序的功能基本上与鼠标处理程序相同，除了它们是“硬件不可知的”，这意味着它们不*只*与鼠标交互，还包括其他“指针设备”，如触摸(手指、脚趾等)。)表面和笔/触笔表面。也就是说，使用指针处理程序可以简化和改善用户体验，因此通常是我们用例的首选。

*   `onPointerDown` —按下*指针*时调用
*   `onPointerUp` —按下*指针*时调用
*   `onPointerMove` —按下*指针*时调用

# DragMove 组件

这个 React 组件的目标是允许通过一个`css`属性将一个元素移动到 DOM 空间中的一个新位置。因为我们实际上是在移动或*转换*元素，所以我们*而不是*将使用`drag`处理程序集，因为它们更关心的是移动数据，而不是元素本身。相反，我们将使用`pointer`处理程序。为了避免混淆，并与实现`drag`处理程序的组件区分开来，我们将组件命名为`DragMove`。

DragMove component

包装很简单，但是让我们来看一下。

## 小道具

它需要两个可选的回调:`onPointerDown`和`onPointerMove`。如果您想扩展组件的功能，可以提供这些。

它还需要一个必需的`onDragMove`函数，该函数为`onPointerMove`传回事件。

我们通过`children`访问被包装的子节点，它是我们想要拖动和移动的任何有效的 React 节点。

最后，我们还接受可选的`style`和`className`道具，以防我们想要或需要扩展`div`包装器的样式。

## 状态

我们声明一个`isDragging`状态变量来跟踪包装器当前是否在拖动。

## 方法

在组件中，我们声明了三个处理程序方法:`handlePointerDown`、`handlePointerUp`和`handlePointerMove`，它们分别被分配给包装传递的`children`的`div`容器上的属性`onPointerDown`、`onPointerUp`和`onPointerMove`。

每当按下`div`上的`pointer`时，`handlePointerDown`被调用，我们将`isDragging`设置为`true`(如果传递了一个函数，则调用我们可选的`onPointerDown`函数)。

每当在`window`上释放`pointer`时，就会调用`handlePointerUp`，我们将`isDragging`设置为`false`(如果传递了一个函数，则调用可选的`onPointerUp`函数)。

最后还有`onPointerMove`，每当指针移动的时候就叫*。由于我们只想在`isDragging`为`true`时移动包装器，所以我们先检查`isDragging`，如果是`true`，我们调用所需的`onDragMove`函数。如果可选的`onPointerMove`函数被传递，我们在这里也调用它。*

## 效果

我们定义了一个`useEffect`钩子，只在组件挂载后触发一次(因为我们传递了一个空的依赖关系数组`[]`)。安装后，我们将`pointerup`监听器添加到`window`对象，该对象调用`handlePointerUp`。我们在`window`而不是`div`上注册这个监听器，因为否则的话`isDragging`状态只会在指针上升*同时*超过`div`时切换。我们想在指针上升时切换`isDragging`状态，不管它在哪里。我们还返回一个移除事件侦听器的函数，该函数在组件卸载时运行。

# 例子

这里有一个`DragMove`包装器的示例实现。注意，我们声明了一个`translate`状态变量来保存被包装的`children`的当前位置。每当我们在图像上按下并拖动指针时，`handleDragMove`被调用，我们从事件中提取`movementX`和`movementY`，并将它们添加到当前的`translateX`和`translateY`。甜度！

## 其他考虑

在我们的例子中，我们用元素的`transform`属性移动了它。我们也可以设置我们的元素有`relative`或`absolute`定位，并用`left`和/或`top` CSS 属性调整它的位置。这是我们选择*而不是*在`DragMove`组件内部保存当前位置信息的一个原因——它让您决定如何处理拖动信息以及如何根据具体情况实现它。

当然，您可以将`translate`状态移动到`DragMove`组件中，这样可以简化它的使用，但是可能会降低它的可扩展性。

# SVG 元素

可缩放矢量图形(SVG)是一种“基于 XML 的标记语言，用于描述基于二维的矢量图形[。也就是说，SVG 可以用来制作漂亮的——借助于像`DragMove`这样的东西——交互式图形。](https://en.wikipedia.org/wiki/Vector_graphics)

虽然 SVG 很棒，但是我们不能像现在一样使用我们的`DragMove`包装器，因为 SVG 使用他们自己的一组特殊标签，不包括像`div`这样的标签，这是我们用来包装`children`的。让我们对考虑到`svg`的`DragMove`组件做一个小小的修改。

DragMove component—upgraded for SVG

我们添加了一个`isSvg`属性，它决定了它是否在`svg`中被渲染。当`true`时，我们动态地将包装元素从`div`更改为`g`，这是一个“组”SVG 容器元素，它将其属性传递给其子元素。

> 注意:动态设置元素标签类型时，变量名**必须**以大写字母开头。

就是这样！这是另一个使用包装器包装`svg`组件的例子。尝试移动地图上的**紫色航点**。

# 摘要

噪音🎉，我们制作了自己的包装器，允许我们移动常规 DOM 元素和 SVG 元素！以下是一些要点:

## **拖动事件**

通常用于拖放*数据*，而不是实际改变元素的 CSS 定位。

## 指针事件

可用于操纵给定 DOM 或 SVG 元素的 CSS 定位。通常也是`mouse`事件的更好替代，因为它包含更广泛的设备类型(触摸等)。).

*   `onPointerUp`
*   `onPointerDown`
*   `onPointerMove`

## SVG 元素

SVG 元素不像`div`那样使用原生 DOM 元素，相反，您会希望使用`g`元素来“分组”SVG 元素。

差不多就是这样！感谢阅读🙏，希望你学到了一些东西(我当然有)！

# 资源和参考

*   [示例代码沙箱](https://codesandbox.io/s/dragmove-wrapper-cg4hu)
*   [示例 SVG 代码沙箱](https://codesandbox.io/s/dragmove-wrapper-svg-gdogo)
*   [https://github.com/tmarshall07/medium-dragmove-component](https://github.com/tmarshall07/medium-dragmove-component)
*   [https://reactjs.org/docs/handling-events.html](https://reactjs.org/docs/handling-events.html)