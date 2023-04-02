# 将 React 组件转换为 Vue.js

> 原文：<https://javascript.plainenglish.io/convert-a-reactjs-component-to-vuejs-49b3d132fd8b?source=collection_archive---------13----------------------->

![](img/b43d938909b82c68848189c55557258e.png)

> 在本教程中，我们将把 React by [Florin Pop](https://www.youtube.com/watch?v=tcUVUBlyXX8) 内置的时间线组件重写为 Vue.js。你可以在这里看到组件的运行[。](https://www.florin-pop.com/timeline/)

## 使用 [Vite](https://vitejs.dev/) 搭建你的 Vue.js 应用

只要有机会，我都会尝试使用 Vite。

由于即时服务器启动和闪电般快速的 HMR(热模块替换)等特性，它极大地提高了开发速度。

1.  让我们初始化我们的项目:

```
npm init vite@latest
```

1.  按照提示选择`vue`作为我们的框架和变体。
2.  `cd`放入生成的目录，用`npm install`安装依赖项。
3.  使用`npm run dev`运行新的 Vite + Vue.js 项目。

## 构建 Vue.js 组件

现在，有趣的事情。让我们开始转换 React 代码。

## `App.vue`看起来很像 React 版本:

```
// App.vue
<script setup>
import Timeline from './components/Timeline.vue'
</script>

<template>
  <Timeline />
</template>// React Version
const App = () => (
  <>
    <h1>React Timeline</h1>
    <Timeline />
  </>
)
```

这里的关键区别是[模板标签](https://vuejs.org/v2/guide/syntax.html)，这是 Vue.js 语法的重要部分。

## 现在让我们深入研究时间轴组件— `Timeline.vue`

时间轴组件是数据收集和容器发生的地方。

在本例中，我们从本地`data.json`文件中收集数据。使用像 [axios](https://axios-http.com/) 这样的软件包，让这个组件处理实时数据应该不需要太多额外的工作。

虽然 React 版本占用的垂直空间更少，但 Vue.js 版本更容易阅读。我们使用`v-for`来应用相同的功能，而不是应用内联映射函数。

Vue.js 将动态数据附加到一个名为 [v-bind](https://vuejs.org/v2/api/#v-bind) 的属性中。v-bind 的简写是`:`。如你所见`:data=data`是等同于`data={data}`的 Vue.js。

还要注意，Vue.js 不使用`className`来应用它的 CSS。相反，您可以使用经典的`class`关键字。

```
// React Version
const Timeline = () =>
  timelineData.length > 0 && (
    <div className="timeline-container">
      {timelineData.map((data, idx) => (
        <TimelineItem data={data} key={idx} />
      ))}
    </div>
  )// components/Timeline.vue

<template>
  <div class="timeline-container">
    <TimelineItem v-for="(data, idx) in timelineData" :data="data" :key="idx" />
  </div>
</template>

<script>
import json from '../assets/data.json'
import TimelineItem from './TimelineItem.vue'

export default {
  components: {
    TimelineItem,
  },
  data: () => ({
    timelineData: json,
  }),
}
</script>
```

以下是数据的一个示例:

```
[
  {
     "text": "Started working on the app-ideas repository",
     "date": "February 25 2021",
     "category": {
        "tag": "app-ideas",
        "color": "#FFDB14"
     },
     "link": {
        "url": "https://github.com/florinpop17/app-ideas",
        "text": "Check it out on GitHub"
     }
  },
  ...
]
```

## 将 TimelineItem 组件转换为 Vue.js

TimelineItem 组件是大多数 UI 逻辑发生的地方。我们现在正在处理我们在时间轴组件中收集的数据。

除了析构数据对象和根据需要进行样式化之外，没有发生太多事情。

我们在 Vue.js 中销毁数据的方式不同于在 React 中。

*   当在两个 HTML 元素之间使用数据时，你必须用两个花括号`{{}}`来解构它
*   当访问一个`v-bind:`中的数据时，你使用单个花括号`{data}`来析构它
*   当访问指令中的数据时，比如`v-if`，你输入数据`v-if="data"`

```
const TimelineItem = ({ data }) => (
  <div className="timeline-item">
    <div className="timeline-item-content">
      <span className="tag" style={{ background: data.category.color }}>
        {data.category.tag}
      </span>
      <time>{data.date}</time>
      <p>{data.text}</p>
      {data.link && (
        <a href={data.link.url} target="_blank" rel="noopener noreferrer">
          {data.link.text}
        </a>
      )}
      <span className="circle" />
    </div>
  </div>
)// components/TimelineItem.vue
<template>
  <div class="timeline-item">
    <div class="timeline-item-content">
      <span class="tag" :style="{ background: `${data.category.color}` }">
        {{ data.category.tag }}
      </span>
      <time>{{ data.date }}</time>
      <p>{{ data.text }}</p>
      <a
        v-if="data.link"
        :href="data.link.url"
        target="_blank"
        rel="noopener noreferrer"
      >
        {{ data.link.text }}
      </a>
      <span class="circle" />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
}
</script>

<style></style>
```

## 附加 Vue.js 配置

为了让下面提供的 CSS 样式化我们的组件，我们需要公开 CSS 以在我们的 Vue.js 应用程序中工作。对于这个例子，我在我的`main.js`文件中放置了一个导入语句。

```
import { createApp } from 'vue'
import App from './App.vue'

import './assets/main.css'

createApp(App).mount('#app')
```

## 使用 CSS 样式化组件

对于这个组件，我使用放置在我们的`assets`目录中的`main.css`文件。下面是该组件中使用的 CSS:

```
/* assets/main.css */
@import url('https://fonts.googleapis.com/css?family=Lato');

* {
  box-sizing: border-box;
}

body {
  background-image: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);

  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;

  min-height: 100vh;
  font-family: 'Lato', sans-serif;
  margin: 0;
}

h1 {
  text-align: center;
}

#app {
  padding: 0 20px;
  width: 100%;
}

.timeline-container {
  display: flex;
  flex-direction: column;
  position: relative;
  margin: 40px 0;
}

.timeline-container::after {
  background-color: #e17b77;
  content: '';
  position: absolute;
  left: calc(50% - 2px);
  width: 4px;
  height: 100%;
}

.timeline-item {
  display: flex;
  justify-content: flex-end;
  padding-right: 30px;
  position: relative;
  margin: 10px 0;
  width: 50%;
}

.timeline-item:nth-child(odd) {
  align-self: flex-end;
  justify-content: flex-start;
  padding-left: 30px;
  padding-right: 0;
}

.timeline-item-content {
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  border-radius: 5px;
  background-color: #fff;
  display: flex;
  flex-direction: column;
  align-items: flex-end;
  padding: 15px;
  position: relative;
  width: 400px;
  max-width: 70%;
  text-align: right;
}

.timeline-item-content::after {
  content: ' ';
  background-color: #fff;
  box-shadow: 1px -1px 1px rgba(0, 0, 0, 0.2);
  position: absolute;
  right: -7.5px;
  top: calc(50% - 7.5px);
  transform: rotate(45deg);
  width: 15px;
  height: 15px;
}

.timeline-item:nth-child(odd) .timeline-item-content {
  text-align: left;
  align-items: flex-start;
}

.timeline-item:nth-child(odd) .timeline-item-content::after {
  right: auto;
  left: -7.5px;
  box-shadow: -1px 1px 1px rgba(0, 0, 0, 0.2);
}

.timeline-item-content .tag {
  color: #fff;
  font-size: 12px;
  font-weight: bold;
  top: 5px;
  left: 5px;
  letter-spacing: 1px;
  padding: 5px;
  position: absolute;
  text-transform: uppercase;
}

.timeline-item:nth-child(odd) .timeline-item-content .tag {
  left: auto;
  right: 5px;
}

.timeline-item-content time {
  color: #777;
  font-size: 12px;
  font-weight: bold;
}

.timeline-item-content p {
  font-size: 16px;
  line-height: 24px;
  margin: 15px 0;
  max-width: 250px;
}

.timeline-item-content a {
  color: #333;
  text-decoration: none;
  font-size: 14px;
  font-weight: bold;
}

.timeline-item-content a::after {
  content: ' ►';
  font-size: 12px;
}

.timeline-item-content .circle {
  background-color: #fff;
  border: 3px solid #e17b77;
  border-radius: 50%;
  position: absolute;
  top: calc(50% - 10px);
  right: -40px;
  width: 20px;
  height: 20px;
  z-index: 100;
}

.timeline-item:nth-child(odd) .timeline-item-content .circle {
  right: auto;
  left: -40px;
}

@media only screen and (max-width: 1023px) {
  .timeline-item-content {
    max-width: 100%;
  }
}

@media only screen and (max-width: 767px) {
  .timeline-item-content,
  .timeline-item:nth-child(odd) .timeline-item-content {
    padding: 15px 10px;
    text-align: center;
    align-items: center;
  }

  .timeline-item-content .tag {
    width: calc(100% - 10px);
    text-align: center;
  }

  .timeline-item-content time {
    margin-top: 20px;
  }

  .timeline-item-content a {
    text-decoration: underline;
  }

  .timeline-item-content a::after {
    display: none;
  }
}

footer {
  background-color: #222;
  color: #fff;
  font-size: 14px;
  bottom: 0;
  position: fixed;
  left: 0;
  right: 0;
  text-align: center;
  z-index: 999;
}

footer p {
  margin: 10px 0;
}

footer i {
  color: red;
}

footer a {
  color: #3c97bf;
  text-decoration: none;
}
```

## 额外资源

*   带有源代码的 Github 库—[https://github.com/CodyBontecou/timeline-component-vuejs](https://github.com/CodyBontecou/timeline-component-vuejs)
*   Florin Pop 制作了一个 [YouTube 视频](https://www.youtube.com/watch?v=tcUVUBlyXX8)演示如何使用 React 构建这个组件。
*   [反应码打开](https://codepen.io/FlorinPop17/pen/GLEPZy)

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***