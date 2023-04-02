# 使用 Quasar 库开发 Vue 应用——断点和 Flexbox

> 原文：<https://javascript.plainenglish.io/developing-vue-apps-with-the-quasar-library-breakpoints-and-flexbox-ce9558c1f684?source=collection_archive---------11----------------------->

![](img/4de51e9ad4c6a0a36bd627ad8a6d85bd.png)

Photo by [Priscilla Du Preez](https://unsplash.com/@priscilladupreez?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Quasar 是一个流行的 Vue UI 库，用于开发好看的 Vue 应用程序。

在本文中，我们将了解如何使用 Quasar UI 库创建 Vue 应用程序。

# 断点

Quasar 使用以下断点:

*   `xs` —高达 599 像素
*   `sm` —高达 1023 像素
*   `md` —高达 1439 像素
*   `lg` —高达 1919 像素
*   `xl` —大于 1920 像素

# Flexbox

Quasar 附带了 flexbox 助手类。

我们可以用`row`类创建行，用`col`类创建列。

例如，我们可以写:

```
<!DOCTYPE html>
<html>
  <head>
    <link
      href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900|Material+Icons"
      rel="stylesheet"
      type="text/css"
    />
    <link
      href="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.min.css"
      rel="stylesheet"
      type="text/css"
    />
  </head> <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <div class="row">
        <div class="col">
          .col
        </div>
        <div class="col">
          .col
        </div>
      </div>
    </div> <script>
      new Vue({
        el: "#q-app",
        data() {
          return {};
        },
        methods: {}
      });
    </script>
  </body>
</html>
```

`col`类将把行分成大小相等的列。

# 设置一个列宽

我们可以指定一列的列宽。

例如，我们可以写:

```
<!DOCTYPE html>
<html>
  <head>
    <link
      href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900|Material+Icons"
      rel="stylesheet"
      type="text/css"
    />
    <link
      href="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.min.css"
      rel="stylesheet"
      type="text/css"
    />
  </head> <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <div class="row">
        <div class="col">
          .col
        </div>
        <div class="col-6">
          .col-6
        </div>
        <div class="col">
          .col
        </div>
      </div>
    </div> <script>
      new Vue({
        el: "#q-app",
        data() {
          return {};
        },
        methods: {}
      });
    </script>
  </body>
</html>
```

我们将中间列的类设置为`col-6`以使其更宽。

一列的最大宽度是 12 个单位。

# 可变宽度内容

我们可以用 Quasar 添加可变宽度的内容。

例如，我们可以写:

```
<!DOCTYPE html>
<html>
  <head>
    <link
      href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900|Material+Icons"
      rel="stylesheet"
      type="text/css"
    />
    <link
      href="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.min.css"
      rel="stylesheet"
      type="text/css"
    />
  </head> <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <div class="row">
        <div class="col-12 col-md-2">
          .col-12 .col-md-2
        </div>
        <div class="col-12 col-md-auto">
          .col-12 .col-md-auto
        </div>
        <div class="col-12 col-md-2">
          .col-12 .col-md-2
        </div>
      </div>
    </div> <script>
      new Vue({
        el: "#q-app",
        data() {
          return {};
        },
        methods: {}
      });
    </script>
  </body>
</html>
```

当断点为`md`时，我们需要`col-md-2`使列宽为 2。

`col-md-auto`自动调整宽度。

# 对齐

我们可以用 Quasar 提供的类来改变 flexbox 容器中元素的对齐方式。

例如，我们可以写:

```
<!DOCTYPE html>
<html>
  <head>
    <link
      href="https://fonts.googleapis.com/css?family=Roboto:100,300,400,500,700,900|Material+Icons"
      rel="stylesheet"
      type="text/css"
    />
    <link
      href="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.min.css"
      rel="stylesheet"
      type="text/css"
    />
  </head> <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <div class="row items-start">
        <div class="col">
          1
        </div>
        <div class="col">
          2
        </div>
        <div class="col">
          3
        </div>
      </div>
    </div> <script>
      new Vue({
        el: "#q-app",
        data() {
          return {};
        },
        methods: {}
      });
    </script>
  </body>
</html>
```

我们用`items-start`类将所有的列 div 放在容器的顶部。

还有一个`items-center`类使子元素垂直居中，`items-end`使子元素底部对齐。

# 结论

我们可以使用 Quasar 提供的类来定位和调整元素的大小。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**