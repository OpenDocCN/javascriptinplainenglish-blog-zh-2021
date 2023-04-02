# 如何测试元素是否存在

> 原文：<https://javascript.plainenglish.io/how-to-test-if-a-dom-element-exists-in-a-svelte-component-with-jest-2a3d86f0abac?source=collection_archive---------5----------------------->

![](img/a20e2d2bcc8ee6ee894a3f9916547487.png)

Photo by [Marija Zaric](https://unsplash.com/@simplicity?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/existence?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

关于一个问题的快速帖子:如何测试一个元素是否存在于一个组件中。我省略了与 Jest 与 svelite kit 的[配置相关的部分，我在不久前谈到过。我只关注这个问题。](https://el3um4s.medium.com/how-to-test-sveltekit-app-with-jest-848afa8edbc7)

我想运行 3 个测试:

1.  如果一个元素存在于一个纤细的组件中
2.  如果元素存在并且包含给定的文本
3.  如果页面上不存在该项目

我用我为组件[svelet-component-info](https://github.com/el3um4s/svelte-component-info)实现的测试作为例子:

# 检查一个元素是否存在于一个瘦组件中

第一个很简单。创建组件后，我使用 [Jest](https://jestjs.io/) 来定位元素。在本例中，我在寻找一个标签为`H1`的元素:

```
expect(svelteInfo.queryByRole("heading")).toBeTruthy();
```

Jest 通过这种方式检查 Svelte 组件是否包含 ARIA 角色`heading`的元素。如果没有找到，测试失败。

# 检查元素是否有特定的文本

如果我想检查一个元素是否有特定的属性，我使用不同的代码。首先我捕捉元素

```
const title = svelteInfo.getByRole("heading");
```

然后我检查文本:

```
expect(title).toHaveTextContent("Hello");
```

我建议参考[testing-library/jest-DOM](https://github.com/testing-library/jest-dom)资源库，了解其他可用的选项。

# 检查一个项目不存在于苗条

最后，不太直观的事情:如何检查一个元素**而不是**出现在一个网页或一个苗条的元素中。在这种情况下，我使用了与第一个类似的代码，但是我没有使用`expect(..).toBeTruthy()`，而是使用了`expect(...).toBeNull()`:

```
expect(svelteInfo.queryByTestId("description")).toBeNull();
```

仅此而已。正如已经提到的，这是一个提醒未来的我如何测试一个元素的存在与否的快速注释。

感谢阅读！敬请关注更多内容。

***不要错过我的下一篇文章—报名参加我的*** [***中邮箱列表***](https://medium.com/subscribe/@el3um4s)

[](https://el3um4s.medium.com/membership) [## 通过我的推荐链接加入 Medium—Samuele

### 阅读萨缪尔的每一个故事(以及媒体上成千上万的其他作家)。不是中等会员？在这里加入一块…

el3um4s.medium.com](https://el3um4s.medium.com/membership) 

*原载于 2021 年 11 月 17 日*[*https://blog.stranianelli.com*](https://blog.stranianelli.com/how-to-test-if-dom-element-exists-with-jest-and-svelte-english/)*。*

*更多内容看*[***plain English . io***](http://plainenglish.io/)