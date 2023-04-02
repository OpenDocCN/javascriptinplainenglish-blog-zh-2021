# 3 个代码块帮助您更好地理解“var”、“let”和“const”

> 原文：<https://javascript.plainenglish.io/3-code-chunks-to-help-you-understand-var-let-const-better-bb34e898cd4d?source=collection_archive---------19----------------------->

## 这就是为什么你在 2021 年没有用 var 声明 JavaScript 变量。

![](img/c43a82fd9a768c05b5d0182dd12be3c8.png)

Photo by [Joshua Aragon](https://unsplash.com/@goshua13?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 无处不在。人们正在用 JavaScript 做着令人惊叹的事情，它可能运行在你的手机、浏览器甚至服务器上。

这里列出了一些代码块来帮助你理解`let`、`var`和`const`，以及为什么你不应该用`var`来声明 JavaScript 变量。

```
Before 2015, using the var keyword was the only way to **declare** a JavaScrip**t variable**.
```

```
**// let**
for (let i = 0; i < 5; i++) {
  // i accessible ✔️
}
// i not accessible ❌**// const**for (const i = 0; i < 5; i++) {
  // i is not changeable as its constant ❌
}
// i not accessible ❌**// Var**for (var i = 0; i < 5; i++) {
  // i accessible ✔️
}
// i accessible ✔️
```

```
 ** **var** is **Function** Scoped but **let/const** is block **scoped **** // i IS NOT known here
// j IS NOT known here
// k IS known here, but undefined
// l IS NOT known here

function loop(arr) {
    // i IS known here, but undefined
    // j IS NOT known here
    // k IS known here, but has a value only the second time loop is called
    // l IS NOT known here

    for( var i = 0; i < arr.length; i++ ) {
        // i IS known here, and has a value
        // j IS NOT known here
        // k IS known here, but has a value only the second time loop is called
        // l IS NOT known here
    };

    // i IS known here, and has a value
    // j IS NOT known here
    // k IS known here, but has a value only the second time loop is called
    // l IS NOT known here

    for( let j = 0; j < arr.length; j++ ) {
        // i IS known here, and has a value
        // j IS known here, and has a value
        // k IS known here, but has a value only the second time loop is called
        // l IS NOT known here
    };

    // i IS known here, and has a value
    // j IS NOT known here
    // k IS known here, but has a value only the second time loop is called
    // l IS NOT known here
}

loop([1,2,3,4]);

for( var k = 0; k < arr.length; k++ ) {
    // i IS NOT known here
    // j IS NOT known here
    // k IS known here, and has a value
    // l IS NOT known here
};

for( let l = 0; l < arr.length; l++ ) {
    // i IS NOT known here
    // j IS NOT known here
    // k IS known here, and has a value
    // l IS known here, and has a value
};

loop([1,2,3,4]);

// i IS NOT known here
// j IS NOT known here
// k IS known here, and has a value
// l IS NOT known here
```

```
// **var** is global scope (hoist-able) variable but **let/const** is not !{
    let l = 'let';
    const c = 'const';
    var v = 'var';
    v2 = 'var 2';
}

console.log(v, this.v);
console.log(v2, this.v2);
console.log(l); // ReferenceError: l is not defined
console.log(c); // ReferenceError: c is not defined
```

注:本文写作灵感来自[这个](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var)堆栈溢出线程。

感谢您的阅读和快乐的 Java 编写。

*更多内容看* [***说白了就是***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***