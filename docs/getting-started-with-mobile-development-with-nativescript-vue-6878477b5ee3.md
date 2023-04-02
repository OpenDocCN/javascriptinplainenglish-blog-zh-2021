# 使用 NativeScript Vue 开始移动开发

> 原文：<https://javascript.plainenglish.io/getting-started-with-mobile-development-with-nativescript-vue-6878477b5ee3?source=collection_archive---------13----------------------->

![](img/d8e737d136844d9652ce1b187e3dd220.png)

Photo by [Maria Teneva](https://unsplash.com/@miteneva?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 是一个易于使用的构建前端应用的框架。

NativeScript 是一个移动应用程序框架，它允许我们使用流行的前端框架构建原生移动应用程序。

在本文中，我们将了解如何使用 NativeScript Vue 构建一个应用程序。

# 安装 NativeScript

我们首先通过运行以下命令来全局安装`nativescript`节点包:

```
npm install -g nativescript
```

# 创建应用程序项目

一旦我们安装了这个包，我们通过编写以下内容来创建这个项目:"

```
$ npm install -g @vue/cli @vue/cli-init
$ vue init nativescript-vue/vue-cli-template <project-name>
$ cd <project-name>
$ npm install
```

我们安装 Vue CLI。

然后，我们用最后 3 个命令创建项目。

为了运行这个项目，我们安装了 Genymotion 模拟器来预览这个应用程序。

它将显示为一个普通的 Android 设备。

进入文件夹后，我们可以运行`tns preview`或`tns run`来运行项目。

这应该作为管理员用户来完成。然后我们可以选择 Configure for Local Build，让它安装运行项目所需的所有包。

如果启动了 Genymotion，那么您应该会看到这个项目。

# 第一个应用

一旦我们创建了我们的项目，我们应该在`components/App.vue`中有如下内容

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <GridLayout columns="*" rows="*">
      <Label class="message" :text="msg" col="0" row="0" />
    </GridLayout>
  </Page>
</template><script >
export default {
  data() {
    return {
      msg: "Hello World!",
    };
  },
};
</script><style scoped>
ActionBar {
  background-color: #53ba82;
  color: #ffffff;
}.message {
  vertical-align: center;
  text-align: center;
  font-size: 20;
  color: #333333;
}
</style>
```

这是该项目的主屏幕，我们在上面显示“Hello World”消息。

我们使用与任何 web 应用相同的 Vue 组件，但我们从它创建了一个原生应用。

# 绝对布局

我们可以用`AbsoluteLayout`组件添加具有绝对定位的元素。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <AbsoluteLayout backgroundColor="#3c495e">
      <Label
        text="10,10"
        left="10"
        top="10"
        width="100"
        height="100"
        backgroundColor="green"
      />
      <Label
        text="150,10"
        left="120"
        top="10"
        width="100"
        height="100"
        backgroundColor="green"
      />
      <Label
        text="10,150"
        left="10"
        top="120"
        width="100"
        height="100"
        backgroundColor="green"
      />
      <Label
        text="150,150"
        left="120"
        top="120"
        width="100"
        height="100"
        backgroundColor="green"
      />
    </AbsoluteLayout>
  </Page>
</template><script >
export default {};
</script>
```

添加`AbsoluteLayout`组件来添加我们的布局。

在它里面，我们有`Label`组件来添加文本框，我们在里面显示一些文本。

我们设置每个组件的`left`和`top`位置来定位它们。

# 码头布局

`DockLayout`是一个布局容器，允许我们将子元素停靠在布局的边上或中间。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="Welcome to NativeScript-Vue!" />
    <DockLayout stretchLastChild="false" backgroundColor="#3c495e">
      <Label text="left" dock="left" width="40" backgroundColor="lightgreen" />
      <Label text="top" dock="top" height="40" backgroundColor="#289062" />
      <Label text="right" dock="right" width="40" backgroundColor="lightgreen" />
      <Label
        text="bottom"
        dock="bottom"
        height="40"
        backgroundColor="#289062"
      />
    </DockLayout>
  </Page>
</template><script >
export default {};
</script>
```

我们添加`Label`组件来设置它的位置。

`dock`道具设置我们停靠的位置。

`text`属性设置标签的文本。

# 结论

我们可以使用 NativeScript Vue 创建一个本地应用程序，并轻松添加布局。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**