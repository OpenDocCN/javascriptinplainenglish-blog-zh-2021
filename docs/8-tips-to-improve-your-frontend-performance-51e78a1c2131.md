# 提高前端性能的 8 个技巧

> 原文：<https://javascript.plainenglish.io/8-tips-to-improve-your-frontend-performance-51e78a1c2131?source=collection_archive---------16----------------------->

![](img/0ba99a495da5fc1b7e57557ce5abf374.png)

Photo by [Mimi Thian](https://unsplash.com/@mimithian?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

性能改进是我们在任何前端应用程序中面临的最常见问题之一。几乎在每个项目中，在某个时候(通常在后期)，您都会遇到这个问题。在这篇文章中，我想介绍一些我在许多项目中使用过的技术，并希望这些指南和模式也能帮助你。

这里有一些我已经在[我的另一篇文章](/did-someone-say-composition-c7843d898b2)中提到了，但是除此之外，在你真正进行改进之前，还有其他方面需要研究。

# 在任何变化之前

首先，当我们谈到性能调优时，我们需要建立一些测量机制。你不能依赖直觉，因为它很容易把你引向错误的方向。我们认为可能是性能问题背后的原因*通常*根本没有任何问题。一旦你有了度量，就像我们有覆盖所有逻辑的单元测试一样，通常它可以引导你走向正确的方向——或者至少当你在错误的道路上时你会注意到。

# 定义你的目标

在进行性能调优项目之前，明确自己的目标至关重要。它决定了你是否会达到你的目标。所以这里的问题应该是——好的表现意味着什么？达到什么程度我们才能说有了实质性的改善？你不能只是说越快越好。

例如，如果页面加载时间减少 20%意味着成功，那么接下来的每一步都应该以实现这个目标为目标。

# 设置测量

现在我们知道了*改进意味着什么*，我们可以研究测量的方法并建立基线。这是实现度量定义步骤的一个步骤，您需要在构建管道中设置一个性能测试，并可视化您上面定义的`DoD`。您可能不需要每次提交都运行它们，但是可能需要定期检查(每日构建)来了解您的目标和当前状态之间的差距。

例如，从浏览器发送的在屏幕上呈现某样东西的请求需要 5 秒，我们可以将这 5 秒设置为基线，你的团队所做的所有更改都不应该比它慢。就像任何其他测试一样，当页面呈现时间增加时，它会失败。此外，您也可以使用包大小或其他指标来衡量性能。

有像`yslow`或`lighthouse`这样的工具，你可以用来持续集成服务，让你保持正轨。

# 分析和分类

现在我们定义什么是成功，以及相应的反馈回路。**怎么做**从这个阶段开始最重要。我们通常需要对问题进行分析和分类。

首先，我们需要分析它是什么类型的慢。是单纯的代码问题还是更广泛的架构问题？或者，在某些情况下，你会发现一个设计问题。代码问题很简单，也很容易解决。比如使用一些低性能的依赖项(只需替换它们就能获得更好的结果)，或者使用`debounce` / `throttle`来减少调整输入框大小或改变输入框的事件处理量。

另一方面，所有其他问题都可以归为设计问题，比如如何构建模块，或者组件之间的依赖关系是什么。这些问题通常会涉及大的变化，但投资回报率也很高。从长远来看，这对维护和降低缺陷率都有好处。

因此，在此步骤中，您应该确定哪些问题可以通过简单的更改(替换依赖项、添加缓存或记忆叶组件)简单地解决。实际上，因为我们有一个先前定义的基线，一些目标可以通过这些简单的改变来实现。

如果不令人满意，我们需要向前迈进一步。

# 概述

如果简单的更改不起作用，我们需要更多的时间和精力来重构和重新设计我们的应用程序，以满足性能需求。

我们将通过几个具体的例子来讨论一些我们可以使用的技术。我们需要确定一些问题，从正确的方向进行抽象，然后进行拆分。最终目标是确保每个模块/组件尽可能独立，并且易于与其他模块/组件组合。

![](img/22af19148e54b616a12d30730ec663d2.png)

Photo by [Xavier von Erlach](https://unsplash.com/@xavier_von_erlach?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

# 控制反转—类型 1

就像我在本文中讨论的[,`Avatar`不应该包含`Tooltip`，它们应该组合在一起或者单独使用。](/did-someone-say-composition-c7843d898b2)

改变后，`Avatar`不再依赖`Tooltip`:

```
import Avatar from "@atlaskit/avatar";  
import Tooltip from "@material-ui/core/Tooltip";const MyAvatar = (props) => (  
  <Tooltip title="Juntao Qiu" placement="top" classes={...}>  
    <Avatar  
      name="Juntao Qiu"  
      url="https://avatars.githubusercontent.com/u/122324"  
    />  
  </Tooltip>  
);
```

# 控制的反向——类型 2

在其他一些情况下，一个组件被链接到另一个组件，但是它们可以被其他类似的组件替换。像我上一篇文章中[的`InlineEdit`和`InlineDialog`场景。](/did-someone-say-composition-c7843d898b2)

我们可以使用 [render props](https://reactjs.org/docs/render-props.html) 来反转控件，使得一个组件不依赖于具体的实现，而是依赖于一个接口(或者一个协议)。这样，实现接口的所有组件都可以匹配，然后我们可以削减对具体包的依赖(在`package.json`中定义)。

请注意，这与前面的场景非常相似，不同之处在于拆分后这两个组件之间存在一些薄弱环节。`render`函数中的参数是双方都在使用的协议。

```
const MyEdit = () => {  
  return (  
    <InlineEdit  
      editView={(fieldProps, isInvalid, error) => (  
        <Popover open={isInvalid}>  
          <Typography>{error}</Typography>  
          <Textfield {...fieldProps} />  
        </Popover>  
      )}  
      validate={(value) => {  
        return false;  
      }}  
    />  
  );  
};
```

就像上面的例子一样，`editView`的参数不是任意的，它必须是一个包含`fieldProps`、`isInvalid`和`error`的对象(尽管用户可以选择忽略一些参数)。

# 多个入口点

在有些情况下，您只使用一体化库中的一小部分，我们可以使用多个入口点来拆分库，让消费者挑选他们需要的东西。

一个典型的例子是在早期版本的`lodash`中，当用户想要使用一个函数，比如说`partition`，他们需要导入整个包:

```
import _ from 'lodash';const result = _.partition([1, 2, 3, 4], n => n % 2)
```

通过多个入口点，您可以只导入您现在需要的内容:

```
import partition from 'lodash/partition';const result = partition([1, 2, 3, 4], n => n % 2)
```

很可能，你可能有一个`Button`包，它有所有的变体，你可以按类型分割它们并分别导出它们。像`StandardButton`、`LoadingButton`(内置一个附加图标)，或者任何其他专门的类型。

# 惰性负载

你不必一开始就加载所有内容，有些内容可以异步加载，或者只在使用时加载。例如，在 react 中，我们可以使用`React.lazy`或者像`loadable`这样的第三方库来进行延迟加载。它在主页加载(或者只有上面的折叠屏幕)的情况下工作得很好，例如，在用户配置文件下可能有一个巨大的下拉菜单，当用户真正需要它时，你可以让它延迟加载。

```
const UserProfile = React.lazy(() => import('./UserProfile'));
```

在`loading`期间，您可以有一个占位符组件:

```
function HomePage() {
  return (
    <div>
      <Suspense fallback={<div>Loading...</div>}>
        <UserProfile />
      </Suspense>
    </div>
  );
}
```

# 使用缓存

最后一个技巧是使用缓存，这也是人们在后端一直使用的传统方法。简单地缓存昂贵的计算结果，并在内存中的某个地方减少更改内容，可以为以后的访问节省大量时间。它可以在代码级别、本地浏览器数据库(LocalStorage 或 SessionStorage)中，也可以在更高级别，如 CDN 或 redis 缓存服务中。

例如，在 React 中，我们可以使用如下 API:

*   `useMemo`获取数据
*   `useCallback`为功能
*   `memo`对于通常在叶节点的组件

假设我们有一个`Toggle`组件:

```
const Toggle = ({defaultChecked}) => {
    const [checked, setChecked] = useState(defaultChecked);

    const styles = getToggleStyles('light');

    const onClick = () => {
        setChecked(checked => !checked)
    }

    return <label css={styles}>
        //...
    </label>
}export default Toggle;
```

使用`React`中的缓存 API，代码可能如下所示:

```
const Toggle = ({defaultChecked}) => {
    const [checked, setChecked] = useState(defaultChecked);

    const styles = useMemo(getToggleStyles('light'));

    const onClick = useCallback(() => {
        setChecked(checked => !checked)
    }, [])

    return <label css={styles}>
        //...
    </label>
}export default memo(Toggle);
```

注意当使用像`useMemo`或`useCallback`这样的 API 时，这些函数本身的调用不是免费的，所以你需要确保我们之前设置的性能测试告诉你使用前后的区别。

# 摘要

在本文中，我们讨论了前端开发中性能改进的几种方法和模式。在进行任何代码更改之前，我们需要确保我们有成功的定义，然后我们设置基线和相应的测试，以便在任何给定的时间我们都知道更改实际上是否有效。

接下来，我们分析问题并将其分为两大类。简单的修复有时已经很令人满意了。如果不能，那么我们必须使用一些其他的高级技术，比如反向控制、多入口点来简化每个组件，并且更加倾向于可组合的 API。

在一些其他的库或框架中，你可能需要一些其他的 API，但是我们在这里讨论的想法是非常通用的，可以应用在其他类似的场景中。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)