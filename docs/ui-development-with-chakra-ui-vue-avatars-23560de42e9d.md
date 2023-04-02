# 使用 Chakra UI Vue 开发 UI——头像

> 原文：<https://javascript.plainenglish.io/ui-development-with-chakra-ui-vue-avatars-23560de42e9d?source=collection_archive---------19----------------------->

![](img/b0226cffb6632f765514c479c68baa37.png)

Photo by [Elena Mozhvilo](https://unsplash.com/@miracleday?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Chakra UI Vue 是一个为 Vue.js 制作的 UI 框架，让我们可以将好看的 UI 组件添加到我们的 Vue 应用程序中。

本文将介绍如何开始使用 Chakra UI Vue 进行 UI 开发。

# 神使

查克拉 UI Vue 自带头像组件。

例如，我们可以写:

```
<template>
  <c-box>
    <c-avatar name="dog" src="https://picsum.photos/id/237/200" />
  </c-box>
</template>
<script>
import { CAvatar, CBox } from "@chakra-ui/vue";
export default {
  components: {
    CAvatar,
    CBox,
  },
};
</script>
```

注册`CAvatar`组件以添加头像图像。

`src`道具有图片的 URL。

`name`有图像的文字描述。

我们可以设置`size`道具来设置它的大小。

可能的值有`2xs`、`xs`、`sm`、`md`、`lg`、`xl`和`2xl`，其中`2xs`最小，`2xl`最大。

所以我们可以写:

```
<template>
  <c-box>
    <c-avatar size="lg" name="dog" src="https://picsum.photos/id/237/200" />
  </c-box>
</template>
<script>
import { CAvatar, CBox } from "@chakra-ui/vue";
export default {
  components: {
    CAvatar,
    CBox,
  },
};
</script>
```

使头像比默认的大。

我们可以用`CAvatarBagde`组件在头像右下角添加一个徽章:

```
<template>
  <c-box>
    <c-avatar size="lg" name="dog" src="https://picsum.photos/id/237/200">
      <c-avatar-badge size="1.0em" bg="green.500" />
    </c-avatar>
  </c-box>
</template>
<script>
import { CAvatar, CAvatarBadge, CBox } from "@chakra-ui/vue";
export default {
  components: {
    CAvatar,
    CAvatarBadge,
    CBox,
  },
};
</script>
```

`size`设置尺寸，`bg`设置背景颜色。

# 结论

我们可以使用 Chakra UI Vue 轻松地将头像添加到 Vue 应用程序中。

*更多内容请看* [***说白了就是***](https://plainenglish.io/) *。报名参加我们的* [***免费每周简讯***](http://newsletter.plainenglish.io/) *。关注我们*[***Twitter***](https://twitter.com/inPlainEngHQ)*和*[***LinkedIn***](https://www.linkedin.com/company/inplainenglish/)*。加入我们的* [***社区不和谐***](https://discord.gg/GtDtUAvyhW) *。*