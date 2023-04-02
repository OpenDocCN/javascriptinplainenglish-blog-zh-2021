# 如何使用地理定位 API 获取用户的当前位置

> 原文：<https://javascript.plainenglish.io/geolocation-api-d62df2b374ca?source=collection_archive---------9----------------------->

为了给网站的访问者提供更好的用户体验，有时你需要知道他们的位置。

在本文中，我将向您展示如何确定用户的地理坐标(经度和纬度)。为此，我使用了地理定位 API。

![](img/eff9d40b9d554d902da0bd53ad69ef2c.png)

> 此功能仅在部分或所有受支持的浏览器中的安全上下文(HTTPS)中可用。

# 安全性

地理定位 API 通过请求许可来报告位置信息来保护用户的隐私。因此，用户的操作系统会在第一次请求时弹出一个对话框，要求用户允许共享位置信息。用户可以接受或拒绝请求。

# **怎么用？**

从一个简单的 HTML div 容器开始，显示坐标的结果。以及一个带有事件处理程序 onclick 的按钮，它触发一个函数来获取这些坐标。

```
<button onclick='getLocation()'> Get my current location </button>
<div id = "location"></div><script>
   let current_location = document.getElementById("location");
</script>
```

现在，我们需要调用全局“navigator”对象。它返回一个地理位置对象，该对象提供对设备位置的访问。

> 如果 navigation.geolocation 的类型== undefined，这意味着您的浏览器不支持此功能。

```
if(navigator.geolocation){ //do something } 
else { //browser does not support this feature }
```

为了访问设备的当前位置，我们需要使用返回地理位置对象的`getCurrentPosition method()`。它需要 1 个**必需的**参数(成功)和一个可选的(错误)参数来处理提供用户位置数据的两种许可可能性:授权或拒绝。

```
const getLocation = () => {
  if(navigator.geolocation)
    navigator.geolocation.getCurrentPosition(success, error);
  else 
    current_location.textContent = `Your browser does not support this feature`;
}
```

**成功:**一个回调函数。它接受一个参数 *GeolocationPosition* 对象。

```
const success = (position) => {
  const longitude = position.coords.longitude;
  const latitude = position.coords.latitude;

  current_location.textContent = `Longitude = ${longitude} \n latitude = ${latitude}`;
}
```

**错误:一个**回调函数。它采用一个参数*GeolocationPositionError*对象，该对象表示使用地理定位设备时出错的原因。

> geolocationpositionerror . message 返回人类可读的错误消息。

```
const error = (error) => {
  current_location.textContent = `Couldn't access your location \n Reason: ${error.message}`;
}
```

# 决赛成绩

```
<button onclick = "getLocation()">Get my current location</button>
<div id = "location"></div><script>let current_location = document.getElementById("location");const success = (position) => {
  const longitude = position.coords.longitude;
  const latitude = position.coords.latitude;

  current_location.textContent = `Longitute = ${longitude} \n latitude = ${latitude}`;
}const error = (error) => {
  current_location.textContent = `Couldn't access your location \n Reason: ${PositionError.message}`;
}const getLocation = () => {
  if(navigator.geolocation)
    navigator.geolocation.getCurrentPosition(success,error);
  else 
    current_location.textContent = `Your browser does not support this feature`;
}</script>
```

你觉得我还有什么要补充的吗？欢迎评论或写回复！

***随时通过*** [***在 LinkedIn 上关注我***](https://www.linkedin.com/in/hiba-abdel-karim/) ***了解我更多信息。***

*更多内容请看*[*plain English . io*](http://plainenglish.io/)