# NativeScript Vue —堆叠和包装布局和操作栏

> 原文：<https://javascript.plainenglish.io/nativescript-vue-stack-and-wrap-layouts-and-action-bars-ad815565c1e?source=collection_archive---------14----------------------->

![](img/245a530e3f991ae19857570777f3aea8.png)

Photo by [Myrtle Schilling](https://unsplash.com/@myrtleschilling?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 是一个易于使用的构建前端应用的框架。

NativeScript 是一个移动应用程序框架，它允许我们使用流行的前端框架构建原生移动应用程序。

在本文中，我们将了解如何使用 NativeScript Vue 构建一个应用程序。

# 带有水平对齐子元素的堆栈布局

我们可以添加水平对齐子组件的堆栈布局。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <StackLayout backgroundColor="#3c495e">
      <Label
        text="left"
        horizontalAlignment="left"
        width="33%"
        height="70"
        backgroundColor="red"
      />
      <Label
        text="center"
        horizontalAlignment="center"
        width="33%"
        height="70"
        backgroundColor="green"
      />
      <Label
        text="right"
        horizontalAlignment="right"
        width="33%"
        height="70"
        backgroundColor="blue"
      />
      <Label
        text="stretch"
        horizontalAlignment="stretch"
        height="70"
        backgroundColor="yellow"
      />
    </StackLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将`horizontalAlignment`支柱设置到我们想要放置`Label`的位置。

设置为`'stretch'`将使`Label`横跨整个屏幕的宽度。

此外，我们可以使子组件垂直对齐。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <StackLayout orientation="horizontal" backgroundColor="#3c495e">
      <Label
        text="top"
        verticalAlignment="top"
        width="70"
        height="33%"
        backgroundColor="red"
      />
      <Label
        text="center"
        verticalAlignment="center"
        width="70"
        height="33%"
        backgroundColor="green"
      />
      <Label
        text="bottom"
        verticalAlignment="bottom"
        width="70"
        height="33%"
        backgroundColor="blue"
      />
      <Label
        text="stretch"
        verticalAlignment="stretch"
        width="70"
        backgroundColor="yellow"
      />
    </StackLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将`orientation`设置为`'horizontal'`来垂直对齐`Label` s

然后在`Label` s 中，我们设置了`verticalAlignment`道具，而不是`horizontalAlignment`。

# 包装布局

`WrapLayout`组件让我们在行或列中定位项目。

我们可以添加一行大小相等的项目，并在默认情况下包装任何溢出的项目。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <WrapLayout backgroundColor="#3c495e">
      <Label text="first" width="30%" height="30%" backgroundColor="red" />
      <Label text="second" width="30%" height="30%" backgroundColor="green" />
      <Label text="third" width="30%" height="30%" backgroundColor="blue" />
      <Label text="fourth" width="30%" height="30%" backgroundColor="yellow" />
    </WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

添加内有`Label` s 的`WrapLayout`。

我们可以将`orientation`属性更改为`'vertical'`来将溢出的项目包装到一个新列中。

为此，我们写道:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <WrapLayout orientation="vertical" backgroundColor="#3c495e">
      <Label text="first" width="30%" height="30%" backgroundColor="red" />
      <Label text="second" width="30%" height="30%" backgroundColor="green" />
      <Label text="third" width="30%" height="30%" backgroundColor="blue" />
      <Label text="fourth" width="30%" height="30%" backgroundColor="yellow" />
    </WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

# 动作栏

我们可以使用`ActionBar`组件在活动窗口的顶部添加一个工具栏。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <WrapLayout></WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

将`ActionBar`组件添加到屏幕顶部。

`title`道具具有显示在顶部栏的文本。

此外，我们可以在`ActionBar`中添加更多项目:

```
<template>
  <Page>
    <ActionBar>
      <StackLayout orientation="horizontal">
        <Image
          src="res://icon"
          width="40"
          height="40"
          verticalAlignment="center"
        />
        <Label text="NativeScript" fontSize="24" verticalAlignment="center" />
      </StackLayout>
    </ActionBar>
    <WrapLayout></WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将`verticalAlignment`设置为`'center'`，使图像垂直居中。

我们添加了`Label`和`text`来做同样的事情。

我们可以通过设置`ActioBar`的道具来添加 app 图标:

```
<template>
  <Page>
    <ActionBar
      title="NativeScript App"
      android.icon="res://icon"
      android.iconVisibility="always"
    >
    </ActionBar>
    <WrapLayout></WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们设置`android.icon`和`android.iconVisible`道具来添加图标并使其可见。

此外，我们可以通过将`flat`道具设置为`'true'`来移除边框:

```
<template>
  <Page>
    <ActionBar title="NativeScript App" flat="true" />
    <WrapLayout></WrapLayout>
  </Page>
</template><script >
export default {};
</script>
```

# 结论

我们可以使用 NativeScript Vue 向我们的移动应用程序添加堆栈和包装布局以及顶栏。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**