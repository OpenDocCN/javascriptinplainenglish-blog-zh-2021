# 如何在 React 中动态加载脚本

> 原文：<https://javascript.plainenglish.io/how-to-load-a-dynamic-script-in-react-2940d30998dd?source=collection_archive---------0----------------------->

![](img/8ce97721c5c4ddd11bc753b28097ea04.png)

向网站添加脚本是常见的要求。让我们假设网站正在使用一些外部工具。要正确使用它，您必须使用外部 JavaScript。很简单的要求，是吧？

你可以通过两种方式添加脚本——静态方式，只需添加脚本标签**index.html**。

但是这种方式存在一些缺陷，例如:

*   它会增加网站的加载时间，从而影响网站的性能。
*   脚本将加载到根本不使用外部脚本的其他页面上。
*   您无法控制脚本何时/如何加载和执行。

另一种加载脚本的方式是**动态加载**。

# 动态加载脚本的好处

一些好处是:

*   您可以在真正需要脚本页面上加载脚本
*   这将减少页面初始加载时间
*   在加载脚本之前，您可以有一个后备用户界面。它将改善用户体验。
*   简单干净的代码

# 使用钩子动态加载它

由于我们的网站在 React 中，我将使用`hooks`来动态加载脚本。

***useexternalscript . js:***

```
import { useEffect, useState } from "react";export const useExternalScript = (url) => {
  let [state, setState] = useState(url ? "loading" : "idle");

  useEffect(() => {
    if (!url) {
      setState("idle");
      return;
     } let script = document.querySelector(`script[src="${url}"]`);

    const handleScript = (e) => {
      setState(e.type === "load" ? "ready" : "error");
    };

    if (!script) {
      script = document.createElement("script");
      script.type = "application/javascript";
      script.src = url;
      script.async = true;
      document.body.appendChild(script);
      script.addEventListener("load", handleScript);
      script.addEventListener("error", handleScript);
    }

   script.addEventListener("load", handleScript);
   script.addEventListener("error", handleScript);

   return () => {
     script.removeEventListener("load", handleScript);
     script.removeEventListener("error", handleScript);
   };
  }, [url]);

  return state;
};
```

上面的代码块包含使用外部脚本所需的代码。首先，它将检查脚本标记是否已经存在。如果是，它将为事件`load`和`error`添加事件监听器

如果 script 标签不存在，它将创建一个 script 标签，设置它的`src`和其他属性，并将其附加到主体。还增加了`load`和`error`事件监听器。

在这里，你可以看到钩子外面是一个字符串`state`。有 4 种可能的输出，分别是`loading`、`idle`、`load`和`error`。

现在我们的`useExternalScript`钩子准备好了。现在，让我们在组件中使用它。

# *useExternalScript* 钩子的用法

让我们假设组件:

***演示:***

```
import React from "react";
import { useExternalScript } from "./hooks/useExternalScript";
import { ComponentWithScript } from "./ComponentWithScript";export const Demo = () => {
  const externalScript = "*<external-script-url>*";
  const state = useExternalScript(externalScript);
  return (
    <div>
     {state === "loading" && <p>Loading...</p>}
     {state === "ready" && <ComponentWithScript />}
    </div>
  );
};
```

在上面的组件中，您可以看到相应的 UI 是基于状态值加载的。

下面是一个工作示例:

就是这样！我希望您喜欢阅读这篇文章，并发现它很有用。请务必在评论中告诉我们你的想法。

*更多内容请看*[***plain English . io***](http://plainenglish.io)