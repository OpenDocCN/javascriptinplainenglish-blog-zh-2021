# JavaScript 中的振动 API

> 原文：<https://javascript.plainenglish.io/the-vibration-api-in-javascript-64cda2a919a6?source=collection_archive---------15----------------------->

![](img/b5e5edcff3594640da73ae2cce880b93.png)

Photo by [Sebastian Bednarek](https://unsplash.com/@abeso?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

振动是为用户的任何动作提供物理反馈的最佳方式，主要针对移动用户。例如，在显示警告消息或警报时，在接收消息或通知时等。

振动 API 允许 web 应用程序访问设备的振动硬件(如果存在)来产生振动。出于同样的目的，它提供了一个名为`navigator.vibrate()`的方法。

# navigator.vibrate()方法

该方法以毫秒为单位获取振动持续时间值，并使设备振动该时间。

```
navigator.vibrate(500); 
// device will vibrate for 500ms
```

少数浏览器不支持震动 API，如 IE、Opera、Safari 等。，所以在使用之前最好先检查一下浏览器的支持。

```
if (navigator.vibrate) {
   navigator.vibrate(500);
}
```

# 以一种模式振动

`vibrate()`方法也可以接受一组值作为参数。我们可以提供不同的值来表示它振动的时间和不振动的时间。对于偶数索引处的值，它将振动，对于奇数索引处的值，它将暂停。

```
navigator.vibrate([320, 200, 320, 1000, 320, 200, 320]);
```

这里，它将首先振动 320 毫秒并暂停 200 毫秒，然后再次振动 320 毫秒并暂停 1000 毫秒，以此类推。

要取消正在运行的振动，我们可以通过传递 0 或空数组作为参数来调用`vibrate()`方法。

```
navigator.vibrate(0);
// OR
navigator.vibrate([]);
```

尝试这些强大的代码，并查看它们的运行情况(在移动设备上尝试)。

# 你可能也喜欢

*   [JavaScript 获取 API 进行 HTTP 请求](https://jscurious.com/javascript-fetch-api-to-make-http-requests/)
*   [JavaScript 设置对象存储唯一值](https://jscurious.com/javascript-set-object-to-store-unique-values/)
*   [JavaScript 中的生成器函数](https://jscurious.com/generator-functions-in-javascript/)
*   [JavaScript getter 和 setter](https://jscurious.com/javascript-getters-and-setters/)
*   [20+ JavaScript 速记编码技巧](https://jscurious.com/20-javascript-shorthand-techniques-that-will-save-your-time/)

*感谢您的宝贵时间:)*
***阿米塔夫·米什拉***

*更多内容请看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***