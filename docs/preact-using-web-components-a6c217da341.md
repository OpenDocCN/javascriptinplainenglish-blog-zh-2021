# 预动作—使用 Web 组件

> 原文：<https://javascript.plainenglish.io/preact-using-web-components-a6c217da341?source=collection_archive---------13----------------------->

![](img/f372b05ff318ac54e576a9e4d9f73939.png)

Photo by [Nicolas Picard](https://unsplash.com/@artnok?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Preact 是一个前端 web 框架，类似于 react。

它比 React 小，也不复杂。

在本文中，我们将了解如何开始使用 Preact 进行前端开发。

# Web 组件

我们可以在 Preact 组件中呈现 web 组件。

例如，我们可以写:

```
import { Component, render } from "preact";window.customElements.define(
  "x-foo",
  class extends HTMLElement {
    constructor() {
      super();
      let tmpl = document.createElement("template");
      tmpl.innerHTML = `   
        <b>I am in the shadown dom</b>           
        <slot></slot>
      `;
      let shadowRoot = this.attachShadow({ mode: "open" });
      shadowRoot.appendChild(tmpl.content.cloneNode(true));
    }
  }
);export default class App extends Component {
  render() {
    return <x-foo position={{ x: 10, y: 20 }}>foo bar</x-foo>;
  }
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们调用`customElements.define`来创建我们的 web 组件。

然后我们在`App`组件中引用它，并将我们的内容添加到`slot`中。

我们可以通过编写来使用`x`和`y`属性:

```
import { Component, render } from "preact";window.customElements.define(
  "x-foo",
  class extends HTMLElement {
    constructor() {
      super();
      let tmpl = document.createElement("template");
      tmpl.innerHTML = `   
        <b>I am in the shadown dom</b>           
        <slot></slot>
      `;
      let shadowRoot = this.attachShadow({ mode: "open" });
      shadowRoot.appendChild(tmpl.content.cloneNode(true));
    } set position({ x, y }) {
      this.style.cssText = `left:${x}px; top:${y}px; position: absolute`;
    }
  }
);export default class App extends Component {
  render() {
    return <x-foo position={{ x: 10, y: 20 }}>foo bar</x-foo>;
  }
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们添加了`position`设置器。

然后我们设置`this.style.cssText`属性来设置`x-foo`组件的位置。

因此，`x-foo`组件应用了位置值。

我们也可以在 web 组件类中调用方法。

为此，我们将一个 ref 分配给 web 组件。

然后我们可以调用 web 组件类中的方法:

```
import { render } from "preact";
import { useEffect, useRef } from "preact/hooks";window.customElements.define(
  "x-foo",
  class extends HTMLElement {
    constructor() {
      super();
      let tmpl = document.createElement("template");
      tmpl.innerHTML = `   
        <b>I am in the shadown dom</b>           
        <slot></slot>
      `;
      let shadowRoot = this.attachShadow({ mode: "open" });
      shadowRoot.appendChild(tmpl.content.cloneNode(true));
    } set position({ x, y }) {
      this.style.cssText = `left:${x}px; top:${y}px; position: absolute`;
    } doSomething() {
      console.log("did something");
    }
  }
);export default function App() {
  const myRef = useRef(null); useEffect(() => {
    if (myRef.current) {
      myRef.current.doSomething();
    }
  }, []); return <x-foo ref={myRef} />;
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们将`ref` prop 设置为`myRef` ref 对象，它是从`useRef`钩子创建的。

然后在`useEffect`回调中，我们调用`myRef.current.doSomething()`方法来调用 web 组件中的`doSomething`方法。

# 侦听 Web 组件事件

我们可以监听网络组件。例如，我们可以写:

```
import { render } from "preact";
import { useEffect, useRef } from "preact/hooks";window.customElements.define(
  "x-foo",
  class extends HTMLElement {
    constructor() {
      super();
      let tmpl = document.createElement("template");
      tmpl.innerHTML = `   
        <b>I am in the shadown dom</b>           
        <slot></slot>
      `;
      let shadowRoot = this.attachShadow({ mode: "open" });
      shadowRoot.appendChild(tmpl.content.cloneNode(true));
    } set position({ x, y }) {
      this.style.cssText = `left:${x}px; top:${y}px; position: absolute`;
    } connectedCallback() {
      this.shadowRoot.addEventListener("click", function (e) {
        console.log("listend to click event");
        console.log(e);
      });
    }
  }
);export default function App() {
  return <x-foo onclick={() => console.log("click")}>foo bar</x-foo>;
}
if (typeof window !== "undefined") {
  render(<App />, document.getElementById("root"));
}
```

我们调用`addEventListener`将点击事件监听器添加到我们的 web 组件中。

我们设置`onclick`属性为`click`事件分配一个事件监听器。

因此，当我们单击文本时，我们应该看到来自两个事件侦听器的控制台日志。

# 结论

我们可以在 Preact 应用程序中直接使用 web 组件。

喜欢这篇文章吗？如果有，请在[**plain English . io**](https://plainenglish.io)获取更多类似内容