# 使用 Quasar 库开发 Vue 应用程序—滑块选项

> 原文：<https://javascript.plainenglish.io/developing-vue-apps-with-the-quasar-library-slider-options-f75a39796b0f?source=collection_archive---------15----------------------->

![](img/48a87ec9876289f6f4d0f2d962a8dc22.png)

Photo by [freddie marriage](https://unsplash.com/@fredmarriage?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Quasar 是一个流行的 Vue UI 库，用于开发好看的 Vue 应用程序。

在本文中，我们将了解如何使用 Quasar UI 库创建 Vue 应用程序。

# 滑块的自定义标签值

我们可以用`label-value`属性改变滑块的标签值:

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
  </head>
  <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <q-layout
        view="lHh Lpr lFf"
        container
        style="height: 100vh;"
        class="shadow-2 rounded-borders"
      >
        <div class="q-pa-md">
          <q-slider
            label
            :label-value="`${model}px`"
            label-always
            v-model="model"
            :min="0"
            :max="200"
          >
          </q-slider>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {
          model: 0
        }
      });
    </script>
  </body>
</html>
```

我们可以添加`markers`道具来将标记添加到滑块中:

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
  </head>
  <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <q-layout
        view="lHh Lpr lFf"
        container
        style="height: 100vh;"
        class="shadow-2 rounded-borders"
      >
        <div class="q-pa-md">
          <q-slider markers v-model="model" :min="0" :max="200"> </q-slider>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {
          model: 0
        }
      });
    </script>
  </body>
</html>
```

我们还可以添加带有`markers`道具的`snap`道具来捕捉标记:

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
  </head>
  <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <q-layout
        view="lHh Lpr lFf"
        container
        style="height: 100vh;"
        class="shadow-2 rounded-borders"
      >
        <div class="q-pa-md">
          <q-slider markers snap v-model="model" :min="0" :max="200">
          </q-slider>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {
          model: 0
        }
      });
    </script>
  </body>
</html>
```

我们可以通过附加一个`change`监听器，将模型值设置为仅当我们抬起鼠标按钮时才改变:

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
  </head>
  <body class="body--dark">
    <script src="https://cdn.jsdelivr.net/npm/vue@^2.0.0/dist/vue.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/quasar@1.12.13/dist/quasar.umd.min.js"></script>
    <div id="q-app">
      <q-layout
        view="lHh Lpr lFf"
        container
        style="height: 100vh;"
        class="shadow-2 rounded-borders"
      >
        <div class="q-pa-md">
          <q-badge color="secondary">
            {{ model }}
          </q-badge> <q-slider
            :value="model"
            @change="val => { model = val }"
            :min="0"
            :max="45"
            :step="5"
            color="purple"
            label
          >
          </q-slider>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {
          model: 0
        }
      });
    </script>
  </body>
</html>
```

我们获取具有选定值的`val`参数，然后将其值设置为`model`无功属性。

我们将`value`属性设置为`model`来显示滑块上的值。

只有当我们抬起鼠标按钮时才会发出`change`事件，所以`model`值不会经常改变。

# 结论

我们可以用 Quasar `q-slider`组件设置滑块的各种选项。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**