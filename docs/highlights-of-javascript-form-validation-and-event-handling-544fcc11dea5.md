# JavaScript 亮点——表单验证和事件处理

> 原文：<https://javascript.plainenglish.io/highlights-of-javascript-form-validation-and-event-handling-544fcc11dea5?source=collection_archive---------5----------------------->

![](img/fa97349b5bc488e8d8e4e0e7300b18ba.png)

Photo by [Jakob Dalbjörn](https://unsplash.com/@jakobdalbjorn?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

学习 JavaScript，必须先学基础。

在本文中，我们将研究 JavaScript 语言的最基本部分。

# 下拉验证

我们可以添加验证来选择下拉字段。

例如，我们可以编写以下 HTML:

```
<form onSubmit="return checkForSelection();">
  <select id="fruits">
    <option value="" selected="selected">
      SELECT A FRUIT</option>
    <option value="apple">apple</option>
    <option value="orange">orange</option>
    <option value="grape">grape</option>    
  </select>
  <br>
  <input type="submit" value="Submit Form">
</form>
```

然后添加以下 JavaScript:

```
const checkForSelection = () => {
  if (document.getElementById("fruits").selectedIndex === 0) {
    alert("Please select a fruit.");
    return false;
  }
}
```

我们添加了一个选择元素，当我们点击提交表单时，`checkForSelection`函数就会运行。

我们添加了关键字`return`,以便停止默认的提交行为，让`checkForSelection`运行。

# 单选按钮验证

此外，我们可以向一组单选按钮添加验证。

例如，我们可以编写以下 HTML:

```
<form onSubmit="return validateRadios();">
  <input type="radio" name="r1" value="apple"> apple<br>
  <input type="radio" name="r1" value="orange"> orange<br>
  <input type="radio" name="r1" value="grape"> grape<br>
  <input type="submit" value="Submit Form">
</form>
```

以及下面的 JavaScript:

```
const validateRadios = () => {
  const radios = document.getElementsByName("r1");
  for (const r of radios) {
    if (r.checked) {
      return true;
    }
  }
  alert("Please check one.");
  return false;
}
```

我们有一个表单，其中有一堆单选按钮，它们具有相同的`name`属性值。

他们应该有相同的名字，这样他们就被认为是在同一个组。

当我们点击提交表单按钮时，运行`validateRadios`功能。

在函数中，我们通过用单选按钮的`name`属性值调用`getElementsByName`来获取所有单选按钮。

我们用 for-of 循环遍历单选按钮。

如果选中了一个，我们返回`true`。

否则，我们会显示一个警告，并返回`false`它们都没有被选中。

# 电子邮件验证

我们可以通过使用正则表达式检查输入文本的格式来验证表单字段中的电子邮件地址。

例如，我们可以编写以下 HTML:

```
<form onSubmit="return validateEmail();">
  Please enter your email.<br>
  <input type="text" id="emailField">
  <input type="submit" value="Submit">
</form>
```

并编写以下 JavaScript 代码:

```
const validateEmail = () => {
  const emailField = document.getElementById("emailField");
  const regex = /^[\w\-\.\+]+\@[a-zA-Z0-9\. \-]+\.[a-zA-z0-9]{2,4}$/;
  if (!(regex.test(emailField.value))) {
    alert("Please correct email address");
    return false;
  }
}
```

我们有`validateEmail`函数来获取 ID 为`emailField`的输入值。

然后我们调用`regex.test`方法来检查输入的值是否与 regex 格式匹配。

如果没有，那么我们显示一个警告并返回`false`。

关键字`return`让我们阻止默认提交行为的运行。

# 处理事件

我们可以将事件监听器附加到 HTML 元素上。

例如，我们可以编写以下 HTML:

```
<input type="button" value="Click" id='button1'>
```

并编写以下 JavaScript:

```
const b1 = document.getElementById("button1");
const sayHello = () => {
  alert('hello');
}
b1.onclick = sayHello;
```

我们用`getElementById`得到按钮。

然后我们将`onclick`属性设置为`sayHello`事件处理函数。

这些功能通过`alert`功能显示警报。

现在，当我们点击按钮时，我们显示警告。

# 结论

我们可以向 HTML 元素添加表单验证和添加事件处理程序，这样当用户对元素做某些事情时，我们就可以做我们想做的事情。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**