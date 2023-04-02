# React 图像加载优化和滚动渲染性能技术

> 原文：<https://javascript.plainenglish.io/scroll-rendering-performance-react-image-loading-optimization-techniques-17350d8f04a8?source=collection_archive---------0----------------------->

## 第 3 部分:react-lazyload 和 react-window 的性能优化、内存化以及如何处理这两个包带来的问题…

## 第 1+2 部分概述

在[第 1 部分](/image-loading-in-react-js-preloading-lazy-loading-intersectionobserver-fade-in-transitions-722c24f4d5fb)和[第 2 部分](/react-image-loading-optimization-techniques-b885427bde44)中，我们看了如何关注我们实现图像加载组件的问题。我们创建了一个实现，其中包含的功能可以有条件地预加载图像，并在图像组件进入视口的某个阈值时触发图像的网络请求(使用交叉点观察器 API)。我们还看了当图像不能从 url 加载时显示的占位符，以及当图像加载失败时，我们如何处理< img >组件上的 onError()回调函数不总是被调用的事实。

此外，我们添加了淡入过渡，通过动画显示图像不透明度从 0 到 1，以防止图像进入可见状态的硬过渡，我们禁用了通过右键单击下载图像的可能性，或者更烦人的是，通过在移动设备上长按它。
对于这一切，你当然要看看以前的文章。

## 当您没有正确处理大量行的呈现时，会出现性能问题

当你通过台式机或笔记本电脑进入 [metacules 网站](https://metacules.com)上的播客或视频页面时，你会看到每一行都有数十个条目，不同的类别类型也有数以吨计的行。

Brief LoFi overview of what the podcast page looks like

所有这些行包含成百上千的项目。
您可以想象，在进入页面时同时触发所有这些内容的呈现可能会导致一些问题(确实如此！).

让我们看一下主屏幕的主要组件之一:包含 250 多人列表的卡片，用户可以从中选择查询所有可用的媒体项目。

要在该行上呈现 *persons* 集合，您可以创建一个类似如下的 div:

```
<div className="row__scroller" ref={navRef}>
    {persons &&
    persons.map((person) => (
        <div
            key={person.name}
            onClick={() => onPersonClicked(person.name)}>
            <PersonCard 
                name={person.name}
                photoUrl={person.photoUrl}
            />
        </div>
    ))}
</div>
```

这确实造成了严重的性能问题，它只会随着您添加到页面的每一行项目而成倍增加。

这里的问题是，如果你有一个 250 人的集合(这是我们的例子)，那么当组件被挂载，所有 250 个网络请求(如果它们没有被浏览器缓存)加载它们各自的图像时，所有的人卡都将被立即呈现。您可以希望并尝试相信 ImageLoader 组件实现了 IntersectionObserver API，这样您就可以在组件进入视口附近之前不加载图像。

但是……每次父组件渲染时都会渲染 250 个 PersonCard 组件，而不仅仅是视窗中的 PersonCard 组件。

那么我们如何解决这个问题呢？

![](img/3e3c0a1dc887a2f5ae1da059b4679ac3.png)

Swiping & scrolling on the mobile counterpart of the podcast page

# 使用 react-lazyload:

尽管如此，如果您浏览 react-lazyload 的 GitHub repo 上的问题帖子，会发现 react-lazyload 应该适用于水平滚动列表，但当您扩展上面的简单实现并将映射的项目包装到如下所示的 lazyload 组件中时，它并不适用:

```
<div className="row__scroller" ref={navRef}>
  {persons.map((person) =>
    <LazyLoad offset={100} key={person.name}>
        <div
            key={person.name}
            onClick={() => onPersonClicked(person.name)}>
            <PersonCardHome
                name={person.name}
                photoUrl={person.photoUrl}
            />
        </div>
    </LazyLoad>
   )}
</div>
```

垂直滚动确实有效(我们将在本文中进一步讨论)，但我似乎无法实现水平滚动，因为当父组件第一次呈现时，水平列表中的所有元素都会立即呈现。

显然，我不是唯一一个遇到这个问题的人，仍然有一个开放的请求，要求一个例子来告诉我们(如果和如何)它实际上是可行的。如果你想了解这个问题的最新进展，你可以点击这里关注这个问题:[https://github.com/twobin/react-lazyload/issues?q = is %发布+水平+滚动](https://github.com/twobin/react-lazyload/issues?q=is%3Aissue+horizontal+scroll)

那现在怎么办？LazyLoad 似乎不能为我们做到这一点，所以暂时，我恢复使用**反应窗口。**

React-window 至少可以有一个水平滚动列表，其中只有视窗(+threshold)内的项目被渲染，但不幸的是它有自己的问题。

# 反应窗口的使用

React-virtualized 和 react-window(轻量级的对应物)似乎是解决不渲染在*窗口*视窗之外的项目的优化方案。

react-window 的问题是，当滚动列表时，在视口(+ threshold)范围内的项目似乎比需要的更多。

改善这个问题的一个方法是*记忆*列表项目，这样列表中不需要更新的项目就不会被触发进行不必要的重新渲染。这当然已经是一个很好的改进了，但是在使用 react-window 的列表组件时又出现了另一个讨厌的问题…

我没有深入研究 react-window 实际上是如何工作的，但它看起来像是重新渲染 react-window，实际上是卸载和重新装载它的列表组件。

如果你有一个非常简单的用例(就像 react-window 给出的例子一样)，就像一个简单的文本视图组件，那么你不会注意到任何问题。

在我们的例子中，虽然我们有这些图像加载组件，它们也负责添加一个平滑的不透明过渡动画来显示图像。这个功能现在不再像期望的那样工作了，因为每当带有 ImageLoading 组件的列表项被重新装载时，图像开始闪烁，因为从 0 到 1 的不透明度的过渡动画开始一个新的。如何解决这个问题？
您可以在这里找到一个解决方案，以某种方式跟踪哪些图像已经被加载并在之前经历了淡入动画，这样，每当 ImageLoading 组件重新加载相同的图像时，您就不会再显示淡入。

如果你真的必须这样做，作为最后的手段，你也许可以实现这样的解决方案，但理想情况下，我想远离这样的解决方案，并弄清楚你是否能解决问题的根源(而不是症状)。
这看起来像是需要潜入 react-window 库并在那里重写一些代码，这是我目前不想做的。
现在我指望 react-lazyload 的水平滚动条会在某个时候得到修复，这将节省我很多时间。

目前，我选择了一个基于 react-window 的解决方案，在这个方案中，图像是在没有淡入过渡动画的情况下加载的。不理想，但如果你看看 Metacules.com[的播客或视频页面上的行，你会发现它看起来很好，尽管动画没有淡入。](https://metacules.com)

那么实现会是什么样子呢？显示人员卡片的组件的简化版本如下所示:

```
import React, {memo} from "react";
import {areEqual, **FixedSizeList** as List} from "react-window";

function HomePersonsList({persons, onPersonClicked}) {

    const PersonCard = memo(({index, style}) => {
        const person = persons[index];

        **console**.log("RENDER: PersonCard: " + person.name);

        return (
            <div
                onClick={() => onPersonClicked(person.name)}
              **  style={{...style, paddingLeft: "10px"}}>**
                <PersonCardHome
                    useFadeInAnimation={false}
                    key={person.name}
                    name={person.name}
                    photoUrl={person.photoUrl}
                />
            </div>
        );
    }, areEqual);

    return (
        <div className={**classes**.listContainer}>
            <List
                className={**classes**.list}
                **layout="horizontal"**
                height={itemHeight}
                width={**window**.innerWidth * 0.6}
                itemSize={itemWidth + margin}
                itemCount={persons.length}> **  {PersonCard}** </List>
        </div>
    );
}

export default React.memo(HomePersonsList);
```

注意，我们现在有一个列表组件(来自 react-window ),它包含一个子组件，基本上是列表中每个列表项的模板/占位符。要使用水平滚动，你不仅要将布局属性的值设置为“horizontal”，还要确保你传递了列表组件的样式，并将其设置在它的子组件上，如: **style={{…style，等等。}}**

如果不这样做，列表仍然会垂直显示。

***注意****:list 组件使用 React.memo()仅在它的属性实际发生变化时才重新呈现。在那里添加控制台日志，自己看看组件何时被渲染，以及使用 memo 或不使用 memo 之间的区别。*

我想提到的最后一件事是，您还必须设置列表的宽度(它用于计算应该呈现多少项)。在 metacules.com 上，卡片占据了 60%的屏幕宽度，所以我通过占据窗口的**内宽**来做到这一点。如果你想实现它，就像用户界面在调整大小时不能很好地调整一样，那么你必须做一些稍微不同的事情。但是我会让你来决定怎么做；)

水平滚动到此为止。那是骗局。垂直滚动怎么样？

# 使用 react-lazyload 限制垂直放置项目的呈现

*这里可以得到 react-lazy load*[](https://www.npmjs.com/package/react-lazyload)**。**

*幸运的是，优化垂直平面中呈现的行数只是小菜一碟。如果你看看 metacules.com 的播客屏幕，你会发现当你向下滚动时，在某一点上有很多行按类别显示播客。要确保这些行仅在几乎进入视图时才被呈现，代码很简单:*

```
*{categories.map((category) =>
    <LazyLoad offset={600} key={category.id}>
        <PodcastRowCategory category={category} 
                            onPodcastClicked={onPodcastClicked}/>
    </LazyLoad>
)}*
```

*将此处的 offset 设置为 600，这意味着当该行到达视口外 600px 以内时，它将开始渲染。*

*就是这样！*

*![](img/1c0b7f3d3c1bb6c34172162449dd1a12.png)*

*如果你想知道更多，或者想帮助 Metacules.com 的创作，请联系我，通过任何一个渠道关注我，了解未来的最新消息。*

*如果你有任何额外的东西要添加、改进，或者如果你想给我们的项目送去一些爱或支持，你可以给我买咖啡或帮助筹集我们创建元规则(一种审查的解毒剂)平台的资金*

*   *[https://www.buymeacoffee.com/l5LnQfk](https://www.buymeacoffee.com/l5LnQfk)*
*   *[https://fundrazr.com/f1ldl3](https://fundrazr.com/f1ldl3)*

**里克·范·韦尔森是 metacules 的创始人，高级(Android)移动开发者，目前是使用 React/NodeJs 的 metacules 平台的开发者。
您可以在社交媒体上关注我们:**

**-推特:*[https://twitter.com/VelzenRik](https://twitter.com/VelzenRik)
-*推特*:[https://twitter.com/metacules](https://twitter.com/metacules)
-*脸书*:[https://www.facebook.com/Metaculescom-100856938688500](https://www.facebook.com/Metaculescom-100856938688500)*

*![](img/45940f2a1498e67c4011d91eb410e142.png)*

*Screenshot of part of the Landing Page of [metacules.com](https://metacules.com)*

# *来源:*

*   *第一部分:[https://JavaScript . plain English . io/image-loading-in-react-js-preloading-lazy-loading-intersection observer-fade-in-transitions-722 c24 F4 D5 FB](/image-loading-in-react-js-preloading-lazy-loading-intersectionobserver-fade-in-transitions-722c24f4d5fb)*
*   *第二部分:[https://JavaScript . plain English . io/react-image-loading-optimization-techniques-b 885427 bde 44](/react-image-loading-optimization-techniques-b885427bde44)*
*   *用 react-lazyload 跟踪关于水平滚动的更新:【https://github.com/twobin/react-lazyload/issues? q =是% 3 发行+水平+滚动*
*   *[https://react-window.now.sh/#/examples/list/fixed-size](https://react-window.now.sh/#/examples/list/fixed-size)*
*   *[https://www.npmjs.com/package/react-window](https://www.npmjs.com/package/react-window)*
*   *[https://www.npmjs.com/package/react-lazyload](https://www.npmjs.com/package/react-lazyload)*
*   *[https://metacules.com](https://metacules.com/)~创造审查的解药*
*   *[https://fundrazr.com/f1ldl3](https://fundrazr.com/f1ldl3)*