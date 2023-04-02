# Vue.js 您应该采用的最佳实践

> 原文：<https://javascript.plainenglish.io/vue-js-best-practices-you-should-adopt-3f3b3a8abace?source=collection_archive---------3----------------------->

## 使用 Vue.js 时的最佳实践

![](img/32c37ce2e8e455748d1a01a2bc556e68.png)

Image by author — [John Philip](https://medium.com/u/c2cdb19c0977?source=post_page-----3f3b3a8abace--------------------------------)

Vue.js 是一个用于构建用户界面的渐进式框架。与其他整体框架不同，Vue 从一开始就被设计成可增量采用的。

Vue.js 是一个神奇的框架，有很多超能力。在创建简单和复杂的应用程序时，Vue.js 都非常出色。

像任何其他框架一样，使用 Vue.js 有很多现成的规则。在本文中，我们将探讨一些在创建 Vue.js 应用程序时可以采用的最佳实践。

除了其他常见的编程原则之外，这些实践对于确保应用程序结构的可理解性和可维护性是必不可少的。

## **命名约定**

Vue.js 在创建应用程序时大量基于组件。

在 Vue.js 中创建和命名组件时，按照 Pascal 大小写命名约定命名组件被认为是一种最佳实践。

Pascal case 是一种编程命名约定，其中变量中每个复合词的第一个字母都是大写的。

根据 [Vue](https://v3.vuejs.org/) 的说法，PascalCase 与代码编辑器中的自动完成功能配合得最好，因为它与我们在 JS(X)和模板中引用组件的方式一致，只要有可能。然而，混合大小写的文件名有时会在不区分大小写的文件系统上产生问题，这就是为什么 kebab-case 也是完全可以接受的。

所以，假设我们有一个组件想用作侧边栏组件。

我们可以实现它，并将其命名如下:

## 不良做法

侧栏。某视频剪辑软件

## 良好实践

SideBar.vue

侧栏. vue

## **使用 v-for 和 v-if 指令**

在开发 Vue.js 应用程序时，我们有时倾向于使用 v-for 和 v-if 指令。

这些指令是 Vue.js 中最常用的一些指令。可能有一天我们需要在同一个元素上同时使用它们。

当我们在 Vue.js 中使用这两个指令时，尤其是使用 Vue 3 时，v-if 往往比 v-for 具有更高的优先级。

避免在同一个元素上同时使用这两种方法被认为是更好的做法，因为这可能会导致语法不明确。

实现这一点的一种方法不是在模板级别进行管理，而是创建一个计算属性来过滤出可见元素的列表。

## **始终使用:v-内的键代表指令**

V-for 是一个 Vue.js 指令，用于循环数组或对象中的元素。

在 Vue 2 和更高版本的 Vue 中，我们可以使用 child 并把它放在 children 元素上。

## 不良做法

```
<! — Vue 2.x →<div v-for=”photo in photos”> <p :key=”’Photo’ + photo.id”>…</p></div>
```

在 Vue.js 3 中，强烈建议将:键放在 v-for 的标签元素上，而不是放在子标签上。

## 良好实践

```
<! — Vue 3.x →<div v-for=”photo in photos” :key=”photo.id”> <p>{{item}}</p></div>
```

## **数据**

数据是 Vue.js 中的一个重要组成部分。它使我们能够相应地存储状态。有些人倾向于做的是，他们总是不把它作为函数返回。

## 不良做法

```
data: {

photo: [],
user: ‘John Philip’ }
```

## 良好实践

数据应该总是被声明为返回某些东西的函数。

```
data(){return{photo: [],
user: ‘John Philip’}
}
```

这是开发 Vue.js 应用程序时最佳实践系列的第一篇文章。在下一篇文章中，我们将看看在使用 Vue.js 开发应用程序时要实现的一些最佳实践。

在使用 Vue.js 时，您有什么可以推荐的最佳实践吗？不要犹豫，在评论区分享它们。我也想向你学习更多。

## **最终想法**

如果你喜欢读这篇文章，并且认为其他人也会喜欢，不要犹豫，分享它。

如果你觉得我遗漏了什么，请不吝赐教，指出来。

## **更读着**

[](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [## 5 个 Chrome 扩展来加速你的开发

### 5 个有用的 Chrome 扩展，帮助开发者提高工作效率，完成更多工作。

javascript.plainenglish.io](/5-chrome-extensions-to-speed-up-your-development-70350aaf2e3) [](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) [## 作为一名开发人员，我在构建投资组合时学到了什么

### 你也可以从中学习。

javascript.plainenglish.io](/what-i-learned-while-building-my-portfolio-as-a-developer-26a20873517b) 

*更多内容尽在*[***plain English . io***](http://plainenglish.io)