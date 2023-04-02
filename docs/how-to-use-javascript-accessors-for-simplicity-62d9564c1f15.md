# 如何简单地使用 JavaScript 访问器

> 原文：<https://javascript.plainenglish.io/how-to-use-javascript-accessors-for-simplicity-62d9564c1f15?source=collection_archive---------12----------------------->

![](img/8598fa5c25002fa0c17af4f04d6ad287.png)

访问器允许在访问变量时运行逻辑。在涉及复杂逻辑的情况下，可以使用访问器来简化代码。为了便于说明，让我们考虑在 iOS 设备上的移动网页中布局 UI 所需的逻辑。

通常，网页在 Safari 中运行，它有一个地址栏。在这种情况下，`window.innerWidth`和`window.innerHeight`提供了网页上可用空间的尺寸。但是，可以在主屏幕的页面上安装一个书签。使用此快捷方式启动 Safari 时，网页的行为类似于应用程序。地址栏是隐藏的，整个屏幕是可用的空间。在这种模式下，`window.outerWidth`和`window.outerHeight`提供了网页上可用空间的尺寸。通过使用访问器，我们可以在进行计算时简化逻辑，这样，除了访问器确定是使用`inner`还是`outer`属性之外，可以执行相同的计算。

首先，我们需要检测浏览器的模式。这是通过检查`navigator.standalone`属性来完成的。为了更好地衡量，我们还将通过检查`navigator.userAgent`来检查 Safari 是否被使用。如果网页已经从主屏幕启动，以下测试返回`true`:

`/Safari/.test(navigator.userAgent) && navigator.standalone`

如果不使用访问器，我们将需要使用复杂的逻辑来执行计算。我们可以定义函数来简化表达式，但是，如果有很多代码已经使用了需要修改的`inner`和`outer`，那么很多代码将需要修改。如果逻辑足够复杂，用函数调用替换代码很容易出错。例如，来自 React 应用程序的这段代码检测设备是否被旋转过:

```
handleResize() {
  if (window.innerWidth != this.state.DisplayWidth && 
      window.innerHeight != this.state.DisplayHeight) {
    this.setState({
      DisplayHeight: window.innerHeight,
      DisplayWidth: window.innerWidth
    });
  }
}
```

让我们定义一个函数来修改这个逻辑并使用它:

```
launchedFromHomeScreen() {
  return /Safari/.test(navigator.userAgent) && navigator.standalone
}

handleResize() {
  if (this.launchedFromHomeScreen() {
    if (window.outerWidth != this.state.DisplayWidth && 
        window.outerHeight != this.state.DisplayHeight) {
      this.setState({
        DisplayHeight: window.outerHeight,
        DisplayWidth: window.outerWidth
      });
    }
  } else {
    if (window.innerWidth != this.state.DisplayWidth && 
        window.innerHeight != this.state.DisplayHeight) {
      this.setState({
        DisplayHeight: window.innerHeight,
        DisplayWidth: window.innerWidth
      });
    }
  }
}
```

如您所见，代码量翻了一番。此外，任何逻辑更改都需要进行两次。

在`dim`对象上使用`defineProperty`创建访问器...

```
const dim = {};

Object.defineProperty(dim, "launchedFromHomeScreen", {
  get() {
    return /Safari/.test(navigator.userAgent) && navigator.standalone;
  },
});

Object.defineProperty(dim, "width", {
  get() {
    return dim.launchedFromHomeScreen
      ? window.outerWidth
      : window.innerWidth;
  },
});

Object.defineProperty(dim, "height", {
  get() {
    return dim.launchedFromHomeScreen
      ? window.outerHeight
      : window.innerHeight;
  },
});
```

请注意，将`window.innerHeight`改为`dim.height`是一个保持原始逻辑的简单解决方案。

```
handleResize() {
  if (dim.width != this.state.DisplayWidth && 
      dim.height != this.state.DisplayHeight) {
    this.setState({
      DisplayHeight: dim.height,
      DisplayWidth: dim.width
    });
  }
}
```

*原载于 2021 年 10 月 17 日*[*【https://focusedforsuccess.com】*](https://focusedforsuccess.com/using-javascript-accessors/)*。*

*更多内容请看*[***plain English . io***](http://plainenglish.io/)