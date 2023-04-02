# NativeScript Vue —网格和堆栈布局

> 原文：<https://javascript.plainenglish.io/nativescript-vue-grid-and-stack-layouts-58482c8aad4?source=collection_archive---------16----------------------->

![](img/a83cabe7dba2f2d3f6ff99262289be82.png)

Photo by [Maria Teneva](https://unsplash.com/@miteneva?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 是一个易于使用的构建前端应用的框架。

NativeScript 是一个移动应用程序框架，它允许我们使用流行的前端框架构建原生移动应用程序。

在本文中，我们将了解如何使用 NativeScript Vue 构建一个应用程序。

# 网格和星形尺寸

我们可以创建一个星形大小的网格，为子元素按比例设置网格大小。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <GridLayout columns="*, 2*" rows="2*, 3*" backgroundColor="#3c495e">
      <Label text="0,0" row="0" col="0" backgroundColor="red" />
      <Label text="0,1" row="0" col="1" backgroundColor="green" />
      <Label text="1,0" row="1" col="0" backgroundColor="blue" />
      <Label text="1,1" row="1" col="1" backgroundColor="yellow" />
    </GridLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将列分别设置为屏幕宽度的 1/3 和 2/3。

我们将行分别设置为屏幕高度的 3/5 和 3/5。

我们可以将网格布局设置为固定或自动调整大小。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <GridLayout columns="80, auto" rows="80, 80" backgroundColor="#3c495e">
      <Label text="0,0" row="0" col="0" backgroundColor="red" />
      <Label text="0,1" row="0" col="1" backgroundColor="green" />
      <Label text="1,0" row="1" col="0" backgroundColor="blue" />
      <Label text="1,1" row="1" col="1" backgroundColor="yellow" />
    </GridLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将第二列的宽度设置为`auto`,这样它的大小就适合内容了。

此外，我们可以设置混合大小和合并单元格的网格布局。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <GridLayout
      columns="40, auto, *"
      rows="40, auto, *"
      backgroundColor="#3c495e"
    >
      <Label text="0,0" row="0" col="0" backgroundColor="red" />
      <Label text="0,1" row="0" col="1" colSpan="2" backgroundColor="green" />
      <Label text="1,0" row="1" col="0" rowSpan="2" backgroundColor="blue" />
      <Label text="1,1" row="1" col="1" backgroundColor="yellow" />
      <Label text="1,2" row="1" col="2" backgroundColor="lightred" />
      <Label text="2,1" row="2" col="1" backgroundColor="lightgreen" />
      <Label text="2,2" row="2" col="2" backgroundColor="lightblue" />
    </GridLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们设置了`colSpan`和`rowSpan`道具来合并列和行。

我们设置`columns`和`rows`道具来设置行和列的大小。

# StackLayout

`StacjLayout`组件允许我们添加组件并将它们显示为一列。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <StackLayout backgroundColor="#3c495e">
      <Label text="first" height="70" backgroundColor="red" />
      <Label text="second" height="70" backgroundColor="green" />
      <Label text="third" height="70" backgroundColor="blue" />
    </StackLayout>
  </Page>
</template><script >
export default {};
</script>
```

添加`Label`并将它们显示在一列中。

我们还可以通过改变`orientation`属性来显示布局内部的组件:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <StackLayout orientation="horizontal" backgroundColor="#3c495e">
      <Label text="first" width="70" backgroundColor="red" />
      <Label text="second" width="70" backgroundColor="green" />
      <Label text="third" width="70" backgroundColor="blue" />
    </StackLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们将`orientation`属性设置为`'horizontal'`来设置`Label` s 并排显示`Label` s。

# 结论

我们可以用 NativeScript Vue 添加网格布局和堆栈布局。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**