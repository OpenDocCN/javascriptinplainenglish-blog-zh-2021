# 反应本机导航子组件更新

> 原文：<https://javascript.plainenglish.io/react-native-navigational-child-component-updates-767ab3199238?source=collection_archive---------14----------------------->

![](img/3fe9697f9e58f54ffcfb05ac348675d2.png)

Photo by [Markus Winkler](https://unsplash.com/@markuswinkler?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# “犯错是人之常情，真正把事情搞砸需要电脑”

哦，千真万确。虽然 React 在概念上看起来很简单，但它处理的是一个状态模型，需要我们在头脑中拥有多个状态机。把状态放在不同的地方并把它搞砸实在是太容易了——然后你会发现为什么。

在为我的孩子创建一个故事应用程序时，我遇到了一个有趣的问题。

它在整个故事中运行得很好——但是我无法通过父组件重置故事。

![](img/f755e79ac72fd2a5a09987557ea52b1f.png)

Looks great — but the last screen…. is the end of another book.

## 我有 3 个组件

*   故事屏幕—以卡片形式保存故事列表。
*   位置屏幕—这表示处理位置容器的滚动视图。
*   位置—显示该特定位置的选项、文本和其他信息的实际组件。

流程如下所示:

1.  位置屏幕:位置 ID: 0 +故事 ID: 0
2.  位置:LocationID: 0 + StoryID: 0

到目前为止，一切都很好！

这些是作为道具传入的。

但是，单击其中一个按钮，会显示以下内容:位置:位置 ID: 0 +故事 ID: 0

这是因为我们使用 state 来触发 LocationsID 的刷新—我不想构建导航链或历史。

到目前为止，一切顺利。位置组件会不断更新自己，直到我们用尽故事，没有地方可去。

点击不同的故事，显示如下:

1.  位置屏幕:位置 ID: 0 +故事 ID: 1
2.  位置:LocationID: 0 + StoryID: 1

这…看起来是正确的—新故事的位置 0(1，而不是旧的 0)。

但是，我们显示的不是位置 0，而是位置 2，也就是我们结束上一个故事的位置。

现在是时候看看代码了——原因应该很明显:

在这个功能组件的中间有两个 React 挂钩。第一个存储 locationID，第二个存储 storyID。

第 4 行——Location id——被设置为传递到组件位置的默认值。

根据状态挂钩，以下是正确的:

*   当一个组件被安装时，钩子对象(curLocation)被初始化为一个值。
*   如果该值已经初始化，则不会重新初始化。

稍微改变一下我们的图案，我们可以看到:

```
Location: LocationID: 0 + StoryID: 1 + curLocation: 1
```

这是我们上一本书的 curLocation 值。

本质上，这意味着我们需要解决一个用例——用户需要能够改变到一个新的故事。想一想，我认为我们应该只在用户从我们的故事屏幕上点击“阅读”时重新开始一本书，这是一个不同的故事。如果他们在同一个故事上点击阅读，我们应该从他们停止的地方继续他们正在阅读的故事，就像他们使用了“当前故事”导航项目一样。

我意识到这意味着用户需要在开始一个新的故事之前完成故事中的一条路径，但就目前而言，我认为这是最简单的方法。也许以后我会改变主意。:)

因此，这意味着我们需要触发一个父组件(故事屏幕)来告诉较低级别的组件(位置屏幕)更改默认位置。

我的第一次尝试是将这段代码插入位置屏幕:

```
if (curStory !== storyID) {
   setLocation(locationID);
   setStory(storyID);
    console.log(‘Resetting Story ID to ‘ + storyID);
}
```

这一次运行代码时，我们可以看到以下输出:

*   将文章 ID 重置为 1

好——这正是我们想要看到的。

代码工作正常——任何时候我们使用同一本书，我们都使用我们在书中最后知道的位置。每当我们加载不同的书，我们使用一个新的位置 1。

我不喜欢这个解决方案，但它确实有效。我不喜欢它，因为它迫使我们在 Locations 组件中添加代码来跟踪状态。我更喜欢:

1.  从顶层组件设置故事和位置
2.  或者在我有新的故事要处理时卸载位置组件。

让我们继续努力，看看我们能做些什么不同的事情…

首先，让我们添加一点代码来告诉我们组件是否被挂载。这将使用 React Native 的“useEffect”挂钩。

这会打印出以下消息:

```
Location:IN MOUNT: LocationID: 0 + StoryID: 1 + curLocation: 0
```

现在我们有了，让我们用另一种方法来研究。

React 中的组件使用一个键来确定更改、添加或删除了什么项目。它们看起来像道具，但不会传递给组件——而是作为一种提示方式，提示对以后的组件更改做出反应。

使用数组索引并不被认为是好的做法——但是我们这里有 storyID。将来，我可能会考虑使用“nanoID()”直接与故事进行深度链接。不过，我们将在另一篇文章中讨论这个问题。

首先，让我们修改我们的 use effect——只在组件的初始安装或卸载时打印。这模仿了 componentDidMount 和 componentWillUnmount 的 React 类方法。

## 这里发生了两件事

1.  我们在这段代码中添加了一个新的返回——该函数将在组件清理之前运行。
2.  我们将空数组[]添加到依赖项列表中。这意味着这种效果不依赖于任何变量的改变，因此我们应该只在挂载和卸载时运行，而不是在每次渲染后运行

现在运行它，结果如下:

```
LocationScreen: LocationID: 0 + StoryID: 0
Location: LocationID: 0 + StoryID: 0 + curLocation: 0
Location:IN MOUNT: LocationID: 0 + StoryID: 0 + curLocation: 0
Location: LocationID: 0 + StoryID: 0 + curLocation: 2
LocationScreen: LocationID: 0 + StoryID: 1
Location: LocationID: 0 + StoryID: 1 + curLocation: 2
```

注意 StoryID 是如何改变的，但是 curLocation 没有被重置？此外，以前的位置组件没有被拆除。那就是 b\c React 不知道这个位置和其他任何位置都不一样。

让我们继续将关键字添加到位置:

```
<Location
    jsondata={route.params.story.locations}
    locationID={route.params.locationID}
    storyID={route.params.storyID}
    key={route.params.storyID}
/>
```

这样，我们可以看到 curLocation，我们的状态值，在组件被安装时被保存，在我们改变故事后被重置。

```
Location: LocationID: 0 + StoryID: 0 + curLocation: 1
LocationScreen: LocationID: 0 + StoryID: 1
Location: CleaningUP
Location:IN MOUNT:        LocationID: 0 + StoryID: 1 + curLocation: 0
```

这是一个简单得多的解决方案。

我们也可以选择用另一个使用效果来做这件事:

当“storyID”更新时，该事件被触发，并被传递到函数中。

当 storyID 更改时，这个新效果会触发，并重置位置状态。

## 实现该功能的另外两种方法

1.  使用“useRef”钩子——这将允许我进入位置组件，并调用 resetLocation，或者任何我想要的特定函数。这本来可以很好地工作，除了感觉完全没有必要——为什么我的父组件需要调用子组件的函数？
2.  将位置和故事放在上下文提供者中。现在对我来说，这感觉有点过了，但是这并不是不可能的——以后当我想支持状态保存和恢复、深度链接等时，我可能会需要它。

在这里可以看到更多的方法:[https://it next . io/changing-children-state-from-other-component-with-react-hooks-5c 982 c 042 e 8](https://itnext.io/changing-children-state-from-another-component-with-react-hooks-5c982c042e8)

目前，我选择了“key”方法——这是最简单、最直接的方法。它让 React 负责设置和管理组件初始化，并确保我的用例正确工作。

**参考文献:**

*   React Hook eslint 插件——你会想要的！【https://www.npmjs.com/package/eslint-plugin-react-hooks 
*   [https://reactjs.org/docs/hooks-effect.html](https://reactjs.org/docs/hooks-effect.html)
*   [https://react js . org/docs/hooks-FAQ . html # how-do-life cycle-methods-comment-to-hooks](https://reactjs.org/docs/hooks-faq.html#how-do-lifecycle-methods-correspond-to-hooks)
*   [https://medium . com/@ albertogasparin/forcing-state-reset-on-a-react-component-by-using-the-key-prop-14b 36 CD 7448 e](https://medium.com/@albertogasparin/forcing-state-reset-on-a-react-component-by-using-the-key-prop-14b36cd7448e)
*   [https://stack overflow . com/questions/39556753/how-to-reset-child-elements-state](https://stackoverflow.com/questions/39556753/how-to-reset-child-elements-state)
*   [https://reactjs.org/docs/hooks-state.html](https://reactjs.org/docs/hooks-state.html)
*   [https://robinpokorny . medium . com/index-as-a-key-is-an-anti-pattern-e 0349 aece 318](https://robinpokorny.medium.com/index-as-a-key-is-an-anti-pattern-e0349aece318)
*   [https://kentcdodds.com/blog/understanding-reacts-key-prop](https://kentcdodds.com/blog/understanding-reacts-key-prop)
*   [https://react js . org/docs/re conciliation . html # recursing-on-children](https://reactjs.org/docs/reconciliation.html#recursing-on-children)
*   [https://reactjs.org/docs/forwarding-refs.html](https://reactjs.org/docs/forwarding-refs.html)
*   https://reactjs.org/docs/hooks-reference.html
*   【https://reactjs.org/docs/lists-and-keys.html 