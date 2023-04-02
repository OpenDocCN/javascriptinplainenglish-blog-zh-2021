# 如何检查 HTML 元素中的文本溢出省略号？

> 原文：<https://javascript.plainenglish.io/how-to-check-for-text-overflow-ellipsis-in-an-html-element-52d32c720c3e?source=collection_archive---------2----------------------->

![](img/ced00441cdfe6f9a39f66b278a3e91f2.png)

Photo by [Nareeta Martin](https://unsplash.com/@splashabout?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

有时，我们希望检查`text-overflow`省略号是否在元素中呈现。

在本文中，我们将看看如何检查 HTML 元素中的`text-overflow`省略号。

# 检查 offsetWidth 是否小于 scrollWidth

元素的`offsetWidth`属性告诉我们元素在屏幕上呈现的宽度。

`scrollWidth`告诉我们元素的宽度，包括截断的部分。

因此，我们可以通过检查`offsetWidth`是否小于`scrollWidth`来判断一段文本是否被 CSS `text-overflow`属性截断。

例如，如果我们有下面的 HTML:

```
<div>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Aliquam in neque laoreet, venenatis quam id, tristique ipsum. Sed augue ipsum, pharetra in ipsum eget, varius placerat odio. Pellentesque a luctus metus, commodo placerat elit. Nullam efficitur augue in magna consectetur finibus. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Cras porttitor lectus pretium, placerat nulla eget, hendrerit magna. Nunc in sem dui. Sed sollicitudin sem a massa malesuada cursus. Mauris feugiat enim sit amet efficitur lobortis.
</div>
```

和 CSS:

```
div {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}
```

然后，我们可以通过编写以下内容来进行检查:

```
const isEllipsisActive = (e) => {
  return (e.offsetWidth < e.scrollWidth);
}const div = document.querySelector('div')
console.log(isEllipsisActive(div))
```

我们在`isEllipsisActive`函数中指定的`offsetWidth`和`scrollWidth`之间进行比较。

然后我们用`querySelector`获取 div，并将其传递给`isEllipsisActive`。

所以控制台日志应该记录`true`，因为我们用 CSS 截断了文本。

# 结论

我们可以通过检查元素的`offsetWidth`是否小于其`scrollWidth`来检查一段文本是否被 CSS `text-overflow`属性截断。

*更多内容请看*[***plain English . io***](http://plainenglish.io)