# 21 个对日常开发有用的 JavaScript 代码片段

> 原文：<https://javascript.plainenglish.io/21-useful-javascript-snippets-for-everyday-development-9e66e33bfb86?source=collection_archive---------4----------------------->

## 有用且省时的小 JavaScript 代码片段

![](img/632bd60a7c275fb91fc9ebd646614385.png)

Photo by [Evelyn Clement](https://unsplash.com/@e_clement?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

下面是一些有用的 JavaScript 代码片段，任何前端/web 开发人员都可以添加到他们的应用程序中，并在日常开发中使用。

许多代码片段都是一行程序，易于理解，可以添加到任何 web 开发前端项目中。

由于 JavaScript 一直在变化，所以创建可重用的方法很重要，这样如果有什么变化，你只需要在一个地方改变它。希望下面的列表中至少有一个可以帮助你创建一些你自己的可重用方法！

## 1.以数字形式获取输入值

```
const checkMyValueType = (event) => {
  console.log(typeof event.target.value) // string
  console.log(typeof event.target.**valueAsNumber**) // number
}<input type="number" onkeyup="checkMyValueType(event)" />
```

## 2.将输入复制到剪贴板

```
function copyToClipboard(inputID){
navigator.clipboard.writeText(document.querySelector(inputID).value);
}
```

***注意:并非每个浏览器都支持导航器(一定要检查 IE)***

## 3.检查选项卡浏览器选项卡是否在视图中

```
const isBrowserTabInView = () => document.hidden;isBrowserTabInView(); // returns true or false depending if tab is in view / focus
```

## 4.将布尔值更改为相反的值

```
let myBool = false;myBool = !myBool;
console.log(myBool); // truemyBool = !myBool;
console.log(myBool); // false
```

## 5.检查给定的数字是否是偶数

```
const isEven = num => num % 2 === 0;console.log(isEven(2)) // true
console.log(isEven(3)) // false
```

## 6.检查日期是否是工作日

```
const isWeekday = d => d.getDay() % 6 !== 0;console.log(isWeekday(new Date(2021, 0, 11))); // true (Monday)
console.log(isWeekday(new Date(2021, 0, 10))); // false (Sunday)
```

## 7.向日期添加天数

```
const addDaysToDate = (date, n) => {
  date.setDate(date.getDate() + n);
  return date.toISOString().split('T')[0];
};addDaysToDate('2021-0-10', 10); // "2021-01-20"
addDaysToDate('2021-0-10', -10); // '2020-12-31'
```

## 8.从日期中获取时间

```
const timeFromDate = date => date.toTimeString().slice(0, 8);console.log(timeFromDate(new Date(2021, 0, 10, 17, 30, 0))); 
// "17:30:00"
console.log(timeFromDate(new Date(2021, 0, 10, 5, 56, 44)));
// "05:56:44"
```

## 9.计算两个日期之间的周数

```
const countWeekDaysBetween = (startDate, endDate) =>
  Array
    .from({ length: (endDate - startDate) / (1000 * 3600 * 24) })
    .reduce(count => {
      if (startDate.getDay() % 6 !== 0) {
        count++;
      }
     startDate = new Date(startDate.setDate(startDate.getDate() + 1));
      return count;
    }, 0);countWeekDaysBetween(new Date(2021, 0, 10), new Date(2021, 0, 20)); // 7
countWeekDaysBetween(new Date(2021, 1, 10), new Date(2021, 2, 18)); // 26
```

## 10.检查本地存储是否已启用

```
const isLocalStorageEnabled = () => {
  try {
    const key = `__storage__test`;
    window.localStorage.setItem(key, null);
    window.localStorage.removeItem(key);
    return true;
  } catch (e) {
    return false;
  }
};isLocalStorageEnabled(); *// true, if localStorage is accessible*
```

## 11.检查某事花了多长时间

```
var startTime = performance.now();
anyMethodOrCode();
const endTime = performance.now();console.log(endTime - startTime + " milliseconds."); // (Time in milliseconds)
```

## 12.捕捉右键点击

```
window.oncontextmenu = () => {
  console.log('right click');
}
```

## 13.仅触发一次事件侦听器

```
const myButton = document.getElementById("myBtn");const myClickFunction = () => {
  console.log('this click will only get called once')
}myButton.addEventListener('click', myClickHandler, {
  once: true,
});
```

## 14.滚动到页面顶部

```
const scrollToTopOfDocument = () => {
  const c = document.documentElement.scrollTop || document.body.scrollTop;
  if (c > 0) {
    window.requestAnimationFrame(scrollToTop);
    window.scrollTo(0, c - c / 8);
  }
};scrollToTopOfDocument();
```

## 15.检查字符串是否大写

```
const isUpperCase = str => str === str.toUpperCase();console.log(isUpperCase("string")); // false
console.log(isUpperCase("STRING")); // true
console.log(isUpperCase("5TR1NG")); // true
```

## 16.检查给定元素是否在焦点上

```
const elementIsInFocus = el => (el === document.activeElement);elementIsInFocus(anyElement)// returns true if in focus, false if not in focus
```

## 17.查找数组之间的差异

```
const differenceInArrays = (array1, array2) =>  {  
    const set = new Set(array2);  
    return array1.filter(x => !set.has(x));
}; differenceInArrays(["apple", "orange", "banana"], ["apple", "orange", "mango"]); // ["banana"]differenceInArrays([10, 12, 5], [66, 10, 6]); // [12, 5]
```

## 18.从元素中移除事件侦听器

```
const removeEventOffElement = (el, evt, fn, opts = false) => el.removeEventListener(evt, fn, opts);const testFunction = () => console.log('My function has been called');
document.body.addEventListener('click', testFunction);// Call remove method
removeEventOffElement(document.body, 'click', fn); 
```

## 19.以十六进制格式生成随机颜色

```
const generateRandomColour = () =>   "#" + Math.floor(Math.random()*16777215).toString(16);//EXAMPLE
document.getElementsByTagName("body")[0].style.color = generateRandomColour();
```

## 20.查找第一个定义的非空参数

```
const getFirstValidValue = (...values) => values.find(v => ![undefined, null].includes(v));console.log(getFirstValidValue(null, undefined, 'Hey', null); // 'Hey'
```

## 21.侦听指定元素之外的点击

```
const onClickOutsideElement = (element, callback) => {
  document.addEventListener('click', e => {
    if (!element.contains(e.target)) callback();
  });
};onClickOutside('#some-element', () => console.log('Hey you missed'));
// Will log "Hey you missed" everytime a click that was not "some-element" was clicked
```

# 结论

有时使用 JavaScript，开发人员会发现自己一遍又一遍地创建相同的东西，希望上面的一些片段可以在您的应用程序中重用。

跟上新的 JavaScript 特性和浏览器 API 非常重要。许多开发人员有时会创建过于复杂的方法，因为他们不知道从浏览器/ JavaScript 中可以免费获得什么。

希望你喜欢阅读！