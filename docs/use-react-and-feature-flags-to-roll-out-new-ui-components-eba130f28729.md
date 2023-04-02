# 使用 React 和 Feature 标志推出新的 UI 组件

> 原文：<https://javascript.plainenglish.io/use-react-and-feature-flags-to-roll-out-new-ui-components-eba130f28729?source=collection_archive---------0----------------------->

## 随着开关的拨动

![](img/a188467fff9db43f71aa8373d8f5b86b.png)

最近，在 [Parallax](https://www.getparallax.com/) ，我和我的团队对我们的用户界面进行了一次彻底的更新。我们更新了按钮、输入、选择、对话框和许多其他视觉元素。以下是对这一努力的一小部分的解释。

# 问题

2021 年夏天，我和我的团队面临了一些有趣的挑战。下一组工作将包括:

*   用新的样式更新我们的许多共享组件(按钮、输入、选择、对话框等)
*   这些更新中有许多会影响设计，但我们也会抓住机会精简组件 API
*   我们应该计划*而不是*能够一次发布所有内容。这样做将意味着巨大的变化和高风险的发布
*   我们应该能够在不改变代码的情况下在新旧组件变体之间进行切换

让我们深入研究一下。

更新设计并不是什么新鲜事。这经常发生，这是我们计划好的。一次做这么多是全新的，也是一项相当大的任务。

一次做这么多的更改，同时还要继续维护当前的组件，这又增加了一层复杂性。这是必要的，否则我们会错过我们必须做出这些改变的窗口，在这将结束后不久，新的功能工作就要开始了。这种巨大的变化将导致大量的技术债务。它增加了在**T5 之前和 T7 之后的努力。我们同意这一点，但这不是一个折扣。**

![](img/d22043cda8f7fcdda7449e96c8b868d4.png)

Photo by [Marek Piwnicki](https://unsplash.com/@marekpiwnicki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 思维能力

进入这个项目时，我们知道我们需要某种[特征标志](https://martinfowler.com/articles/feature-toggles.html)。我们已经在 UI(和 BE)中的其他地方使用了[Launch darky](https://launchdarkly.com/),所以那个部分已经就位了。

有了特性标志解决方案之后，下一个主要挑战是找到一种方法来保留当前的组件，同时更新每个实现以按需使用新的变化。这使得事情变得有趣。我们是就地更新，还是在旧版本的基础上增加新版本？这两种策略各有利弊，经过深思熟虑后，我们认为这两种策略都不是正确的前进方向。我们会两者都用！

现在，随着大方向的确定，我们需要找出一些方法来按需在旧的或新的组件变体之间切换，**而不必改变任何代码**。我们的 UI 是基于 [React](https://reactjs.org/) (具体来说就是 [Next.js](https://nextjs.org/) )构建的，所以这实际上是一次相当短暂的冒险。

# 解决办法

经过相当多的深思熟虑，我们决定创建一个名为`UiExperiment`的新组件(我们在共享组件前加了前缀`Ui`，以便于识别)。该组件将接受一个*【旧】*组件和一个*【新】*组件(`ReactNode`)作为道具，并且还接受一个道具来确定哪一个应该呈现哪一个将由特征标志驱动。

UiExperiment React component, with Typescript

*注:*`*ExperimentName*`*`*Experiment*`*住在这个部件旁边只是为了便于演示。在现实生活中，这些都生活在一个* `**.constants.ts*` *和* `**.types.ts*` *文件旁边的组件文件中。**

*根据设计，这是一个非常简单的组件。如果`isExperimentActive`作为`false`传递，那么渲染作为`props.a`传递的内容。如果作为`true`传递，则渲染`props.b`。在现实生活中，`isExperimentActive`的值来自于一个特征标志。不过，你可能会看到，这可能会比我们在这里所做的更加强大。也许利用这样的组件进行真正的实验，或者用它进行访问控制，等等。*

*现在在应用程序中使用`UiExperiment`非常简单。在我们将旧组件换成新组件的地方，我们在当前组件周围添加`UiExperiment`，然后在其旁边添加新组件。我们现在可以做所有这些工作，继续推向生产，当我们准备好向我们的用户发布这些更新时，只需"*拨动开关"**。**

**Example usage of UiExperiment component**

**等一下，我们再来看看那些`props`。**

**UiExperiment props and supporting types**

**我们为什么要这样设置`props`？嗯，我们正在做一些未来的工作。我们构建这个组件是为了解决今天的一个问题，但我们很早就意识到它也可以用于其他一些很酷的事情。如果我们想在两个以上的组件上做实验呢？还是基于某种旗帜提供不同的体验？**

**`UiExperiment`原来的 api 没有使用道具`isExperimentActive`，只是一个简单的标志。相反，我们将`ExperimentName`作为一个名为`activeExperiment.`的道具传递，这意味着我们可以进行`n`次实验*和*它将是强类型的！**

**不过，我要说的是，我们在这里使用简单切换的原因是，在实践中，这实际上比我们计划的要多。实现组件必须先做一些逻辑工作来传递正确的枚举，而不是传递标志，这并不理想。它最终变得太笨重，导致代码更难阅读。**

**将来我们可能会带回那个道具，但是对于这个项目来说，它没有任何意义。**

**![](img/729aa37a28ca2c9402a37df5dc24b0d4.png)**

**Photo by [Dmitry Ratushny](https://unsplash.com/@ratushny?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)**

# **学习**

## **现有组件 API**

**一些读者可能想知道为什么我们没有把这个逻辑开关放在每个现有的 UI 组件中？**

**What if we used a flag on existing components?**

**我们当然可以做到这一点，在某些情况下我们做到了。不过，在很大程度上，我们希望有一些可移植的东西，在整个应用程序中易于重复。当我们在一个组件上使用了一个标志时，通常是因为我们只是切换了样式，仅此而已。在这些情况下，将标志放在组件上是有意义的。**

**另一部分原因是因为大部分时间工作不仅仅是更新设计，还包括更新组件 API。在许多情况下，更有意义的做法是构建全新的简单组件，然后利用`UiExperiment`在新旧版本之间切换。**

## **清除**

**这项工作需要计划在发布前完成工作，但也需要在发布后完成工作。使用`UiExperiment`会招致技术债务，我们计划在发布后尽快移除。**

**`UiExperiment`的一个好处是新的组件版本已经就位。一旦我们准备好清理并删除所有旧代码，我们就删除了围绕新实现的东西。这将是纯粹的减法，这使得这一点更容易。我们可以很容易地移除包装`UiExperiment`并删除旧的组件，我们就完成了。Typescript 将通过从组件中移除 prop 并处理任何作为结果弹出的 TS 错误来指导我们使用`isV1`标志。**

## **命名**

**我们仍然对道具名`a`和`b`不满意。我和我的团队非常认真地对待命名，这两个名字仍然感觉像…嗯，这些本来可以更好。**

# **结论**

**这个组件成了我们的救命稻草！它允许我们在将功能推向生产的同时，进行所有的 UI 更新。因为我们提前计划使用功能标志，我们可以通过[黑暗启动](https://launchdarkly.com/)和针对特定用户的目标标志状态更进一步。这意味着在我们向所有用户推出之前，我们可以在生产的幕后测试所有的设计更新！**

**最终，这个组件完成了我们需要的一切，甚至更多，并继续存在于我们的应用中。事实上，我们在数百个地方使用这种技术所产生的技术债务也比我们想象的要少。在我们发布这些更新后，我们能够移除所有与这项工作相关的`UiExperiments`。我们计划了大约整整两周，但结果我们不需要它，它只需要一周！！🎉**

**如果你想自己动手修补和`UiExperiment`，我为我的读者准备了一个简单的[代码沙箱](https://codesandbox.io/s/ui-experiment-example-eoj94)。**

**你以前做过类似的事情吗？有没有更好的办法？我很想听听，请在评论中告诉我吧！**

## **参考**

*   **[https://martinfowler.com/articles/feature-toggles.html](https://martinfowler.com/articles/feature-toggles.html)**
*   **[https://launchdarkly.com/](https://launchdarkly.com/)**
*   **[https://reactjs.org/](https://reactjs.org/)**
*   **[https://nextjs.org/](https://nextjs.org/)**
*   **[https://medium . com/counterarts/tinker-with-purpose-9 FB 4 F5 a 52459](https://medium.com/counterarts/tinker-with-purpose-9fb4f5a52459)**
*   **[https://codesandbox.io/s/ui-experiment-example-eoj94](https://codesandbox.io/s/ui-experiment-example-eoj94)**

***更多内容请看*[***plain English . io***](http://plainenglish.io/)**