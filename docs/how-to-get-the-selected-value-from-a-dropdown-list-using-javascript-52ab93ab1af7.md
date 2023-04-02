# 如何使用 JavaScript 从下拉列表中获取选定的值？

> 原文：<https://javascript.plainenglish.io/how-to-get-the-selected-value-from-a-dropdown-list-using-javascript-52ab93ab1af7?source=collection_archive---------10----------------------->

![](img/25ee717b4ca756bba40c497ab134c244.png)

Photo by [Danial Igdery](https://unsplash.com/@ricaros?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在 JavaScript 中，获取下拉列表的选定值有时是我们必须做的事情。

在本文中，我们将看看如何用 JavaScript 从下拉列表中获取选定的值。

# 从下拉列表中获取选定的值

要从下拉列表中获取选定的值，我们可以获取 select 元素。

然后我们可以使用`value`属性来获取所选`option`元素的`value`属性的值。

例如，如果我们有下面的 HTML:

```
<select>
  <option value="1">apple</option>
  <option value="2" selected>orange</option>
  <option value="3">grape</option>
</select>
```

然后选择第二个`option`元素，因为我们已经为它添加了`selected`属性。

所以我们可以写:

```
const select = document.querySelector("select");
const selectedChoice = select.value;
console.log(selectedChoice)
```

用`document.querySelector`得到选择元素。

然后我们用`value`属性获得 select `option`元素的`value`属性的值。

然后我们应该看到`selectedChoice`是 2。

# 从下拉列表中获取所选选项元素的文本

我们还可以从下拉列表中获取 select `option`元素的文本。

为此，我们写道:

```
const select = document.querySelector("select");
const value = select.options[select.selectedIndex].value;
const text = select.options[select.selectedIndex].text;
console.log(value, text)
```

假设我们有和以前一样的 HTML 代码。

我们用`document.querySelector`得到选择元素。

然后我们在一个具有`select.options`属性的对象中获得所有选项。

`select.selectedIndex`具有所选`option`元素的索引。

`value`属性具有所选元素的`value`属性的值。

并且`text`属性具有所选元素中`option`元素的文本。

因此，`value`为 2，`text`为`'orange'`。

# 注意变化

我们可以监听下拉菜单的`change`事件来观察所选项目的选择变化。

例如，如果我们有与前两个示例相同的 select 元素，我们可以写:

```
const select = document.querySelector("select");
select.addEventListener('change', (event) => {
  const {
    value,
    text
  } = event.target.options[event.target.selectedIndex]
  console.log(value, text)
})
```

我们像以前一样得到了`select`元素。

然后我们从`event.target.options`中得到选项。

我们可以通过`event.target.selectedIndex`访问所选选项的索引。

然后我们可以用`value`属性得到`value`属性的值。

而`text`获取选项元素中选中项的文本内容。

# 结论

我们可以从具有`value`属性的 select 元素中获取选中的`option`元素，该元素具有选中的 option 元素的`value`属性的值。

我们还可以获得`options`房产的所有期权。

`selectedIndex`获取选中的`option`元素的索引。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)