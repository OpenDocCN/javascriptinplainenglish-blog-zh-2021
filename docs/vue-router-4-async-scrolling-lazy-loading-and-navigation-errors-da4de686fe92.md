# vue Router 4–异步滚动、延迟加载和导航错误

> 原文：<https://javascript.plainenglish.io/vue-router-4-async-scrolling-lazy-loading-and-navigation-errors-da4de686fe92?source=collection_archive---------10----------------------->

![](img/8755a4e15d923d399dbe9c0cbc6dd719.png)

Photo by [Benjamin Smith](https://unsplash.com/@ifbdesign?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

**Vue Router 4 处于测试阶段，可能会有变化。**

为了轻松地构建一个单页面应用程序，我们需要添加路由，以便将 URL 映射到呈现的组件。

在这篇文章中，我们将看看如何使用 Vue 路由器 4 与 Vue 3。

# 异步滚动行为

我们可以将滚动行为改为异步。

为此，我们可以写:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://unpkg.com/vue@next"></script>
    <script src="https://unpkg.com/vue-router@4.0.0-beta.7/dist/vue-router.global.js"></script>
    <title>App</title>
  </head>
  <body>
    <div id="app">
      <p>
        <router-link to="/foo">foo</router-link>
        <router-link to="/bar">bar</router-link>
      </p>
      <router-view></router-view>
    </div>
    <script>
      const Foo = {
        template: `<div>
          <p v-for='n in 100'>{{n}}</p>
        </div>`
      };
      const Bar = {
        template: `<div>
          <p v-for='n in 100'>{{n}}</p>
        </div>`
      };
      const routes = [
        {
          path: "/foo",
          component: Foo
        },
        {
          path: "/bar",
          component: Bar
        }
      ];
      const router = VueRouter.createRouter({
        history: VueRouter.createWebHistory(),
        routes,
        scrollBehavior(to, from, savedPosition) {
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              resolve({ left: 0, top: 500 });
            }, 500);
          });
        }
      });
      const app = Vue.createApp({});
      app.use(router);
      app.mount("#app");
    </script>
  </body>
</html>
```

我们有`scrollBehavior`方法返回一个承诺，该承诺解析为一个具有滚动位置的对象。

`left`和`top`属性是 x 和 y 坐标的新属性。

它们取代了 Vue 路由器 3 中的`x`和`y`属性。

# 惰性装载路线

我们可以在应用程序中延迟加载路线。

例如，我们可以写:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="[https://unpkg.com/vue@next](https://unpkg.com/vue@next)"></script>
    <script src="[https://unpkg.com/vue-router@4.0.0-beta.7/dist/vue-router.global.js](https://unpkg.com/vue-router@4.0.0-beta.7/dist/vue-router.global.js)"></script>
    <title>App</title>
  </head>
  <body>
    <div id="app">
      <p>
        <router-link to="/foo">foo</router-link>
        <router-link to="/bar">bar</router-link>
      </p>
      <router-view></router-view>
    </div>
    <script>
      const Foo = () =>
        Promise.resolve({
          template: `<div>foo</div>`
        }); const Bar = () =>
        Promise.resolve({
          template: `<div>bar</div>`
        }); const routes = [
        {
          path: "/foo",
          component: Foo
        },
        {
          path: "/bar",
          component: Bar
        }
      ];
      const router = VueRouter.createRouter({
        history: VueRouter.createWebHistory(),
        routes
      });
      const app = Vue.createApp({});
      app.use(router);
      app.mount("#app");
    </script>
  </body>
</html>
```

我们有`Foo`和`Bar`组件。

它们是通过创建一个解析到组件定义的承诺来定义的。

使用 Webpack，我们还可以使用`import`函数来导入我们的组件。

例如，我们可以写:

```
import('./Foo.vue')
```

`import`返回解析到组件的承诺，其工作方式与上面的承诺定义相同。

# 将组件分组到同一个块中

我们可以通过创建具有以下功能的组件来将组件分组到同一个块中:

```
const Foo = () => import(/* webpackChunkName: "group-foo" */ './Foo.vue')
const Bar = () => import(/* webpackChunkName: "group-foo" */ './Bar.vue')
const Baz = () => import(/* webpackChunkName: "group-foo" */ './Baz.vue')
```

我们有带块名的`webpackChunkName`的注释。

# 导航故障

我们可以用程序导航来处理导航错误。

例如，我们可以写:

```
<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://unpkg.com/vue@next"></script>
    <script src="https://unpkg.com/vue-router@4.0.0-beta.7/dist/vue-router.global.js"></script>
    <title>App</title>
  </head>
  <body>
    <div id="app">
      <p>
        <router-link to="/foo">foo</router-link>
        <a href="#" [@click](http://twitter.com/click).stop="go">bar</a>
      </p>
      <router-view></router-view>
    </div>
    <script>
      const Foo = {
        template: `<div>foo</div>`
      }; const Bar = {
        template: `<div>bar</div>`,
        beforeRouteEnter(to, from, next) {
          next(new Error());
        }
      }; const routes = [
        {
          path: "/foo",
          component: Foo
        },
        {
          path: "/bar",
          component: Bar
        }
      ];
      const router = VueRouter.createRouter({
        history: VueRouter.createWebHistory(),
        routes
      });
      const app = Vue.createApp({
        methods: {
          go() {
            this.$router.push("/bar").catch((failure) => {
              console.log(failure);
            });
          }
        }
      });
      app.use(router);
      app.mount("#app");
    </script>
  </body>
</html>
```

处理导航错误。

我们在`Bar`组件中添加了一个`beforeRouterEnter`方法。

它用方法中的一个`Error`实例调用`next`。

这将导致`Error`实例显示在控制台中。

在根 Vue 实例中，我们有试图用`push`方法转到`/bar`路线的`go`方法。

`catch`方法的回调具有`failure`参数，该参数具有被抛出的`Error`实例。

# 结论

我们可以将滚动行为改为异步。

此外，组件可以被分组为块并延迟加载。

最后，我们可以处理编程导航引发的错误。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**