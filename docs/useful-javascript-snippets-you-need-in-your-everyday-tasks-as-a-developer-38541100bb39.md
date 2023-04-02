# 开发人员日常工作中需要的有用的 JavaScript 代码片段

> 原文：<https://javascript.plainenglish.io/useful-javascript-snippets-you-need-in-your-everyday-tasks-as-a-developer-38541100bb39?source=collection_archive---------14----------------------->

## 有用的 JavaScript 代码片段。

![](img/0277de294ff81c601a84664d86e027dc.png)

By FAM

作为一名前端开发人员，JavaScript 是这个世界上的必备知识。这篇文章将会给你一个有用的代码片段列表，这些代码片段是我保存并在编码时使用的。

这些片段有助于我在编写 JavaScript 代码时面临的最常见的任务。如果你有其他有用的片段，请在评论区告诉我。

我们走吧！

# 1.对数组排序

```
const months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]const numbers= [1, 30, 4, 21, 100000];
numbers.sort((a,b)=> {return a-b});
console.log(numbers);
// expected output: Array [1, 4, 21, 30, 100000]
```

# 2.过滤数组

```
const words = ['spray', 'limit', 'elite', 'exuberant', 'destruction', 'present'];const result = words.filter(word => word.length > 6);console.log(result);
// expected output: Array ["exuberant", "destruction", "present"]
```

# 3.遍历一个数组

```
let cars = ["Ford", "Ferrari", "BMW"];for(let car of cars){
console.log(car);
}// Ford
// Ferrari
// BMW 
```

# 4.选择随机元素

```
let items = ["Facebook", "Youtube", "Instagram", "Twitter"];let index = Math.floor(Math.random() * items.length );
console.log(items[index]);
```

# 5.检查一个元素是否有 CSS 类

```
const element = document.querySelector("#elt");
const isActive = element.classList.contains("active");
console.log(isActive);// Returns true or false
```

# 6.字符串插值

```
let name = "Front";console.log(`Hello, so happy to see you in our ${name} blog!`);
// Hello, so happy to see you in our Front blog!
```

# 7.在字符串中替换

```
let str = "My awesome string!";
let txt = str.replace("string", "text");console.log(txt);// My awesome text!
```

# 8.获取当前时间

```
let d = new date();
let now = `${d.getHours()}:${d.getMinutes()}:${d.getSeconds()}`;console.log(now);// 11:04:21
```

# 9.反转一根绳子

```
function reverse(str){
  return str.split("").reverse().join("");
}const reversed = reverse("FRONT");
console.log(reversed);//TNORF
```

# 亲爱的读者，我希望这是清晰和有用的

无论你在哪里，我都希望你和你的家人平安！坚持住。明天会更好！

**联系一下** [**中**](https://medium.com/@famzil/)**[**Linkedin**](https://www.linkedin.com/in/fatima-amzil-9031ba95/)**[**脸书**](https://www.facebook.com/The-Front-End-World)**[**insta gram**](https://www.instagram.com/the_frontend_world/)**，或者**[**Twitter**](https://twitter.com/FatimaAMZIL9)**。********

 ****[## 前面

### 欢迎来到❤家庭前线

www.fam-front.com](http://www.fam-front.com/)**** 

******FAM******

*****更多内容请看*[*plain English . io*](http://plainenglish.io/)****