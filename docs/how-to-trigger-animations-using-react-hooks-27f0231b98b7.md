# 如何用 React 钩子触发动画

> 原文：<https://javascript.plainenglish.io/how-to-trigger-animations-using-react-hooks-27f0231b98b7?source=collection_archive---------5----------------------->

![](img/cce1795085d016dc8aef3d4e07c0bfc1.png)

# 网站动画

在这个时代，网站似乎需要动画。我会说，根据你要去的网站类型，动画可能是合适的。在这篇文章中，让我们来看看如何使用 React 钩子触发动画。我们希望能够控制用户何时看到动画。当用户滚动到网站的某个部分时，我们将使用 CSS 滑动元素。

# 设置

在这篇文章中，我将使用 React 和 Tailwind CSS，但是你可以使用任何你想使用的 CSS。我将为顺风 CSS 使用一个名为@headlessui/react 的组件。所以让我们从安装这个包开始。

```
npm i @headlessui/react
```

# 滑动组件

现在我们已经安装好了，让我们创建一个组件来使用 Tailwind CSS 类，它将动画元素，使其滑入屏幕。

```
import { Transition } from '@headlessui/react';interface Props {
  show?: boolean;
  children: React.ReactNode;
}export default function SlideUp(props: Props) {
  const { show, children } = props;
  return (
    <Transition
      show={show}
      enter="transform transition ease-out duration-500"
      enterFrom="opacity-0 translate-y-full"
      enterTo="opacity-100 translate-y-0"
      leave="transform transition ease-out duration-500"
      leaveFrom="opacity-100 translate-y-0"
      leaveTo="opacity-0 translate-y-full"
    >
      {children}
    </Transition>
  );
}
```

使用这个组件，你可以定义当布尔 show 设置为 true 时 CSS 运行什么。然后当它被设置为 false 时，它将撤销或隐藏该元素。

因此，当它想要显示它将运行这个动画类

从

```
opacity-0 translate-y-full
```

到

```
opacity-100 translate-y-0
```

它将以 0 的不透明度开始，并将元素滑动到视口中，将不透明度动画化为 100。

现在让我们创建一个容器组件来控制显示布尔值。

```
import { useState, useRef } from 'react';
import useTriggerOnScroll from '../../../hooks/useTriggerOnScroll';
import Slide from '../SlideUp';interface Props {
  className?: string;
  children: React.ReactNode;
}export default function ScrollSlideUp(props: Props) {
  const { className = '', children } = props;
  const el = useRef();
  const [show, setShow] = useState<boolean>(false);
  useTriggerOnScroll(el, (triggered) => {
    setShow(triggered);
  });
  return (
    <div className={className} ref={el}>
      <Slide show={show}>{children}</Slide>
    </div>
  );
}
```

这个组件将包围我们的转换组件。你可以设置你自己的 CSS 类，你不需要使用 Tailwind。这个容器组件将设置一个 react 引用来控制元素，并使用我们的自定义钩子来计算元素是否已经被滚动到。如果有，那么它将使用一个触发的布尔值调用回调。然后，使用触发的布尔值，我们可以将过渡组件设置为动画。

# useTriggerOnScroll

现在让我们创建我们的自定义挂钩。

```
import { useEffect, useState } from 'react';function getOffset(el) {
  var _x = 0;
  var _y = 0;
  while (el && !isNaN(el.offsetLeft) && !isNaN(el.offsetTop)) {
    _x += el.offsetLeft - el.scrollLeft;
    _y += el.offsetTop - el.scrollTop;
    el = el.offsetParent;
  }
  return { top: _y, left: _x };
}function hasScrolledTo(el) {
  if (!el) return false;
  const top = getOffset(el).top;
  const offset = window.innerHeight / 2;
  return top - offset <= window.pageYOffset;
}export default function useTriggerOnScroll(ref, onTrigger) {
  const [triggered, setTriggered] = useState<boolean>(false);
  useEffect(() => {
    function onScroll() {
      const viewed = hasScrolledTo(ref.current);
      if (viewed && !triggered) {
        window.removeEventListener('scroll', onScroll);
        setTriggered(true);
        onTrigger(true);
      } else if (!viewed && triggered) {
        window.removeEventListener('scroll', onScroll);
        setTriggered(false);
        onTrigger(false);
      }
    }
    setTimeout(() => {
      window.addEventListener('scroll', onScroll);
    }, 1000);
    return () => {
      window.removeEventListener('scroll', onScroll);
    };
  }, [ref, onTrigger, triggered]);
}
```

这将设置一些帮助函数来计算元素是否已经被滚动到。然后我们设置一个 useEffect 来创建窗口滚动事件监听器。每当网页滚动时，它将调用我们的事件处理程序，并检查元素是否已经滚动到。如果有，我们将状态设置为 true 并调用 onTrigger call back，然后它将调用我们的容器组件并激活元素。当用户向上滚动时，if 会将 show boolean 设置为 false 并重新隐藏该元素。

# 结论

有许多 CSS 动画库和软件包。这是创建一个自定义挂钩，如果你需要任何自定义代码编写动画。如果您对如何运行动画有任何意见或建议，请随时留下您的评论。