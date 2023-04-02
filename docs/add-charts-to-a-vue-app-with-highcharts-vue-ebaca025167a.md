# 使用 Highcharts-Vue 向 Vue 应用程序添加图表

> 原文：<https://javascript.plainenglish.io/add-charts-to-a-vue-app-with-highcharts-vue-ebaca025167a?source=collection_archive---------7----------------------->

![](img/2f52a5672b781de33937588c18a206b3.png)

Photo by [William Iven](https://unsplash.com/@firmbee?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Highcharts-Vue 是一个易于使用的库，允许我们将图表添加到我们的 Vue 应用程序中。

在本文中，我们将了解如何使用 highcharts-vue 库添加图表。

# 入门指南

我们可以通过运行以下命令来安装 highcharts-vue 库:

```
npm i highcharts-vue highcharts
```

`highcharts-vue`库需要`highcharts`库。

然后我们可以通过编写来添加一个简单的图表:

`main.js`

```
import Vue from "vue";
import HighchartsVue from "highcharts-vue";
import App from "./App.vue";Vue.config.productionTip = false;
Vue.use(HighchartsVue);new Vue({
  render: (h) => h(App)
}).$mount("#app");
```

`App.vue`

```
<template>
  <div id="app">
    <highcharts :options="chartOptions"></highcharts>
  </div>
</template><script>
import { Chart } from "highcharts-vue";export default {
  name: "App",
  data() {
    return {
      chartOptions: {
        series: [
          {
            data: [1, 2, 3],
          },
        ],
      },
    };
  },
  components: {
    highcharts: Chart,
  },
};
</script>
```

我们调用`Vue.use(HighchartsVue)`来注册图表库。

然后，我们通过将`Chart`组件放入`comnponents`属性中，将其注册到`App.vue`中。

然后我们用`options`道具将`highcharts`组件添加到模板中。

它被设置为具有数据的`series.data`属性的`chartOptions`反应属性。

# 股票图表

我们可以通过向`highcharts`组件传递更多的道具来添加股票图表。

为此，我们写道:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import Highcharts from "highcharts";
import Stock from "highcharts/modules/stock";
import HighchartsVue from "highcharts-vue";Stock(Highcharts);
Vue.use(HighchartsVue);new Vue({
  el: "#app",
  render: (h) => h(App)
});
```

`App.vue`

```
<template>
  <div>
    <highcharts
      :constructorType="'stockChart'"
      class="hc"
      :options="chartOptions"
      ref="chart"
    ></highcharts>
  </div>
</template><script>
export default {
  data() {
    return {
      chartOptions: {
        series: [
          {
            data: [1, 2, 3],
          },
        ],
      },
    };
  },
};
</script>
```

在`main.js`中，我们用`Highcharts`调用`Stock`函数，让我们添加一个股票图表。

然后在`App.vue`中，我们像之前一样将`constructorType`道具设置为`'stockChart’`和`options`。

# 地图图表

我们可以使用 Highcharts-Vue 轻松添加地图图表。

我们需要安装`@highcharts/map-collection`库来添加地图图表。

要安装它，我们运行:

```
npm i @highcharts/map-collection
```

然后，我们写道:

`main.js`

```
import Vue from "vue";
import App from "./App.vue";
import Highcharts from "highcharts";
import Maps from "highcharts/modules/map";
import HighchartsVue from "highcharts-vue";Maps(Highcharts);
Vue.use(HighchartsVue);new Vue({
  el: "#app",
  render: (h) => h(App)
});
```

`App.vue`

```
<template>
  <div>
    <highcharts
      :constructorType="'mapChart'"
      class="hc"
      :options="chartOptions"
      ref="chart"
    ></highcharts>
  </div>
</template><script>
import worldMap from "@highcharts/map-collection/custom/world.geo.json";export default {
  data() {
    return {
      chartOptions: {
        chart: {
          map: worldMap,
        },
        title: {
          text: "Highmaps",
        },
        subtitle: {
          text: "<b>World map</b>",
        },
        mapNavigation: {
          enabled: true,
          buttonOptions: {
            alignTo: "spacingBox",
          },
        },
        colorAxis: {
          min: 0,
        },
        series: [
          {
            name: "Random data",
            states: {
              hover: {
                color: "#BADA55",
              },
            },
            dataLabels: {
              enabled: true,
              format: "{point.name}",
            },
            allAreas: false,
            data: [
              ["fo", 0],
              ["um", 1],
              ["us", 2],
              ["jp", 3],
              ["sc", 4],
              ["in", 5],
              ["fr", 6],
              ["fm", 7],
              ["cn", 8],
              ["pt", 9],
              ["sw", 10],
              ["sh", 11],
              ["br", 12],
              ["ki", 13],
              ["ph", 14],
              ["mx", 15],
              ["es", 16],
              ["bu", 17],
              ["mv", 18],
              ["sp", 19],
              ["gb", 20],
              ["gr", 21],
              ["as", 22],
              ["dk", 23],
              ["gl", 24],
              ["gu", 25],
              ["mp", 26],
              ["pr", 27],
              ["vi", 28],
              ["ca", 29],
              ["st", 30],
              ["cv", 31],
              ["dm", 32],
              ["nl", 33],
              ["jm", 34],
              ["ws", 35],
              ["om", 36],
              ["vc", 37],
              ["tr", 38],
              ["bd", 39],
              ["lc", 40],
              ["nr", 41],
              ["no", 42],
              ["kn", 43],
              ["bh", 44],
              ["to", 45],
              ["fi", 46],
              ["id", 47],
              ["mu", 48],
              ["se", 49],
              ["tt", 50],
              ["my", 51],
              ["pa", 52],
              ["pw", 53],
              ["tv", 54],
              ["mh", 55],
              ["cl", 56],
              ["th", 57],
              ["gd", 58],
              ["ee", 59],
              ["ag", 60],
              ["tw", 61],
              ["bb", 62],
              ["it", 63],
              ["mt", 64],
              ["vu", 65],
              ["sg", 66],
              ["cy", 67],
              ["lk", 68],
              ["km", 69],
              ["fj", 70],
              ["ru", 71],
              ["va", 72],
              ["sm", 73],
              ["kz", 74],
              ["az", 75],
              ["tj", 76],
              ["ls", 77],
              ["uz", 78],
              ["ma", 79],
              ["co", 80],
              ["tl", 81],
              ["tz", 82],
              ["ar", 83],
              ["sa", 84],
              ["pk", 85],
              ["ye", 86],
              ["ae", 87],
              ["ke", 88],
              ["pe", 89],
              ["do", 90],
              ["ht", 91],
              ["pg", 92],
              ["ao", 93],
              ["kh", 94],
              ["vn", 95],
              ["mz", 96],
              ["cr", 97],
              ["bj", 98],
              ["ng", 99],
              ["ir", 100],
              ["sv", 101],
              ["sl", 102],
              ["gw", 103],
              ["hr", 104],
              ["bz", 105],
              ["za", 106],
              ["cf", 107],
              ["sd", 108],
              ["cd", 109],
              ["kw", 110],
              ["de", 111],
              ["be", 112],
              ["ie", 113],
              ["kp", 114],
              ["kr", 115],
              ["gy", 116],
              ["hn", 117],
              ["mm", 118],
              ["ga", 119],
              ["gq", 120],
              ["ni", 121],
              ["lv", 122],
              ["ug", 123],
              ["mw", 124],
              ["am", 125],
              ["sx", 126],
              ["tm", 127],
              ["zm", 128],
              ["nc", 129],
              ["mr", 130],
              ["dz", 131],
              ["lt", 132],
              ["et", 133],
              ["er", 134],
              ["gh", 135],
              ["si", 136],
              ["gt", 137],
              ["ba", 138],
              ["jo", 139],
              ["sy", 140],
              ["mc", 141],
              ["al", 142],
              ["uy", 143],
              ["cnm", 144],
              ["mn", 145],
              ["rw", 146],
              ["so", 147],
              ["bo", 148],
              ["cm", 149],
              ["cg", 150],
              ["eh", 151],
              ["rs", 152],
              ["me", 153],
              ["tg", 154],
              ["la", 155],
              ["af", 156],
              ["ua", 157],
              ["sk", 158],
              ["jk", 159],
              ["bg", 160],
              ["qa", 161],
              ["li", 162],
              ["at", 163],
              ["sz", 164],
              ["hu", 165],
              ["ro", 166],
              ["ne", 167],
              ["lu", 168],
              ["ad", 169],
              ["ci", 170],
              ["lr", 171],
              ["bn", 172],
              ["iq", 173],
              ["ge", 174],
              ["gm", 175],
              ["ch", 176],
              ["td", 177],
              ["kv", 178],
              ["lb", 179],
              ["dj", 180],
              ["bi", 181],
              ["sr", 182],
              ["il", 183],
              ["ml", 184],
              ["sn", 185],
              ["gn", 186],
              ["zw", 187],
              ["pl", 188],
              ["mk", 189],
              ["py", 190],
              ["by", 191],
              ["cz", 192],
              ["bf", 193],
              ["na", 194],
              ["ly", 195],
              ["tn", 196],
              ["bt", 197],
              ["md", 198],
              ["ss", 199],
              ["bw", 200],
              ["bs", 201],
              ["nz", 202],
              ["cu", 203],
              ["ec", 204],
              ["au", 205],
              ["ve", 206],
              ["sb", 207],
              ["mg", 208],
              ["is", 209],
              ["eg", 210],
              ["kg", 211],
              ["np", 212],
            ],
          },
        ],
      },
    };
  },
};
</script>
```

在`main.js`中，我们调用`Maps`函数来创建地图。

我们导入`worldMap`组件来添加地图图表。

我们把所有的选项放在`charrOptions`对象中。

`title`有主标题。

`subtitle`有副标题。

`mapNaviation`让我们为地图添加导航功能。

`colorAxis`有颜色轴选项。`min`是轴的最小值。

`series`有数据。

`dataLabels`让我们格式化数据标签。

# 结论

我们可以用 Highcharts-Vue 创建各种图表。

*更多内容看*[***plain English . io***](http://plainenglish.io)