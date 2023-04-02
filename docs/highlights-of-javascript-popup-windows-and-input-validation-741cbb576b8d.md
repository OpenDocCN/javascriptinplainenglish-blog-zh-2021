# JavaScript 的亮点——弹出窗口和输入验证

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-popup-windows-and-input-validation-741cbb576b8d?source=collection_archive---------11----------------------->

![](img/33c8385594f5a4f818bffb8eedaa8d52.png)

Photo by [R Mo](https://unsplash.com/@mooo3721?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 打开弹出窗口

我们可以用`window.open`方法打开弹出窗口。

例如，我们可以写:

```
const monkeyWindow = window.open();
```

为了给窗口添加一些内容，我们可以写:

```
const monkeyWindow = window.open();
const windowContent = `<h1>hello world</h1>`;
monkeyWindow.document.write(windowContent);
```

我们调用`monkeyWindow`上的`document.write`来显示内容。

同样，我们可以用`location.assign`方法显示 URL 的内容:

```
const monkeyWindow = window.open();
monkeyWindow.location.assign("https://www.google.com");
```

现在我们应该看到 Google 显示在新窗口中。

我们也可以写:

```
const monkeyWindow = window.open();
monkeyWindow.location.href = "https://www.google.com";
```

做同样的事情。

要关闭一个窗口，我们可以写:

```
const monkeyWindow = window.open();
monkeyWindow.location.href = "https://www.google.com";
monkeyWindow.close();
```

# 控制窗口的大小和位置

我们可以在`window.open`的第三个参数中用一个字符串设置弹出窗口的大小和位置。

例如，我们可以写:

```
const monkeyWindow = window.open("https://www.google.com", "win1", "width=420,height=380");
```

现在窗口的宽度是 420 像素，高度是 380 像素。

要改变它的位置，我们可以写:

```
const monkeyWindow = window.open("https://www.google.com", "win1", "width=420,height=380,left=200,top=100");
```

增加`left`和`top`键设定位置。

# 表单验证

我们可以在表单中添加表单验证。

例如，我们可以编写以下 HTML:

```
<form onSubmit="return checkForLastName();">
  Please enter your last name.<br>
  <input type="text" id="lastNameField">
  <input type="submit" value="Submit">
</form>
```

我们可以添加以下 JavaScript 来添加验证:

```
const checkForLastName = () => {
  if (document.getElementById("lastNameField").value.length === 0) {
    alert("Please enter your last name");
    return false;
  }
}
```

在`checkForLastName`函数中，我们获得 ID 为`lastNameField`的输入值。

如果`value`的`length`为 0，那么我们显示警报。

`onSubmit`属性值中的`return`确保我们与`checkForLastName`中的`return false`一起阻止默认提交行为，以便我们可以运行 JavaScript 验证。

为了改善用户体验，我们可以在元素上调用`focus`:

```
const checkForLastName = () => {
  const lastNameField = document.getElementById("lastNameField")
  if (lastNameField.value.length === 0) {
    alert("Please enter your last name");
    lastNameField.focus();
    return false;
  }
}
```

我们在 input 元素上调用`focus`,这样用户不用点击输入就可以输入文本。

此外，我们可以添加背景色，以便用户可以更容易地看到输入字段:

```
const checkForLastName = () => {
  const lastNameField = document.getElementById("lastNameField")
  if (lastNameField.value.length === 0) {
    alert("Please enter your last name");
    lastNameField.focus();
    lastNameField.style.background = "yellow";
    return false;
  }
  lastNameField.style.background = "white";
}
```

我们通过设置`lastNameField.style.background`属性来设置背景颜色。

# 结论

我们可以用自己的内容打开窗口。

此外，我们应该为字段添加表单验证，以便用户总是输入有效的数据。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**