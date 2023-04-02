# 我来这里不是为了赞美 Redux，而是为了埋葬它

> 原文：<https://javascript.plainenglish.io/i-come-here-not-to-praise-redux-but-to-bury-it-d29f4bde4653?source=collection_archive---------12----------------------->

## Redux 对于普通用途来说已经太大了。我建议使用一个更小、更易于使用的 TypeScript + React 系统，称为 evalvite

![](img/23390cf5e3c7094a29e881c91b145cc1.png)

> 小丑对小偷说
> 这里太混乱了
> 我无法解脱

Redux 是一个巨大的东西。带着些许悲伤，我也认为这是一件重要的事情。我在这里指的是*巨大的*在两种意义上的常见用法:巨大是因为它有许多行代码，尤其是当你考虑到它的必要表亲，如“redux-react”、“redux-devtools”、“redux-persist”、“redux-thunk”，甚至是表亲的祖父“redux toolkit”我甚至不考虑一个有*还原传奇*的世界。另一种“巨大”的感觉是有很多采用、牵引、用户或思想共享的东西。例如，带有伯尼·桑德斯手套的迷因是(曾经是？)，毫无疑问，*巨大。*

许多 React 应用程序的整个操作都依赖于 Redux。(React 是另一个“巨大”的东西，但那是改天的话题。)使用 Redux 和 React 的争论，或者更直接地说，响亮、粗俗的争论通常归结为这样一个概念，即当 Redux 用于驱动 React 组件时，React 组件可以变得更具有声明性。(声明性必然更好的原因通常没有解释。)那些提出上述论点的人通常会指出这样一个事实，即人们可以*声明*从状态(Redux)到显示(React)的转换，并保证它总是为真。这是一种保证，就像“如果你不吸烟，你不会得肺癌”一样(有点错误)当然，不吸烟当然是一个很大的帮助，但有很多重要的细节隐藏在这句话里。

这篇文章的论点是 Redux 已经变得太大、太复杂，而且一般来说太重*以至于不能在实际的 React 应用程序中使用；复杂性并没有给我们带来足够的回报。是的，是的，我知道 Redux 的核心可以很小，但大多数人现在在 Redux 上涂上足够多的糖霜，足以导致一个相当大的欧洲国家的全部人口患糖尿病。向 B. Stroustrup 道歉。*

# Redux 内部是一个小而简单的数据流系统，它拼命地想要出去。

# 以打字打的文件

本文关注在 TypeScript 中使用 Redux 我不会用普通的 JavaScript 来评论 Redux。我可以提出一大堆理由来解释为什么这段婚姻会触礁，但是我认为一个单独的、经常使用的类型声明`AsyncThunkActionCreator`可以解释我所需要的一切:

```
declare type AsyncThunkActionCreator<Returned, ThunkArg, ThunkApiConfig extends AsyncThunkConfig> = IsAny<ThunkArg, (arg: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig>, unknown extends ThunkArg ? (arg: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig> : [ThunkArg] extends [void] | [undefined] ? () => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig> : [void] extends [ThunkArg] ? (arg?: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig> : [undefined] extends [ThunkArg] ? WithStrictNullChecks<(arg?: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig>, (arg: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig>> : (arg: ThunkArg) => AsyncThunkAction<Returned, ThunkArg, ThunkApiConfig>>;
```

如果当你看代码样本时，你的目光呆滞，那么恭喜你，你是一个半正常的人类。

我不是说`AsyncThunkActionCreator`的打字是*坏了*，我是说*错了。*在这里被破坏意味着上面没有像宣传的那样工作，或者在某些方面需要*修复*才能工作；这不是问题所在。相反，这个代码是错误的，因为它是被**而不是**破坏的事实让我担心人类的未来。这也让我想到，“当你需要宣言来实现它时，什么能让你相信你正在做的是一个好主意？”

# 小 Redux 的大麻烦

简而言之，Redux 最大的四个问题详述如下。如果你不同意这些是问题，或者问题大到足以证明更换工具是正确的，那么你可以回到你定期安排的努力，以确保一个 Playstation 5。

*   将 Redux 与 React 一起使用时，您肯定需要理解的概念:Redux、组合 Redux、actions、action creators、dispatch、mapStateToProps、mapDispatchToProps，以及何时何地可以修改状态、选择器、存储和异步 thunks。根据您的工具和应用，您可能还需要了解切片、中间件、增强器和 immer。
*   Redux 的打字和 typescript 不太协调，如果你能忍受的话，再读一遍上面的内容。它们确实有效，但肯定不简单。首先，当你在编辑器中得到一个错误时，你会注意到“解释”它的工具提示覆盖了你的半个屏幕，内容看起来是调制解调器线路噪声！这是因为使 Redux 与 Typescript 一起工作所需的类型声明极其复杂。其次，通过 connect()使用 HOC 或更高阶的组件意味着您必须理解 redux-react 通过 connect()生成的包装器，以及它如何与您的代码(被包装的对象)相关联。这已经成为一个问题，Redux Toolkit 创建了`ConnectedProps`来试图改善一些问题。(Post scriptum: Reddit 用户 acemarke 纠正我说`ConnectedProps`来自 react-redux 而不是我上面写的 Redux Toolkit。我为这个错误道歉。)
*   Redux 的性能与减速器的数量成比例。Redux 将所有调度的动作传递给所有的减速器，从而保证**app 的所有**部件的性能都受到添加**任何**新减速器的影响。换句话说，一旦你的 Redux 数量足够大，你用 Redux 做什么都没关系，都会很慢，哪怕你在做的操作简单到翻转一点点。
*   Redux 对`<Provider>`的设计是将底层数据值的一部分从存储中推入 props 供组件使用，通常是为了进行可视化显示。`mapStateToProps()`控制组件看到哪些值。这个函数名字的讽刺意味不应该被忽略。很明显，Redux store 代表了你的应用程序的**状态**，然而成熟的**状态**的 React 概念却被忽略了。

> 你可能会问自己，我该怎么做？

# evalvite

为了尝试修复上面列出的问题，我构建了 *evalvite* : bad french，意为“快速评估”。软件的名字没有大写。这里是它与 Redux 的主要对比，所以如果你不在乎这些，你可以回到你定期安排的努力，从百思买的网站上狙击 Playstation 5。

*   evalvite 具有属性(自动维护的数据值)和模型(属性的集合)的概念。就是这样。
*   evalvite 是为 Typescript 设计的，具有强类型，所有的类型声明都有直接意义，例如`Attribute<number>`或`Attribute<string>`。
*   evalvite 软件是增量的，因为 EvalVite 是算法(见 Hudson '93)。这里的增量意味着维护数据模型所做的工作量与对数据模型所做的更改量成比例。小变化比大变化快。
*   evalvite 将 React 组件模型的值放入所述组件的“状态”中。这意味着`render()`可以简单地咨询`this.state`来完成它的工作。
*   异步调用不需要特殊的技巧，比如从网络上获取数据。您可以正常处理承诺，根据需要设置属性值。

*注意:evalvite 目前只支持基于类的 React 组件。没有已知的原因使*不能*工作功能组件(FCs ),但是作者更喜欢基于类的组件。如果你是 FCs，hooks 等方面的专家，请提交一份 PR 来解决文章末尾列出的回购问题！*

# 通过示例进行评估

用 evalvite 的话来说，您需要为每个 React 组件创建一个*模型*。如果您的 React 应用程序中有一个`FooList`和一个`FooListItem`组件，那么您可能会有`FooListModel`和`FooListItemModel`包含各自组件显示的数据。evalvite 保证来自模型的最新值在您所在的州总是可用的，所以`render()`很容易。

让我们做一个愚蠢的，但教学上有趣的例子。有几个例子也可以在 evalvite 发行版中帮助您。

我们将定义一个复选框，它的文本内容从普通变为粗体。是的，很傻，但是看看 evalvite 如何解决 UI 问题，比 redux 简单很多，还是很有用的。

# 定义模型

上面的模型在发行版中的文件`example1/models.ts`中，通常将模型放在它们自己的文件中是很方便的，因为如果不分离模型，经常会导致导入循环。这在这里并不是绝对必要的。

正如您所看到的，模型只包含一个属性，如果复选框很重要，它就是一个布尔值，如果是，它将以粗体显示。

# 类型声明

让我们看看我们需要什么声明，通常在组件的文件中:

# 组件本身

因此，与任何 React 组件一样，您需要定义组件的属性和状态。上面我们遵循了从父模型向下传递模型的 React 和 evalvite 约定。这不是强制性的，而是“反应性的”通常，属性`model`用于包含在 models.ts 中定义的模型的副本。

自然，我们现在需要定义组件。不需要 Redux 使用的任何“额外功能”，如 Provider、mapStateToProps、connect、mapDispatchToProps 等。

关于这个定义，有几点值得注意。在构造函数中，我们使用了`bindModelToComponent`来通知 evalvite，当模型更新时，应该重新绘制这个组件。虽然这个模型只有一个属性，但是当一个模型有几个属性改变为**时，绑定到组件的模型中的任何**属性都会导致重绘。

很容易看出，change 函数与复选框的 onChange 相关联，它唯一的动作是操纵模型。这是使用 evalvite 时的典型安排:您只需根据需要更新模型，让 evalvite 处理其余的工作。请注意，如果有其他属性是从模型的重要字段或其他组件中计算出来的，并且因为这一更改而需要更新，那么这些属性将被自动处理。

# 从属属性

记住这个简单的例子，我们将尝试用属性可以相互依赖的思想来扩展您的思维。这些可以以你想要的任何方式跨越模型，但是我们将定义一个只依赖于它自身部分的模型。(旁白:如果您愿意，您还可以将同一个模型传递给不同的组件。)这个完整的示例在示例 3 的分布中。

这个相对愚蠢的应用程序允许你显示任意数量的可以输入数字的框()。所有这些计算都是基于整个输入字段集进行的。计算属性的构造函数的第一个参数是用于更新属性值的函数。第二个参数是新声明属性的依赖属性数组；这些属性的*值*在必要时被传递给作为第一个参数的函数。第三个参数仅用于调试输出。众所周知，EvalVite 在所执行的函数评估数量方面是最优的，尽管这并不能保证该算法在所执行的工作量方面是最优的；EvalVite 不知道计算不同的函数有多贵。

evalvite 自动更新值的一个可能意想不到的副作用是，在向类似“1234”的文本框中键入数字的过程中，从新数字中导出的值会被更新。因此，在您完成输入之前，您会得到 1、12 和 123 的更新。

这里第一个重要的想法是这个模型的字段内容是一个数组。当这个数组的内容改变时(push、pop 等)**或**当数组中的任何元素改变时，相应的属性被更新，呈现它们的组件被重画。自然，数组的内容本身应该是一个模型，就像 React 中有 FooList 和 FooItemList 组件一样。

这个模型中展示的第二个重要思想是属性可以从其他属性中计算出来。evalvite 维护必要的数据结构，以便了解哪些属性是从其他属性派生的，以及它们需要以什么顺序进行计算。除了内容之外的所有属性都是从内容(输入框中的一组数字)中派生出来的，或者是从内容的其他属性中派生出来的！

如果您检查属性 isDefined，您将看到我们正在计算一个布尔属性，只有当内容不为空时，该属性才为真。这是许多界面中的一个常见任务，当列表内容为空时，显示一个组件的完全不同的呈现。在 NumberList(未显示)的 render()函数中，对于 isDefined 为 false 的情况，我们采用不同的代码路径。

另一个有趣的属性是这个模型的平均场。它取决于 isDefined 防止被零除的问题。它还依赖于 sum 和 number 字段分别为平均值计算提供分子和分母。显然，必须确保在平均值之前更新总数和数字。这就是为什么 EvalVite 维护属性之间的依赖关系图，并在进行更新时对所述图进行拓扑排序。

# 结论

github.com/iansmith/evalvite 是上面探索的系统，与 TypeScript 一起干净地工作，大约 800 行代码，将为 1983 年的道奇 Dart 提供动力，并将在冰淇淋上品尝美味。这个简单的应用程序中有一些简单的例子供你借鉴。

如果你需要提醒 Redux 为什么跌倒并且爬不起来，可以将本文中的例子比作

*   https://redux.js.org/recipes/usage-with-typescript
*   https://redux-toolkit.js.org/tutorials/typescript[(注意前提条件！)](https://redux-toolkit.js.org/tutorials/typescript)

> 你好吗，指挥官先生？