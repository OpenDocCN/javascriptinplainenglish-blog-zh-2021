# 10 个有用的自定义反应挂钩

> 原文：<https://javascript.plainenglish.io/10-useful-custom-react-hooks-f24f4307524b?source=collection_archive---------1----------------------->

![](img/19d1f5a9ae67fd4b84b1ff7e264d6039.png)

Photo by [Freysteinn G. Jonsson](https://unsplash.com/@freys?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你了解他们，喜欢他们，没错，我说的是反应钩。它们是最有用和可重用的代码片段。我想你可以说我上瘾了。

但并不是所有的钩子都是一样的。基本的经常使用，通常能完成工作。但有时需要额外的工具，这里是我遇到的 10 个有用的自定义 React 挂钩。

# 1.使用窗口大小

我不能夸大响应式 UI 的重要性，我也不会去尝试。如果你正在读这篇文章，你可能已经知道了响应式设计的痛苦。

幸运的是，我们有这个挂钩，让我们的生活更轻松。我从一个叫 react-use 的回购中找到了这个版本。我喜欢这个库，这里包含的大部分钩子都来源于它。

[](https://github.com/streamich/react-use) [## stream ich/react-使用

### 反应钩-👍。通过在 GitHub 上创建帐户，为 streamich/react-use 开发做出贡献。

github.com](https://github.com/streamich/react-use) 

代码如下:

```
import { useEffect } from 'react';import useRafState from './useRafState';import { isBrowser, off, on } from './misc/util';const useWindowSize = (initialWidth = Infinity, initialHeight = Infinity) => {const [state, setState] = useRafState<{ width: number; height: number }>({width: isBrowser ? window.innerWidth : initialWidth,height: isBrowser ? window.innerHeight : initialHeight,});useEffect((): (() => void) | void => {if (isBrowser) {const handler = () => {setState({width: window.innerWidth,height: window.innerHeight,});};on(window, 'resize', handler);return () => {off(window, 'resize', handler);};}}, []);return state;};export default useWindowSize;
```

*其中一些挂钩使用 react use repo 的 misc/utilities 文件夹中包含的工具。但是如果你不想安装完整的库的话，这其中的逻辑相当简单。*

# 2.使用点击方式

你是否曾经需要在事情失去焦点后放弃它？当然，你有！但是追踪点击状态可能会很烦人。这个钩子可以保护你。

```
import { RefObject, useEffect } from 'react'*const* EVENTS = ['mousedown', 'touchstart']export *type* OnClickAwayFunc = (event: Event) *=>* voidexport *const* useClickAway = (refs: Array<RefObject<HTMLElement | null>>, onClickAway?: OnClickAwayFunc): void *=>* {useEffect(() *=>* {*const* handler = (event): void *=>* {if (onClickAway) {*const* isClickAway = *refs*.every((ref) *=>* {*const* { current: el } = refreturn el && !*el*.contains(*event*.target)})isClickAway && onClickAway(event)}}if (onClickAway) {for (*const* eventName of EVENTS) {*document*.addEventListener(eventName, handler)}}return (): void *=>* {if (onClickAway) {for (*const* eventName of EVENTS) {*document*.removeEventListener(eventName, handler)}}}}, [onClickAway, refs])}
```

# 3.使用反跳

用户可能会变得不耐烦，或者只是工作速度超过了 UI 输入需要处理的速度。在这种情况下我们该怎么办？

我们一直等到输入停止，然后只运行对我们函数的最后一次调用，简而言之就是去抖。

```
import { DependencyList, useEffect } from 'react';import useTimeoutFn from './useTimeoutFn';export type UseDebounceReturn = [() => boolean | null, () => void];export default function useDebounce(fn: Function,ms: number = 0,deps: DependencyList = []): UseDebounceReturn {const [isReady, cancel, reset] = useTimeoutFn(fn, ms);useEffect(reset, deps);return [isReady, cancel];}
```

# 4.使用方向

跟踪屏幕方向的逻辑可能会令人迷惑，但是我们仍然需要知道它是什么，这样我们就可以相应地更新我们的 UI。抛开所有的双关语，下面是一些代码:

```
import { useEffect, useState } from 'react';import { off, on } from './misc/util';export interface OrientationState {angle: number;type: string;}const defaultState: OrientationState = {angle: 0,type: 'landscape-primary',};const useOrientation = (initialState: OrientationState = defaultState) => {const [state, setState] = useState(initialState);useEffect(() => {const screen = window.screen;let mounted = true;const onChange = () => {if (mounted) {const { orientation } = screen as any;if (orientation) {const { angle, type } = orientation;setState({ angle, type });} else if (window.orientation !== undefined) {setState({angle: typeof window.orientation === 'number' ? window.orientation : 0,type: '',});} else {setState(initialState);}}};on(window, 'orientationchange', onChange);onChange();return () => {mounted = false;off(window, 'orientationchange', onChange);};}, []);return state;};export default useOrientation;
```

# 5.使用更新

通常我们想让 react 决定何时或者是否重新渲染组件。但有时我们可能想在这种情况下手动触发重新渲染。

```
import { useReducer } from 'react';const updateReducer = (num: number): number => (num + 1) % 1_000_000;export default function useUpdate(): () => void {const [, update] = useReducer(updateReducer, 0);return update;}
```

# 6.使用大小观察者

我已经介绍了窗口大小的检测，但是有时候您需要知道一个元素的具体大小。

当对元素大小的引用发生变化时，这个钩子将允许您发出回调，并允许您访问该大小。

```
import { useEffect } from 'react'export *type* SizeObserverCallbackFunc = (contentSize: { height: number; width: number }) *=>* void | Promise<void>export *function* useSizeObserver(callback: SizeObserverCallbackFunc, element?: HTMLElement | null): void {useEffect(() *=>* {if (!element) {return}*// Always execute the callback function when it has changed**const* rect = *element*.getBoundingClientRect()callback({height: *rect*.height,width: *rect*.width})*/* As of the Safari 13.1 release in March 2020, ResizeObserver is now**supported by all major browser (Chrome, Firefox, Safari and Edge). We**will observe the parent element of the canvas and run the callback**function whenever the parent element is resized. As a fallback in-case**ResizeObserver is not supported, we will fallback to listening for a**resize event on the window. */*if (*window*.ResizeObserver) {*const* observer = new *window*.ResizeObserver((entries) *=>* {*const* entry = entries[0]if (entry) {callback({height: *entry*.*contentRect*.height,width: *entry*.*contentRect*.width})}})*observer*.observe(element)return (): void *=>* {*observer*.disconnect()}} else {*const* resizeHandler = (): void *=>* {*const* clientRect = *element*.getBoundingClientRect()callback({height: *clientRect*.height,width: *clientRect*.width})}*window*.addEventListener('resize', resizeHandler)return (): void *=>* {*window*.removeEventListener('resize', resizeHandler)}}}, [callback, element])}
```

# 7.使用 Cookie

Nom，nom，nom 如果没有下一个钩子，你就不会想要管理 cookies。现在，使用 cookies 进行站点跟踪和认证已经成为一种常见的做法，但是在 react 中这样做可能会很麻烦。不要做饼干怪兽；用这个钩子代替。

```
import { useCallback, useState } from 'react';import Cookies from 'js-cookie';const useCookie = (cookieName: string): [string | null, (newValue: string, options?: Cookies.CookieAttributes) => void, () => void] => {const [value, setValue] = useState<string | null>(() => Cookies.get(cookieName) || null);const updateCookie = useCallback((newValue: string, options?: Cookies.CookieAttributes) => {Cookies.set(cookieName, newValue, options);setValue(newValue);},[cookieName]);const deleteCookie = useCallback(() => {Cookies.remove(cookieName);setValue(null);}, [cookieName]);return [value, updateCookie, deleteCookie];};export default useCookie;
```

# 8.使用页面离开

我不想成为那样的人，但是弹出窗口在网页设计中有一席之地。这是这个钩子的主要用例。我相信如果你有创意的话，还有其他的应用。

```
import { useEffect } from 'react';import { off, on } from './misc/util';const usePageLeave = (onPageLeave, args = []) => {useEffect(() => {if (!onPageLeave) {return;}const handler = (event) => {event = event ? event : (window.event as any);const from = event.relatedTarget || event.toElement;if (!from || (from as any).nodeName === 'HTML') {onPageLeave();}};on(document, 'mouseout', handler);return () => {off(document, 'mouseout', handler);};}, args);};export default usePageLeave;
```

# 9.使用 CSS

如果你遵循 CSS 和响应样式惯例，你很可能不需要这一个，但无论如何它值得一提。

这个钩子将允许你动态地使用 CSS，并且只会重新呈现变化的 CSS，肯定非常时髦。

```
import { create, NanoRenderer } from 'nano-css';import { addon as addonCSSOM, CSSOMAddon } from 'nano-css/addon/cssom';import { addon as addonVCSSOM, VCSSOMAddon } from 'nano-css/addon/vcssom';import { cssToTree } from 'nano-css/addon/vcssom/cssToTree';import { useMemo } from 'react';import useIsomorphicLayoutEffect from './useIsomorphicLayoutEffect';type Nano = NanoRenderer & CSSOMAddon & VCSSOMAddon;const nano = create() as Nano;addonCSSOM(nano);addonVCSSOM(nano);let counter = 0;const useCss = (css: object): string => {const className = useMemo(() => 'react-use-css-' + (counter++).toString(36), []);const sheet = useMemo(() => new nano.VSheet(), []);useIsomorphicLayoutEffect(() => {const tree = {};cssToTree(tree, css, '.' + className, '');sheet.diff(tree);return () => {sheet.diff({});};});return className;};export default useCss;
```

这个使用了 Streamich 的另一个库，你可以在这里查看:

[](https://github.com/streamich/nano-css) [## stream ich/纳米 css

### 微型第五代 CSS-in-JS 库，您可以在生产中实际使用。纳米 css 的座右铭很简单:创造…

github.com](https://github.com/streamich/nano-css) 

# 10.使用承诺

乍一看，这可能看起来很奇怪，但是有很多次我不得不将异步代码放入 use-effect 中。

在这些情况下，管理状态和确定事件的顺序会变得很棘手。

这个钩子很好，因为任何承诺都可以包装在它提供的帮助函数中。您的承诺将准备就绪，并在执行前等待组件安装。

```
import { useCallback } from 'react';import useMountedState from './useMountedState';export type UsePromise = () => <T>(promise: Promise<T>) => Promise<T>;const usePromise: UsePromise = () => {const isMounted = useMountedState();return useCallback((promise: Promise<any>) =>new Promise<any>((resolve, reject) => {const onValue = (value) => {isMounted() && resolve(value);};const onError = (error) => {isMounted() && reject(error);};promise.then(onValue, onError);}),[]);};export default usePromise;
```

# 结论

这就是我遇到的 10 个有用的定制反应挂钩。其中许多足够通用，至少可以使用一次，还有一些比较特殊。不管怎样，这个列表展示了自定义 React 钩子的能力和潜力。感谢您的阅读！

你可以在 Twitter 上关注我更多: [@Not_TheAuthor](https://twitter.com/Not_TheAuthor)

*更多内容尽在*[***plain English . io***](http://plainenglish.io)