# 通过 React 中的拖放将对象添加到 Konva Stage

> 原文：<https://javascript.plainenglish.io/adding-objects-to-your-konva-stage-via-drag-n-drop-in-react-d0000b5b0acd?source=collection_archive---------8----------------------->

![](img/5ce74f06a80f2dc45ddc488190127bcb.png)

Photo by [Ali Abdul Rahman](https://unsplash.com/@_actually_?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我目前正在为 [Reciprocal.dev](https://examples.reciprocal.dev) 构建一个编辑器，以便用户可以构建他们自己的交互式用户旅程地图，作为构建该功能的一部分，我需要一种允许用户轻松创建用户旅程步骤的方法。

在进行了几次 UX 实验后，我决定采用拖放的方式，通过点击项目在地图中心增加一个新的步骤。

在构建地图工具时，拖放方法允许用户在地图上添加项目的初始位置更加准确，这意味着他们只需更少的点击即可实现构建用户旅程地图的目标。

回退允许不使用定点设备的用户(例如有辅助功能需求的用户)仍然向他们的地图添加步骤，但是由于没有办法用这种方法定义位置，我们必须假设它最初应该去哪里。

# 实现拖放

Konva 的文档中有许多使用拖放来填充画布的例子，所以这种方法是有据可查的。本质上，该过程需要两个要素:要拖动的元素和要接收放下事件的元素。

这两个元素都不在 Konva 画布中，但是接收 drop 事件的元素需要是 Konva 画布的父元素，以便定位坐标匹配。

## 实现拖动部分

拖动元素的工作是在应用程序状态中设置信息，放置事件侦听器将使用这些信息来创建将在画布上呈现的对象。

为了设置应用程序状态，我们首先需要创建一个上下文，拖动元素和放置接收元素都可以通过`useContext`钩子访问。

设置好上下文后，我们可以将拖动事件侦听器添加到拖动元素中来设置状态。为此，我们将`draggable`、`onDragStart`和`onDragEnd`道具添加到我们想要拖动的元素中。

> 请注意，为了让代码例子更简短，我已经用`useState`实现了它们

在`onDragStart`和`onDragEnd`的回调中，我们设置放置接收元素将使用的状态值，`onDragStart`用于设置这些值，`onDragEnd`用于在用户决定取消放置时清除它们。

Callbacks for onDragStart and onDragEnd that set the data used by the drop receiver

## 实现拖放部分

拖放接收元素的工作是监听拖动进入其边界的事件以及用户将拖动元素拖放到其上的事件。

当这个 drop 事件被触发时，回调将访问共享状态，获取拖动开始时设置的值，并创建在画布上呈现对象所需的适当数据。

为此，我们需要设置两个事件侦听器；`onDragOver`监听拖动何时进入元素的边界，而`onDrop`监听用户在元素上释放拖动。

In this example the onDragOver is used to update the position of the item being dragged, this can then be used to provide a preview of the dragged item

如果你是在一个基本的拖放 UX 之后，那么你可以为`onDragOver`构建一个非常基本的回调函数，它只是在事件上调用`preventDefault()`，但是如果像我的实现一样，你在地图上为用户提供最终项目的预览，那么你可以用它来更新预览的位置。

对`onDrop`事件的回调是您创建将在舞台顶部呈现的对象的地方，但是您需要根据指针在舞台上的位置来计算放下事件发生的位置，以确保使用正确的位置。

# 向用户提供被放下的项目的预览

上面描述的拖放的基本实现没有最好的用户体验。当用户拖动元素时，他们看到的是他们正在拖动的元素，而不是舞台上的最终对象，当被拖动的元素与最终对象具有相同的比例和外观时，这是好的，但如果不是这样，可能会不和谐。

为了改善拖放体验，我们首先需要做三件事；拖动时隐藏拖动元素，捕获指针在舞台上的当前位置，并在该位置呈现最终对象的预览。

## 拖动时隐藏拖动元素

我们可以在这里重用`onDragStart`和`onDragEnd`钩子来控制用户拖动元素时的可见性。我通过在各自的回调中添加和删除元素的类，然后添加一个 CSS 规则，告诉浏览器在画布上呈现元素。

The .hide class is added to the dragged element by the onDragStart callback

## 在舞台上展示预览

如前所述,`onDragOver`回调可用于在指针位于拖放接收元素的边界内时捕捉指针的位置，并更新状态值，该值可用于预览的位置。

对于预览本身，我在 Konva `Stage`中添加了一个新层，该层监听状态中预览位置值的变化，并在该层上渲染一个对象(如果它们已设置)。

如果用户取消拖放操作，或者拖放到拖放接收元素之外，为了正确地进行清理，我们需要能够将这个位置值设置为`null`，这样当用户没有拖动任何东西时，我们不会在预览层中结束对象。

A condensed version of the code to render a drag preview on the stage

# 支持非指针用户

不是每个用户都会使用指针，所以我们需要一种方法来允许他们在不拖动的情况下向舞台添加项目。这是一个很容易解决的问题，因为我们可以简单地将一个`onClick`事件监听器添加到拖拽元素中，这样就可以将对象添加到舞台中央的应用程序状态中。

If you’re project has zooming you may need to get the scale for the stage and use that when calculating the centre point

# 演示

您可以在下面查看拖放实现的演示以及源代码。

A simple demo showing the drag ’n’ drop functionality in a single file

# 摘要

通过给用户一种将元素拖动到舞台上的方法，我们允许他们在他们想要的位置准确地添加项目。对于我正在构建的像 Reciprocal.dev 这样的应用程序，它依赖于用户构建一个商品地图，这使得 UX 好得多。

*更多内容尽在*[plain English . io](http://plainenglish.io/)