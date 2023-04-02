# 2022 年的 22+高频 JavaScript 代码片段

> 原文：<https://javascript.plainenglish.io/17-high-frequency-javascript-code-chunks-for-2022-6e9258e28b00?source=collection_archive---------13----------------------->

## JavaScript 开发人员熟知的代码片段。

![](img/eedc5dcfa24cc5d9c06a57036d6f9694.png)

Photo by [Greg Rakozy](https://unsplash.com/@grakozy?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

JavaScript 的故事很长。今天，JavaScript 运行在从手机到服务器的所有设备上。无论你是计划在 2022 年使用 JavaScript 开发，还是已经在编写 JS，这里有一些你可能会用到的有用的代码片段。

## 1.短路表达式

```
const defaultSafeValue = "defaultSafeValue"
let someValueNotSureOfItsExistence = nulllet expectingSomeValue = someValueNotSureOfItsExistence || defaultSafeValueconsole.log(expectingSomeValue)
```

如果`someValueNotSureOfItsExistance`是`undefined` / `null` / `false`，那么`defaultSafeValue`就会到位。如果我们不确定是否存在任何价值，这是很方便的。这也确保了你不会从错误的物体上看到任何东西，例如，像下面这样的东西。

```
let someValueNotSureOfItsExistence = null// let someValueNotSureOfItsExistence = { expectingSomeValue:1 }let { expectingSomeValue } = someValueNotSureOfItsExistence ||  {}console.log(expectingSomeValue)
```

> 你可以在上面的代码中取消类似的注释，这样可以避免崩溃。

## 2.如果存在

```
let someValue = true // or some value like 1,.. {} etcif(someValue){
   console.log('Yes. Its exist')
}
```

## 3.多重条件

```
const conditions = ["Condition 2","Condition String2"];someFunction(str){
  if(str.includes("someValue1") || str.includes("someValue2")){
    return true
  }else{
    return false
  }
}
```

同样可以通过下面的

```
someFunction(str){
   const conditions = ["someValue1","someValue2"];
   return conditions.some(condition=>str.includes(condition));
}
```

## 4.模板文字

```
let name = "John Doe", profession = "Engineering"let someSentence = `My Name is ${name} and he is doing ${profession}`console.log(someSentence)// His Name is John Doe and he is doing Engineering
```

## 5.析构赋值

```
let personObject = {
  name:"John Doe",
  phone:"1234",
  address:{
    line:"abc ave",
    postCode:12223,
  },
}
const {name, phone, address} = personObject;
```

我们经常在 React 这样的框架中这样做，如下所示

`import { observable, action, runInAction } from 'mobx';`

## 6.扩展运算符

```
const previousNumber = [1, 3, 5 ];
const allNumbers = [2 ,4 , 6, ...previousNumber];
console.log(allNumbers);// [ 2, 4, 6, 1, 3, 5 ]//Handy if you want to merge two objects
```

## 7.箭头功能短指针

```
var sayHello = (name)=>{
   return "Hello " + name
}
console.log(sayHello("John"))
```

代替

```
var sayHello = (name)=> "Hello " + name
console.log(sayHello("John"))
```

## 8.数组最大/最小元素

```
const numbers = [1, 2 ,-3, 4, 5]
console.log(Math.min(...numbers)) // Output: -3
console.log(Math.max(...numbers)) // Output: 5
```

## 9.单线阵列反转

```
const numbers = ['3', '2', '1']
console.log(numbers.reverse())   // output: [ "1", "2", "3" ]
```

## 10.移除`duplicates from array`

```
**const** arr = ['1', '1', '2', '1']
**const** filteredArr = [...new Set(arr)]
console.log(filteredArr) *// output: ['1', '2']*
```

## 11.条件函数调用

```
function fn1(){
  console.log('I am Function 1');
}function fn2(){
  console.log('I am Function 2');
}let checkValue = 3;if(checkValue === 3){
 fn1();
}else{
 fn2();
}
```

相反，简言之

`(checkValue ===3 ? fn1:fn2)(); // Short Version`

## 12.&&运算符

```
var value = true; // or true or some value exist
if(value){
  console.log('Value is there or true')
}// OR via this way
value && console.log('Value is there or true')
```

## 13.将字符串转换为数字

```
const numberStr1 = "100";
const numberStr2 = "200";var sampleValue = +numberStr1 + +numberStr2;
console.log(sampleValue);console.log(typeof sampleValue); // Its a number!
```

## 14.避免过多的函数参数

```
function myFunction(employeeName,jobTitle,yrExp,majorExp){}// you can call it viamyFunction("John","Project Manager",12,"Project Management");//    ***** PROBLEMS ARE *****
// Violation of ‘clean code’ principle
// Parameter sequencing is important
// Unused Params warning if not used 
// Testing need to consider a lot of edge cases.
```

相反，创建一个 params 对象，如

`const mockTechPeople = {
employeeName:'John',
jobTitle:'Project Manager',
yrExp:12,
majorExp:'Project Management'
}`

并且**析构**函数中的 params 使得它更加干净，不太可能产生 bug。

```
function myFunction({employeeName,jobTitle,yrExp,majorExp}){

     // ES2015/ES6 **destructuring** syntax is in action
     // map your desired value to variable you need.
}
```

现在打电话很简单

```
myFunction(mockTechPeople); // Only One argument
```

## 15.默认参数值

```
function rectangle(h,w){
 if(!h){
   h=0;
 }else if(!w){
  w=0;
 }
 return h*w;
}
console.log(rectangle())
```

代替

```
function rectangle(h =0,w=0){
  return h*w;
}
console.log(rectangle(1,12))
```

## 16.数学。地板短手

```
var val = "1212121212"console.log(Math.floor(val)) // Long one
console.log(~~val) // smart one
```

## 17.toString 短指针

```
var someNumber = 123
console.log(someNumber.toString()) //return "123"// Or in SHORT CUT
console.log(`${someNumber}`) //return "123"
```

## 18.循环冷却

```
for(let i=0;i<1e3;i++){ // instead of i<1000, Cool, right?   
}
```

## 19.值到对象的映射，即键和值相同

```
var x='x',y='y'
var obj = {x,y} // instead of {x:x, y:y}
console.log(obj)
```

## 20.多行字符串

```
var multiLineString = `some string\n
with multi-line of\n
characters\n`console.log(multiLineString)
```

## 21.吸气方法

```
const obj = {
   firstName:"John",
   lastName:"Snow",
   get fullName(){
    return `${this.firstName} ${this.lastName}`;
   }}console.log(obj.fullName) // John Snow
```

## 22.轻松合并两个数组

```
const fruits= ["Mango", "Pineapple" , "Orange", "Lemon", "Apple"];
const someMoreFruits= ["Banana", "JackFruit"];
const myFruitBasket = [...fruits,...someMoreFruits]// myFruitBasket =  ['Mango', 'Pineapple', 'Orange', 'Lemon', 'Apple', 'Banana', 'JackFruit']
```

## 23.唯一值，设置操作

```
let animals = [
  {
    name:'Lion',
    category: 'carnivore'
  },
  {
    name:'dog',
    category:'pet'
  },
  {
    name:'cat',
    category:'pet'
  },
  {
    name:'wolf',
    category:'carnivore'
  }
]let category = animals.map((animal)=>animal.category);
console.log(category); //["carnivore" , "pet" , "pet" , "carnivore"]// Duplicate Values !!
```

下面是获得唯一值的方法

```
//wrap your iteration in the set method like thislet category = [...new Set(animals.map((animal)=>animal.category))];console.log(category);////["carnivore" , "pet"]
```

## 24.动态复杂的键值对

```
let category = 'carnivore';
let lion = {
  'lion-baby' : "cub",
  [category] : true,
};console.log(lion.lion-baby);
// cause a boom !
// Uncaught ReferenceError: baby is not defined
```

简单的处理方法是把它放在`[]`中，也就是说`console.log(lion[‘lion-baby’])`，这让编译器很高兴😊。

这里有一些有趣的事情你也可以做。

```
const number = 5;
const gavebirth = true;let animal = {
  name: 'lion',
  age: 6,
  [gavebirth && 'babies']: number
};console.log(animal); // { name: "lion" , age: 6 , babies: 5 }// Cool thing right
// [https://www.freecodecamp.org/news/top-javascript-concepts-to-know-before-learning-react/](https://www.freecodecamp.org/news/top-javascript-concepts-to-know-before-learning-react/)
```

厌倦了看一些严肃的东西？阅读[本](/30-funny-code-comments-that-will-make-you-laugh-1c1b54d4ab00)进行思维更新。

感谢阅读。祝 Java 编写愉快。🍻

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯点击这里***](http://newsletter.plainenglish.io/) ***。***