# 超干反应组分

> 原文：<https://javascript.plainenglish.io/super-dry-react-components-d27174003d78?source=collection_archive---------10----------------------->

![](img/99dbe85462df7b3f27fd9bde717b9fe3.png)

Super-dry out here, just like your code should be. Photo by the author.

## 使用可组合包装器将横切关注点应用于功能性 React 组件

你有多少次发现自己编写了这样的组件:

```
const Item => ({ id, title, summary }) => id ? (
  <section>
    {title && <header>
      <h1>
        <a href={`/items/${id}`}>{title}</a>
      </h1>
    </header>}
    <p>{summary}</p>
  </section>
) : null
```

在渲染之前检查`prop`的存在。

如果只有几个组件，这没什么，但是在更大的项目中，这就成了一个负担。

您可以使用`wrapper`功能轻松擦干。

# 封装器

让我们重写`Item`组件，使用一个我们称之为`hasId`的`wrapper`，它拦截对`Item`的调用，并插入一些公共逻辑。

```
const hasId = Component =>
  props => props.id
    ? <Component {...props} />
    : null
```

现在`Item`可以简化为

```
import { hasId } from 'wrappers' // wherever you put themconst Item => ({ id, title, summary }) => (
  <section>
    {title && <header>
      <h2>
        <a href={`/items/${id}`}>{title}</a>
      </h2>
    </header>}
    <p>{summary}</p>
  </section>
)export default hasId(Item)
```

这对于单个组件来说有点过分了，但是如果你想对许多不同的组件应用相同的`id`检查，这就太棒了。

让我们重写一些`Item`来清理`header`。

```
const Header = ({ id, title }) => (
  <header>
    <h2>
      <a href={`/items/${id}`}>{title}</a>
    </h2>
  </header>
)
```

我们知道`id`将一直存在，因为`Header`被设计用于`Item`内部，但作为一个独立的组件，我们不能保证这一点。

同样，我们需要检查`title`是否存在。我们可以让我们的`hasId`包装器更加灵活。

```
const hasProp = name
  => Component
    => props
      => props[name] 
        ? <Component {...props} />
        : null
```

所以现在我们可以在导出之前*包装*我们的`Header`:

```
export default hasProp('title')(Header)
```

并重写了`Item`:

```
import { hasProp } from 'wrappers'const Item => ({ id, title, summary }) => (
  <section>
    <Header id={id} title={title} />
    <p>{summary}</p>
  </section>
)export default hasProp('id')(Item)
```

假设我们希望`Header`超级安全，所以如果没有`id`或`title`就根本不用渲染。使用一个接受一个`names`数组的`hasProps`包装器。

```
const hasProps = (...names)
  => Component
    => props
      => !names.find(n => !props[n])
        ? <Component {...props} />
        : null
```

然后

```
export default hasProps('id', 'title')(Header)
```

如果道具的数量很少，这没问题，并且您应用的包装器只是简单地检查是否定义了一个`prop`。很快您就会想要一种简单的方法来使用任意包装器的整个列表。这就是函数组合派上用场的地方。以下是更多相关信息。

# 这不是高阶元件，而是功能性反应元件吗？

绝对是的。HOCs 作为一种将功能组合到基于类的 React 组件上的干净方式出现，但是当功能组件和钩子流行起来后就不再受欢迎了。但是尽管[钩子在巩固逻辑方面很棒](https://itnext.io/hooked-on-react-10affe4cca3c)，以一种基于类的组件永远无法做到的方式，它们仍然不需要一种方法来组合横切行为。

我描述的包装器比以前的 hoc 简单了几个数量级。而包装器，因为它们返回组件，甚至可以自己使用钩子。

# 带挂钩的包装纸

下面的模式并不少见，其中的文件夹结构如下:

```
components/
  Hero/
    index.js
    Hero.js
```

其中`index.js`是:

```
import { usePreloader } from ‘features/heroes/hooks’
import PureHero from './Hero'const Hero = ({ id }) => (
  <PureHero {...usePreloader(id)} />
)
```

其中`usePreloader`返回一个对象，如

```
{
  isLoading,
  error,
  ...heroData
}
```

要支持这种模式，请编写如下包装器:

`withPreloader`，

```
import { usePreloader } from ‘hooks’const withPreloader = Component
  => ({ id })
    => <Component {...usePreloader(id)} />
```

`withLoading`，

```
const withLoading = Component
  => ({ isLoading, ...props }) => isLoading
    ? <Loading />
    : <Component {...props} />
```

还有`withError`

```
const withError = Component
  => ({ error, ...props }) => error
    ? <Error error={error} />
    : <Component {...props} />
```

现在我们只需要一种简单的方法来用所有这些包装器包装`Hero.js`的内容。

# 构成包装

函数编辑器只是一个函数，它接受一组函数，并使用前面的函数作为输入，依次运行它们。

因此，给定函数`a`和`b`，两者都接受`c`作为参数，并返回`c`的修改版本，那么`compose(a, b)(c)`与运行`a(b(c))`相同。

因为 React 组件只是函数，而包装器只是接受和返回 React 组件的函数，所以您可以编写一个简单的 composer，如下所示:

```
const compose = (...wrappers) =>
  Component => wrappers.*reduceRight*(
    (acc, wrapper) => wrapper(acc),
    Component
  )
```

或者，如果您正在使用 [Redux](https://redux.js.org/api/compose/) ，您可以:

```
import { compose } from 'redux'
```

它做了几乎相同的事情，但有一些可爱的优化。

使用`compose`功能，`Hero`可以简单地导出为:

```
export default compose(
  withPreloader,
  withLoading,
  withError
)(Hero)
```

首先`Hero`将尝试加载数据，然后它将在加载时显示一个`Loading`组件，如果有错误，它将显示一个`Error`。否则，您将获得包含所有数据的`Hero`组件。强大的是，你的核心`Hero`组件很有可能变成一个可记忆的纯组件，它被所需的逻辑所包裹，使其成为一个自我管理的组件。两全其美！

这种组合可重用逻辑块的能力极大地简化了核心组件，使它们更容易推理和测试。

# 结论

当您的组件有许多横切关注点时，您可以通过使用包装器函数来处理这些关注点，从而简化每个单独的组件。简单的包装器函数可以组合成更复杂的包装器，以提供可重用的行为。

我倾向于使用的常见包装器包括

*   `hasProp(name, shape)` —如果缺少命名的`prop`，则返回`null`，
*   `arrayNotEmpty(name, shape, message)` —如果命名数组为空，则返回一个带有`message`的`Empty`组件，如果没有`message`，则返回`null`，
*   `withLoading(isScene)` —返回一个`Loading`组件(或者是一个*场景*关卡或者是*组件*关卡加载器，取决于`isScene`)
*   `withError(message, retry, retryLabel)` —返回一个带有可选`retry`功能的`Error`组件(如果有一个`retry`功能，它会显示一个重试按钮)
*   `withPreloader(hook)` —使用提供的钩子作为`usePreloader`来预载一些数据

其中大多数不到 5 行，易于隔离测试。

# 链接

*   [https://reactjs.org/docs/higher-order-components.html](https://reactjs.org/docs/higher-order-components.html)
*   [https://itnext.io/hooked-on-react-10affe4cca3c](https://itnext.io/hooked-on-react-10affe4cca3c)
*   [https://redux.js.org/api/compose/](https://redux.js.org/api/compose/)
*   [https://it next . io/tame-large-react-projects-by-consistently-applying-these-patterns-and-rules-b7c 70 BAF 5105](https://itnext.io/tame-large-react-projects-by-consistently-applying-these-patterns-and-rules-b7c70baf5105)

—

像这样但不是订户？您可以通过 davesag.medium.com[加入来支持作者。](https://davesag.medium.com/membership)

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。在我们的* [*社区获得独家写作机会和建议*](https://discord.gg/GtDtUAvyhW) *。*