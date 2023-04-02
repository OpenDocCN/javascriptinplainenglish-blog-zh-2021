# Vue Konva —事件、图像和过滤器

> 原文：<https://javascript.plainenglish.io/vue-konva-events-images-and-filters-f1e2008bdf3e?source=collection_archive---------16----------------------->

![](img/b8308e195a7b0d920c315555821f4d74.png)

Photo by [Buse Doga Ay](https://unsplash.com/@busedoay?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

借助 Vue Konva 库，我们可以在 Vue 应用程序中更轻松地使用 HTML 画布。

在本文中，我们将了解如何使用 Vue Konva 来简化 Vue 应用程序中的 HTML 画布。

# 事件

有了 Vue Konva，我们可以轻松地聆听来自输入设备的事件。

例如，我们可以写:

```
<template>
  <v-stage ref="stage" :config="stageSize">
    <v-layer ref="layer">
      <v-circle
        @mousemove="handleMouseMove"
        @mouseout="handleMouseOut"
        :config="configCircle"
      />
      <v-text
        ref="text"
        :config="{
          x: 10,
          y: 10,
          fontFamily: 'Calibri',
          fontSize: 24,
          text: text,
          fill: 'black',
        }"
      />
    </v-layer>
  </v-stage>
</template><script>
const width = window.innerWidth;
const height = window.innerHeight;export default {
  data() {
    return {
      stageSize: {
        width: width,
        height: height,
      },
      text: "",
      configCircle: {
        x: 200,
        y: 200,
        radius: 70,
        fill: "red",
        stroke: "black",
        strokeWidth: 4,
      },
    };
  },
  methods: {
    writeMessage(message) {
      this.text = message;
    },
    handleMouseOut(event) {
      this.writeMessage("Mouseout circle");
    },
    handleMouseMove(event) {
      const mousePos = this.$refs.stage.getNode().getPointerPosition();
      const x = mousePos.x - 190;
      const y = mousePos.y - 40;
      this.writeMessage(`(${x}, ${y})`);
    },
  },
};
</script>
```

我们加了一个圈，听圈的`mouseover`和`mouseout`事件。

在`handleMouseMove`方法中，我们获取`v-stage`的 ref 并从中获取鼠标位置。

然后我们可以用`this.writeMessage`来设置`text`的无功属性，这个属性用在`v-text`组件中。

我们还使用`handleMouseOut`方法来监听`mouseout`事件。

# 形象

我们可以用`v-image`组件将图像添加到画布中。

例如，我们可以写:

```
<template>
  <v-stage ref="stage" :config="stageSize">
    <v-layer ref="layer">
      <v-image
        :config="{
          image,
        }"
      />
    </v-layer>
  </v-stage>
</template><script>
const width = window.innerWidth;
const height = window.innerHeight;export default {
  data() {
    return {
      stageSize: {
        width,
        height,
      },
      image: null,
    };
  },
  created() {
    const image = new window.Image();
    image.src =
      "https://i.picsum.photos/id/100/200/200.jpg?hmac=-Ffd_UnIv9DLflvK15Fq_1gRuN8t2wWU4UiuwAu4Rqs";
    image.onload = () => {
      this.image = image;
    };
  },
};
</script>
```

来增加我们的形象。

我们将`stageSize`设置为窗口的高度和宽度。

我们在`created`钩子中创建一个`Image`实例来加载图像。

`config`被设置为我们想要显示的图像。

# 过滤

我们可以添加滤镜作为形状的背景。

例如，我们可以写:

```
<template>
  <v-stage ref="stage" :config="stageSize">
    <v-layer ref="layer">
      <v-circle
        ref="circle"
        [@mousemove](http://twitter.com/mousemove)="handleMouseMove"
        :config="{
          filters,
          noise: 1,
          x: 40,
          y: 40,
          width: 50,
          height: 50,
          fill: color,
          shadowBlur: 10,
        }"
      />
    </v-layer>
  </v-stage>
</template><script>
const width = window.innerWidth;
const height = window.innerHeight;
import Konva from "konva";export default {
  data() {
    return {
      stageSize: {
        width: width,
        height: height,
      },
      color: "green",
      filters: [Konva.Filters.Noise],
    };
  },
  methods: {
    handleMouseMove() {
      this.color = Konva.Util.getRandomColor();
    },
  },
  mounted() {
    const circleNode = this.$refs.circle.getNode();
    circleNode.cache();
    circleNode.getLayer().batchDraw();
  },
  updated() {
    const circleNode = this.$refs.circle.getNode();
    circleNode.cache();
  },
};
</script>
```

我们添加了我们的`v-circle`组件。

`filters` reactive 属性拥有我们想要设置的过滤器数组。

然后我们通过将`handleMouseMove`方法设置为`mousemove`事件处理程序来监听它上面的`mousemove`事件。

在`handleMouseMove`方法中，我们将`color`反应属性设置为随机颜色。

我们将圆圈缓存在`updated`钩子中。

并在`mounted`钩上画圆。

现在，当我们将鼠标移到圆圈上时，我们会看到滤镜的颜色发生了变化。

# 结论

我们可以通过 Vue Konva 收听事件，并轻松添加图像和滤镜。