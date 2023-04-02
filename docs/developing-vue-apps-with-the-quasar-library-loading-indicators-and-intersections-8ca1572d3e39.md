# 使用 Quasar 库开发 Vue 应用程序—加载指示器和交叉点

> 原文：<https://javascript.plainenglish.io/developing-vue-apps-with-the-quasar-library-loading-indicators-and-intersections-8ca1572d3e39?source=collection_archive---------13----------------------->

![](img/f1b06475691645ff85ebce644a37e304.png)

Photo by [DDP](https://unsplash.com/@moino007?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Quasar 是一个流行的 Vue UI 库，用于开发好看的 Vue 应用程序。

在本文中，我们将了解如何使用 Quasar UI 库创建 Vue 应用程序。

# 装载指示器

我们可以在带有`q-inner-loading`组件的卡中添加一个加载指示器。

为了补充它，我们写道:

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
          <q-card class="bg-grey-3 relative-position card-example">
            <q-card-section class="q-pb-none">
              <div class="text-h6">Lorem Ipsum</div>
            </q-card-section> <q-card-section>
              <transition
                appear
                enter-active-class="animated fadeIn"
                leave-active-class="animated fadeOut"
              >
                <div v-show="showData">
                  Lorem ipsum dolor sit amet
                </div>
              </transition>
            </q-card-section> <q-inner-loading :showing="visible">
              <q-spinner-gears size="50px" color="primary" />
            </q-inner-loading>
          </q-card>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {
          visible: false,
          showData: false
        },
        methods: {
          showTextLoading() {
            this.visible = true;
            this.showData = false;
            setTimeout(() => {
              this.visible = false;
              this.showData = true;
            }, 3000);
          }
        },
        beforeMount() {
          this.showTextLoading();
        }
      });
    </script>
  </body>
</html>
```

`showing`道具让我们控制何时显示指示器。

# 交集

我们可以使用`q-intersection`组件作为滚动容器。

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
    <style>
      .example-item {
        height: 200px;
        width: 200px;
      }
    </style>
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
          <div class="row justify-center q-gutter-sm">
            <q-intersection
              v-for="index in 60"
              :key="index"
              class="example-item"
            >
              <q-card class="q-ma-sm">
                <img src="https://cdn.quasar.dev/img/mountains.jpg" /> <q-card-section>
                  <div class="text-h6">Card #{{ index }}</div>
                </q-card-section>
              </q-card>
            </q-intersection>
          </div>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {}
      });
    </script>
  </body>
</html>
```

我们在里面加上`q-card`来添加卡片显示物品。

我们可以添加`transition`道具来添加过渡效果:

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
    <style>
      .example-item {
        height: 200px;
        width: 200px;
      }
    </style>
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
          <div class="row justify-center q-gutter-sm">
            <q-intersection
              transition="scale"
              v-for="index in 60"
              :key="index"
              class="example-item"
            >
              <q-card class="q-ma-sm">
                <img src="https://cdn.quasar.dev/img/mountains.jpg" /> <q-card-section>
                  <div class="text-h6">Card #{{ index }}</div>
                </q-card-section>
              </q-card>
            </q-intersection>
          </div>
        </div>
      </q-layout>
    </div>
    <script>
      new Vue({
        el: "#q-app",
        data: {}
      });
    </script>
  </body>
</html>
```

# 结论

我们可以添加装载指示器，并观察与类星体的交点。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**