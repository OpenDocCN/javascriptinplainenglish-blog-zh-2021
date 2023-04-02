# 3 单行 JavaScript 字符串操作算法

> 原文：<https://javascript.plainenglish.io/3-one-liner-javascript-string-manipulation-algorithms-2005c9f4cb0a?source=collection_archive---------15----------------------->

## 有和没有 Regex

![](img/a19b95ca4b63edd787a202e6311548d6.png)

Photo by [Brett Jordan](https://unsplash.com/@brett_jordan?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

让我们操纵绳子，“我在公园遛狗。”

# 1.将空格转换为下划线

## **带 Regex**

算法:`a.replace(/ /g, ‘_’)`

示例:

```
const a = "I walked my dog at the park";const b = a.replace(/ /g, '_');console.log(b);
```

输出:`I_walked_my_dog_at_the_park`

## **无 Regex**

算法:`a.split(‘ ‘).join(‘_’)`

示例:

```
const a = "I walked my dog at the park";const b = a.split(' ').join('_');console.log(b);
```

输出:`I_walked_my_dog_at_the_park`

# 2.将每个单词大写

## 与 Regex

算法:`a.replace(/(?: |*\b*)(\w)/g, (key) => key.toUpperCase())`

示例:

```
const a = "I walked my dog at the park";const b = a.replace(/(?: |*\b*)(\w)/g, (key) => key.toUpperCase());console.log(b);
```

输出:`I Walked My Dog At The Park`

## 没有 Regex

算法:`a.split(“ “).map((word) => word[0].toUpperCase() + word.substring(1)).join(“ “)`

示例:

```
const a = "I walked my dog at the park";const b = a.split(" ").map((word) => word[0].toUpperCase() + word.substring(1)).join(" ");console.log(b);
```

输出:`I Walked My Dog At The Park`

# 3.反向单词

## 与 Regex

在**批注中告知💬**如果你知道一个单行的 JavaScript Regex 算法来反转字符串中的单词！

## 没有 Regex

算法:`a.split(“ “).reverse().join(“ “)`

示例:

```
const a = "I walked my dog at the park";const b = a.split(" ").reverse().join(" ");console.log(b);
```

输出:`park the at dog my walked I`

谢谢你的阅读！在 Medium 上跟我来( [Charlie Levine](https://medium.com/u/6da6b651e31a?source=post_page-----2005c9f4cb0a--------------------------------) )获取每周编程和技术文章。

**如果您喜欢，您也可以:**

[](/3-fundamental-concepts-to-master-any-frontend-framework-7d38bdb6b48) [## 掌握任何前端框架的 3 个基本概念

### Angular，React，Vue，Svelte，以及许多未来的框架。

javascript.plainenglish.io](/3-fundamental-concepts-to-master-any-frontend-framework-7d38bdb6b48) [](/the-ultimate-guide-to-creating-auto-saving-forms-in-angular-29806875364) [## 创建角度自动保存表格的最终指南

### 由 RxJS 和角度材料供电

javascript.plainenglish.io](/the-ultimate-guide-to-creating-auto-saving-forms-in-angular-29806875364) [](/the-ultimate-guide-to-infinite-scrolling-in-angular-11-36d3bbce9fff) [## 角度 11 无限滚动的终极指南

### 由 Open Brewery DB、NGX-Infinite-Scroll 和角形材料提供动力

javascript.plainenglish.io](/the-ultimate-guide-to-infinite-scrolling-in-angular-11-36d3bbce9fff)