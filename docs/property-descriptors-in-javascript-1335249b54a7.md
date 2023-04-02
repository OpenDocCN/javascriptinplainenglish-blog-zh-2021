# JavaScript 中的属性描述符

> 原文：<https://javascript.plainenglish.io/property-descriptors-in-javascript-1335249b54a7?source=collection_archive---------13----------------------->

![](img/aab38d416018a2da618626b41d28fea4.png)

JavaScript 是一种动态编程语言。这对于灵活性来说非常好，但是它会使代码变得非常脆弱，因为检查直到运行时才会发生。

所说的灵活性是一把双刃剑。一方面，它给了开发人员很大的自由，但另一方面，它可能会导致意想不到的行为，并增加试图跟踪实际情况的认知负荷。

在这篇文章中，我们将看看**属性描述符**——ES5 中引入的一个特性，它可以帮助控制(甚至扩展)行为，并在这个疯狂、动态的世界中提供一点秩序，我们 JavaScript 开发者称之为家。

属性描述符分为两类:**数据描述符**和**访问器描述符**。这两种类型的描述符都是一个可以用 6 个可选键配置的对象，在本文中，我们将把它们都包含进来。这是介绍本文主题的绝佳机会…

我为本文编写的代码使用了[神奇宝贝 Api](https://pokeapi.co/) ，这是一个非常棒的免费 Api，提供了像我这样的神奇宝贝书呆子可能需要的所有信息！(免责声明:这不是一个赞助帖子，我只是喜欢神奇宝贝。)

不管怎样，回到正题

根据 [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) :

> *数据描述符*是具有值的属性，该值可以是可写的，也可以是不可写的。*访问器描述符*是由 getter-setter 函数对描述的属性。描述符必须是这两种风格之一；不可能两者兼得。

如果只是阅读这篇文章对你来说没有多大意义，你并不孤单。直到我开始钻研代码，它才真正引起我的共鸣。

让我们给出可选键的基本定义:

**可枚举(boolean):** 属性会在枚举过程中显示出来例如`for(key in <yourObject>){...}`
**可写(boolean):** 属性值是否可以被赋予不同的值
**可配置(boolean):** 属性描述符可以被修改和/或删除
**值(任何有效的 JS 值):**将对象的值设置为 **get(函数):**本的返回值

如果你想了解更多关于可用于配置属性描述符的键的信息，你可以在 MDN 文档[这里](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty#description)了解更多。

# 实际例子

在下面的代码中，我们定义了一个`pokemonApi`对象，该对象使用 [node-fetch](https://www.npmjs.com/package/node-fetch) 模块调用 PokéApi 来检索关于特定神奇宝贝的信息。

正如您可能已经猜到的那样，这个示例设计为使用 NodeJS 运行服务器端。

您可以在这里克隆回购[并简单地运行`yarn install && yarn start`来查看运行中的代码。](https://github.com/Adam-Reeves/PropertyDescriptorsDemo)

是时候打破它了🔨

1.  首先我们定义了`makeGetRequest`函数，它使用基本 URI 和指定的资源发出获取请求，将其转换成 JSON 并打印出来。
2.  我们构造`pokemonApi`对象(使用对象字面语法),这将是任何客户端代码与我们的 API 交互的方式。
3.  到好东西上！使用`Object.defineProperty(...)`，我们说对于`pokemonApi`上的`headers`属性，我们想要将`enumerable`、`writable`和 `configurable`设置为假。如果像这种情况下指定的属性已经存在，`Object.defineProperty()`将修改现有的属性。
4.  我们为`pokemonApi.pokemonName.`
    定义了一个 getter 和 setter 函数。`get()`函数首先检查`_pokemonName`是否为真值，然后调用`PokéApi`来检索关于`_pokemonName`中设置的神奇宝贝的信息。注意:我们必须使用`call()`函数来确保`this`被正确绑定。关于这方面的更多信息，请参见我上一篇关于 JS 绑定的文章。
    `set()`将赋值操作的值作为参数`pokemonName`赋值给`_pokemonName`。

我们将`pokemonName`的 getter 和 setter 重定向到`_pokemonName`以防止一个不明显的问题。

如果我们的二传手看起来像这样:

```
set(pokemonName) {
      pokemonApi.pokemonName = pokemonName;
  }
```

当我们不断更新 setter 的值时，我们最终会递归地调用它，直到用尽调用堆栈上的空间。

5.类似于步骤 3，除了我们使用`Object.defineProperties(...)`通过一个函数调用来设置多个属性。

6.我们将`'charizard'`赋值给`pokemonApi.pokemonName`，这将调用我们定义的`set('charizard')`函数并将`_pokemonName`设置为`'charizard'`。

7.最后，我们调用针对`pokemonApi.pokemonName`定义的`get()`函数，该函数包装了对 PokéApi 的调用，因此我们获得了最初 3 个启动器的最佳性能……charizard🔥

# 结束语

虽然您在日常生活中可能不需要太担心属性描述符，但它们绝对有自己的使用案例。

出于好玩，这里有一个我从示例代码中使用的节点获取库中提取的示例:

```
Object.defineProperties(
 Headers.prototype,
 ['get', 'entries', 'forEach', 'values'].reduce((result, property)               => {
     result[property] = {enumerable: true};
     return result;
    }, {})
);
```

这是在几个属性上设置`enumerable: true`的一种非常简洁的方式。

reduce 函数返回:

```
{
  entries: {enumerable: true}
  forEach: {enumerable: true}
  get: {enumerable: true}
  values: {enumerable: true}
}
```

这作为参数之一传递给`Object.defineProperties(...)`，从而设置属性描述符。

我们做到了！我希望这篇文章能让您对属性描述符的工作原理有更多的了解。

一如既往，如果您有任何问题、意见、建议等，请随时联系我们。

快乐黑客👩‍💻