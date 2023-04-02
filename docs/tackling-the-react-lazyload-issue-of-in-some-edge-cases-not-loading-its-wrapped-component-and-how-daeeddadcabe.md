# 处理一些反应迟钝的边缘案例

> 原文：<https://javascript.plainenglish.io/tackling-the-react-lazyload-issue-of-in-some-edge-cases-not-loading-its-wrapped-component-and-how-daeeddadcabe?source=collection_archive---------19----------------------->

## 解决在某些边缘情况下不加载其包装组件的 react-lazyload 问题，以及如何在屏幕之间平滑过渡

之前我写了 3 篇文章，关于如何在[metacules.com](https://metacules.com)网站上完成图像加载、优化和性能，以及当试图解决一些挑战时，什么样的思维过程发挥了作用。

如果你也想看看，你可以在链接下面找到这 3 篇文章:

*   [第 1 部分:预加载、延迟加载、交叉观察器、淡入过渡、窗口、错误处理、占位符等等](/image-loading-in-react-js-preloading-lazy-loading-intersectionobserver-fade-in-transitions-722c24f4d5fb)
*   [第二部分:预加载，交叉观察，淡入过渡，用指针事件阻止图像下载等等…](/react-image-loading-optimization-techniques-b885427bde44)
*   [第 3 部分:react-lazyload 的性能优化& react-window、内存化以及如何处理两个包都存在的问题](/scroll-rendering-performance-react-image-loading-optimization-techniques-17350d8f04a8)

在本文中，我想深入探讨一下我在使用 react-lazyload 时遇到的一个问题，即在某些边缘情况下，当它进入视图时，它不会加载它的组件。

给你一些必要的背景知识。请看下图中 Android 设备上的移动 web 应用程序的 UI。

![](img/94899717362b8a320e364e15c4bb0b6d.png)

‘White’ version of the Mobile UI

在页面底部，您会看到 4 个选项卡，用于在应用程序的主“屏幕”之间导航。
页面之间的导航不是通过像从 **/home** 到 **/videos** 这样的路径来完成的(目前在桌面版本中仍然是这样)。相反，我们有一个主要组件，包含 4 个 div，分别用于主页、视频、播客和书籍屏幕，根据选择的导航选项卡，其他选项卡的 div 将设置为**隐藏**。

我喜欢这种方法，例如，与使用 react-router-dom 相比，react-router-DOM 根据当前活动的路由来装载和卸载组件，因为选项卡之间的转换现在可以更快、更平滑地执行，并且一些内容已经预先呈现和预加载。

但是我遇到了一个问题，当从一个选项卡切换到另一个选项卡时，直到用户第一次滚动屏幕时，这些行才会呈现…
如果您阅读了以前的文章，您可能记得每个屏幕上的行都包装在 LazyLoad 组件中，例如在 Books 屏幕上，这些行看起来像这样:

```
{**Object**.entries(bookRows).map(([title, items]) => (
    <LazyLoad offset={200} key={title}>
        <div key={title}
             className={classes.cardRow}>
            <BookRowMobile
                title={title}
                onBookClicked={onBookClicked}
                items={items}/>
        </div>
    </LazyLoad>
))}
```

lazyload 组件只负责在它位于视口内或在视口的指定偏移量内时触发其子组件的渲染。我遇到的问题是，当切换 tab 和它的 div 状态从隐藏变为可见时，渲染没有被触发，只有当滚动一点点时，LazyLoad 组件才会重新评估渲染是否是它的子组件。

我环顾四周，但找不到如何处理这种特定用例的解决方案。因此，最终我想到了实现一个“创造性”的解决方案，每当新屏幕变得可见时，就在视窗中显示行。我是这样做的，当另一个“屏幕”变得可见时，通过编程向下滚动一个像素，再向上滚动一个像素。以相同的位置结束，但以这种方式触发渲染。

我这样做的方式是通过创建一个自定义挂钩，我将传递每个屏幕组件的主 div 的 **ref** ，然后该自定义挂钩将通过 IntersectionObserver API 评估该 div 是否可见，如果可见，则再次上下滚动 1 个像素。

自定义挂钩看起来像这样:

```
export default function useLazyLoadFirstVisibilityFix(ref) {

    const [isVisible, setIsVisible] = useState(false);

    const observer = new **IntersectionObserver**(
        ([entry]) => {
            if (entry.isIntersecting) {
                setIsVisible(true);
                **window**.scrollTo({top: **window**.pageYOffset + 1});
                **window**.scrollTo({top: **window**.pageYOffset - 1});
            } else {
                setIsVisible(false);
            }
        }
    );

    useEffect(() => {
        observer.observe(ref.current)
        // Remove the observer as soon as the component is unmounted
        return () => {
            observer.disconnect()
        }
    }, []);

    return isVisible
}
```

此外，无论引用的组件是否可见，它都会返回一个布尔值。我们不一定需要这个“黑客”来修复这个行可见性问题，但它被用于其他事情…我们将在后面得到那个…

所以现在“屏幕”组件的代码应该是这样的

```
function BooksMobile() {const classes = useStyles*()*;
const ref = useRef();
const isVisible = useLazyLoadFirstVisibilityFix(ref);[... bunch of other code ...]return (
    <div **ref={ref}** className=*{*`$*{*classes.root*}* $*{*isVisible ? classes.isVisible : classes.isNotVisible*}*`*}*> [... other components ...] {**Object**.entries(bookRows).map(([title, items]) => (
            <LazyLoad offset={200} key={title}>
                <div key={title}
                     className={classes.cardRow}>
                    <BookRowMobile
                        onShareBookClicked={onShareBookClicked}
                        title={title}
                        onBookClicked={onBookClicked}
                        shuffleItems={true}
                        items={items}/>
                </div>
            </LazyLoad>
        ))} </div>
);
}
```

useRef 用于存储对 main

的引用，该引用随后被传递给自定义**useLazyLoadFirstVisibilityFix**钩子，该钩子确保 LazyLoad 组件上的呈现在组件变得可见时被触发。

现在，使用*值的部分是可见的。* 我使用了 Material-UI useStyles 钩子，这个组件的样式看起来像这样:

```
const useStyles = makeStyles((theme) => createStyles({
    root: theme.screenRoot,
    isVisible: {
        opacity: 1,
        transition: "opacity 0.3s",
    },
    isNotVisible: {
        opacity: 0,
    },
 }));
```

现在，当从一个屏幕导航到另一个屏幕时，它会创建一个 0.3 秒的不透明度过渡动画，而不是在屏幕之间导航时有一个硬过渡。就像谷歌新闻应用程序使用的例子一样。

所以这就是这篇文章。如果你想看看我正在开发的手机应用原型的现状，你可以在 https://metacules.com[查看](https://metacules.com)

如果你想知道更多，或者想帮助 Metacules.com 的创作，请联系我，通过任何一个渠道关注我，了解未来的最新消息。

如果你有任何额外的东西要添加、改进，或者如果你想给我们的项目送去一些爱或支持，你可以给我买咖啡或帮助筹集我们创建元规则(一种审查的解毒剂)平台的资金

*   [https://www.buymeacoffee.com/l5LnQfk](https://www.buymeacoffee.com/l5LnQfk)
*   https://fundrazr.com/f1ldl3

*里克·范·韦尔森是 metacules 的创始人，高级(Android)移动开发者，目前是使用 React/NodeJs 的 metacules 平台的开发者。
您可以在社交媒体上关注我们:*

*-推特:*[https://twitter.com/VelzenRik](https://twitter.com/VelzenRik)
-*推特*:[https://twitter.com/metacules](https://twitter.com/metacules)
-*脸书*:[https://www.facebook.com/Metaculescom-100856938688500](https://www.facebook.com/Metaculescom-100856938688500)

![](img/c08ac77f23d3f41940524419906a4ba5.png)

Part of the landing page of metacules.com