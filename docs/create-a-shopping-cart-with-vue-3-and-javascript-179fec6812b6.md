# 用 Vue 3 和 JavaScript 创建一个购物车

> 原文：<https://javascript.plainenglish.io/create-a-shopping-cart-with-vue-3-and-javascript-179fec6812b6?source=collection_archive---------15----------------------->

![](img/d1eed5b2f61d0401ab4eed3348863434.png)

Photo by [Peter Bond](https://unsplash.com/@pvsbond?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Vue 3 是易于使用的 Vue JavaScript 框架的最新版本，让我们可以创建前端应用程序。

在本文中，我们将看看如何用 Vue 3 和 JavaScript 创建一个购物车应用程序。

# 创建项目

我们可以用 Vue CLI 创建 Vue 项目。

要安装它，我们运行:

```
npm install -g @vue/cli
```

与 NPM 或:

```
yarn global add @vue/cli
```

用纱线。

然后我们运行:

```
vue create shopping-cart
```

并选择所有默认选项来创建项目。

我们还需要 Vue 路由器包，让我们导航到应用程序中的不同页面。

为此，我们运行:

```
npm i vue-router@next
```

# 创建购物车

创建购物车的第一步是创建视图文件。

我们在`src`文件夹中创建`views`文件夹。

然后在里面，我们添加了`Cart.vue`和`Store.vue`文件来创建我们可以浏览的商店页面。

`Cart.vue`有购物车页面。

然后在`main.js`中，我们通过编写以下内容将 Vue 路由器添加到我们的应用程序中:

`main.js`

```
import { createApp } from "vue";
import App from "./App.vue";
import Cart from "./views/Cart";
import Store from "./views/Store";
import { createRouter, createWebHashHistory } from "vue-router";const routes = [
  { path: "/", component: Store },
  { path: "/cart", component: Cart }
];const router = createRouter({
  history: createWebHashHistory(),
  routes
});const app = createApp(App);
app.use(router);
app.mount("#app");
```

我们导入之前创建的视图组件文件。

然后我们将它们添加到`routes`数组中。

接下来，我们调用`createRouter`来创建路由器对象。

我们添加前面在参数对象中创建的`routes`对象。

`createWebHashHistory`让 Vue 路由器在 URL 的第一段和其他段之间添加一个`#`符号。

然后我们用`router`调用`app.use`来添加路由器。

为了创建一个简单的商店页面，我们进入`Store.vue`并编写:

```
<template>
  <div>
    <h1>Store</h1>
    <div v-for="item of items" :key="item.id">
      <p>{{ item.name }}</p>
      <img :src="item.imageUrl" />
      <button @click="removeFromCart(item.id)" v-if="isInCart(item.id)">
        remove from cart
      </button>
      <button @click="addToCart(item.id)" v-else>add to cart</button>
    </div>
    <button @click="$router.push('/cart')">check out</button>
  </div>
</template><script>
const items = Object.freeze([
  {
    id: 1,
    imageUrl: "apple.jpg",
    name: "grape",
  },
  {
    id: 2,
    imageUrl: "orange.jpg",
    name: "orange",
  },
  {
    id: 3,
    imageUrl: "[g](https://sites.google.com/site/knowyourfruit/_/rsrc/1284636557816/know-your-apples/Apple%2002.jpg?height=362&width=400)rape.jpg",
    name: "apple",
  },
]);export default {
  name: "Store",
  data() {
    return {
      items,
      cart: [],
    };
  },
  methods: {
    isInCart(itemId) {
      if (!localStorage.getItem("cart")) {
        localStorage.setItem("cart", JSON.stringify([]));
      }
      const cartItem = this.cart.find(({ id }) => id === itemId);
      return Boolean(cartItem);
    },
    addToCart(itemId) {
      const item = this.items.find(({ id }) => id === itemId);
      if (!localStorage.getItem("cart")) {
        localStorage.setItem("cart", JSON.stringify([]));
      }
      const cartItems = JSON.parse(localStorage.getItem("cart"));
      cartItems.push(item);
      localStorage.setItem("cart", JSON.stringify(cartItems));
      this.cart = JSON.parse(localStorage.getItem("cart"));
    },
    removeFromCart(itemId) {
      const cartItems = JSON.parse(localStorage.getItem("cart"));
      const index = cartItems.findIndex(({ id }) => id === itemId);
      cartItems.splice(index, 1);
      localStorage.setItem("cart", JSON.stringify(cartItems));
      this.cart = JSON.parse(localStorage.getItem("cart"));
    },
  },
};
</script>
```

我们用`v-for`渲染商店物品。

如果商品已经添加到购物车顶部，我们将显示“从购物车中移除”按钮。

否则我们会显示“添加到购物车”按钮。

检查是通过`isInCart`方法完成的，该方法从`this.cart`反应属性中获取购物车商品，并检查`find`是否返回给定`itemId`的任何东西。

将条目添加到本地存储的`cart`条目中，如果条目不存在，我们就创建一个数组。

之后，我们用本地存储器中的最新值更新`this.cart`反应属性。

`removeFromCart`用`findIndex`从`itemId`本地存储的`cart`项中查找索引。

然后我们调用`splice`通过`index`移除项目。

然后我们调用`setItem`用购物车中的最新商品更新购物车。

我们用本地存储的最新值更新`this.cart`。

`items`拥有商店的物品。

结帐按钮用`'/cart'`调用`$router.push`进入购物车页面。

为了给购物车页面添加内容，我们在`Cart.vue`中编写了以下内容:

`Cart.vue`

```
<template>
  <div>
    <h1>Cart</h1>
    <div v-for="(c, index) of cart" :key="c.id">
      <p>{{ c.name }}</p>
      <img :src="c.imageUrl" />
      <button @click="removeFromCart(index)">remove from cart</button>
    </div>
  </div>
</template><script>
export default {
  name: "Cart",
  data() {
    return {
      cart: [],
    };
  },
  methods: {
    removeFromCart(itemId) {
      const cartItems = JSON.parse(localStorage.getItem("cart"));
      const index = cartItems.findIndex(({ id }) => id === itemId);
      cartItems.splice(index, 1);
      localStorage.setItem("cart", JSON.stringify(cartItems));
      this.cart = JSON.parse(localStorage.getItem("cart"));
    },
    getCart() {
      if (!localStorage.getItem("cart")) {
        localStorage.setItem("cart", JSON.stringify([]));
      }
      this.cart = JSON.parse(localStorage.getItem("cart"));
    },
  },
  beforeMount() {
    this.getCart();
  },
};
</script>
```

我们有与`Store.vue`相同的`remvoeFromCart`方法。

`getCart`从本地存储中获取`cart`项，然后将返回值设置为`this.cart`反应属性的值。

然后我们在模板中呈现带有`v-for`的`this.cart`条目。

我们有从购物车中移除按钮来移除带有`removeFromCart`的商品。

最后，在`App.vue`中，我们写道:

```
<template>
  <div>
    <router-view></router-view>
  </div>
</template><script>
export default {
  name: "App",
};
</script><style>
img {
  width: 200px;
  height: 200px;
}
</style>
```

添加`router-view`以便我们可以看到 Vue 路由器渲染的路线。

我们还使用`style`标签将图像缩小到 200 像素乘以 200 像素。

# 结论

我们可以用 Vue 3 和 JavaScript 轻松创建一个简单的购物车。

*查看更多内容请点击*[***plain English . io***](https://plainenglish.io/)