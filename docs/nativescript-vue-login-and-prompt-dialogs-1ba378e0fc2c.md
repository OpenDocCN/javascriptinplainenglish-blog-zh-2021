# NativeScript Vue —登录和提示对话框

> 原文：<https://javascript.plainenglish.io/nativescript-vue-login-and-prompt-dialogs-1ba378e0fc2c?source=collection_archive---------14----------------------->

![](img/ec787143c44965f30105a0eb9cd5d85b.png)

Photo by [Phillip Larking](https://unsplash.com/@phillip_larking?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 是一个易于使用的构建前端应用的框架。

NativeScript 是一个移动应用程序框架，它允许我们使用流行的前端框架构建原生移动应用程序。

在本文中，我们将了解如何使用 NativeScript Vue 构建一个应用程序。

# 登录对话框

NativeScript Vue 带有一个登录对话框。

例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Button text="Open Dialog" @tap="openDialog" />
    </FlexboxLayout>
  </Page>
</template><script>
export default {
  methods: {
    async openDialog() {
      const result = await login("Login", "Username field", "Password field");
      const { result: res, userName, password } = result;
      console.log(res, userName, password);
    },
  },
};
</script>
```

我们有一个打开登录对话框的按钮。

`login`功能打开登录对话框。

第一个参数是消息内容。

第二个和第三个参数分别是用户名和密码输入的占位符。

然后，我们可以从解析的值中获得用户名和密码的值。

`res`有表单验证结果。

我们可以通过编写以下内容来设置更多选项:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Button text="Open Dialog" @tap="openDialog" />
    </FlexboxLayout>
  </Page>
</template><script>
export default {
  methods: {
    async openDialog() {
      const result = await login({
        title: "Login Title",
        message: "Login message",
        okButtonText: "OK",
        cancelButtonText: "Cancel",
        userName: "user",
        password: "password",
      });
      const { result: res, userName, password } = result;
      console.log(res, userName, password);
    },
  },
};
</script>
```

`title`有登录对话框标题。

`message`有登录对话框的提示信息。

`okButtonText`设置确定按钮的文本。

`cancelButtonText`设置取消按钮的文本。

`userName`设置用户名字段的默认值。

并且`password`设置密码字段的默认值。

# 提示对话框

`prompt`全局函数让我们用单行文本输入打开一个对话框。

要使用它，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Button text="Open Dialog" @tap="openDialog" />
    </FlexboxLayout>
  </Page>
</template><script>
export default {
  methods: {
    async openDialog() {
      const result = await prompt(
        "Enter something",
        "Suggested user input"
      );
      console.log(result);
    },
  },
};
</script>
```

我们有一个打开提示对话框的按钮。

`prompt`方法将对话框文本作为第一个参数，将输入的默认值作为第二个参数。

我们还可以添加更多选项。例如，我们可以写:

```
<template>
  <Page>
    <ActionBar title="NativeScript App"></ActionBar>
    <FlexboxLayout flexDirection="column">
      <Button text="Open Dialog" @tap="openDialog" />
    </FlexboxLayout>
  </Page>
</template><script>
export default {
  methods: {
    async openDialog() {
      const result = await prompt({
        title: "Title",
        message: "Enter something",
        okButtonText: "OK",
        cancelButtonText: "Cancel",
        defaultText: "Suggested value",
      });
      console.log(result);
    },
  },
};
</script>
```

我们设置`title`值来显示对话框标题。

`message`有对话框提示信息。

`okButtonText`有确定按钮文本。

`cancelButtonText`有取消按钮文本。

`defaultText`已输入默认值。

# 结论

我们可以使用 NativeScript Vue 在我们的移动应用程序中添加登录和提示对话框。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**