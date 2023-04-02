# 如何解决常见的 JavaScript 编码挑战

> 原文：<https://javascript.plainenglish.io/javascript-stringing-along-and-some-easy-coding-challenges-to-practise-ea3f028299a4?source=collection_archive---------10----------------------->

## *您可以使用的常见字符串函数，以及在 JavaScript 中涉及字符串操作的编码挑战*

![](img/19c02d2c8510fa63a994cb66bea30cfb.png)

**有时你只想要一个角色。是的，你喜欢保持简单。**从指定索引处的字符串中获取单个字符:

***charAt(索引)***

```
function **getInitials** (firstName, lastName) { return firstName.**charAt**(0) + lastName.**charAt**(0);}*// Example: getInitials('Charles', 'Boyle') should return 'CB'.*
```

**用更多的琴弦连接琴弦**。

*   **`$ { string go } $ { string two }**
*   **concat(分离器)；**

```
const first_name = ‘Joe’;const last_name = ‘Booboo’;const fullName = first_name.**concat**(‘ ‘, last_name);const fullNameV2 = first_name + “ “ + last_name;  // nobody likes this way anymore, people will judge youconst fullNameV3 = `${first_name} ${last_name}`; // the new cool way
```

对于所有敏感人群，尤其是区分大小写:**我们可以使用大写或小写字符串:**

*   **to ppercase()；**
*   **tolower case()；**

```
const string = ‘dont shout at me’;const uppercase = string.**toUpperCase**();const string2 = ‘OK IM SORRY’;const lowercase = string2.**toLowerCase**();
```

**在找什么？询问 indexOf，它会告诉您它在字符串中找到的索引或位置。如果它找不到它，它将返回-1。**

*   **。**的索引(searchString，其中 indexto startlookingat**)**
*   返回找到的索引或-1

```
const string = “I love cats.”;const searchFor = “cats”;const result = string.indexOf(searchFor); // Result is 7 (YES WE FOUND IT!!!) 
```

**你想要一根绳子吗？** AKA 子串？这个非常直观，它叫做 substr()

*   **。子字符串** (startIndex，endIndex)
*   第一个参数指定开始提取的位置。
*   第二个参数指定要提取的字符数。
*   如果未设置第二个参数，则从字符串的开始位置到结束位置的所有字符都将被提取。

```
function **getUsernameFromEmail** (string) { const indexOfSymbol = string.**indexOf**(‘@’); return string.**substr**(0, indexOfSymbol);}**getUsernameFromEmail**(‘jumanah@gmail.com’) *// output: jumanah*
```

**需要用别的东西替换你绳子上的坏东西..你明白了…替换()**

*   **代替()**
*   第一个参数是要替换的内容
*   第二个参数是替换文本

*仅替换第一个匹配项..需要多次链接，尽管有 replaceAll(需要更新本文)

```
function **formatDate**(date) { let newDate = date.**replace**(‘-’, ‘/’).**replace**(‘-’, ‘/’); return newDate;}*// Example:* **formatDate***('20-05-2017') will return '20/05/2017'.*
```

你有强迫症吗？**你讨厌文本周围的多余空间吗？不要再说了，将它们连同装饰一起移除()；**

*   **修剪()；**
*   删除字符串周围的空白，而不是其中的空白

```
const searchString = ‘animals in australia  ‘function **searchName**(name) { name.**trim**(); // output: 'animals in australia' *// .. GET request or somethang*}**searchName(**searchString); 
```

**将字符串转换为数组**。如果您想对字符串中的每个字母重复某个操作，您可能需要这样做。

*   **。拆分(“分隔符”)；**
*   **[…弦]**
*   **array . from()；**

```
const sentence = ‘i was not stringing him along’;
const string = ‘word’; *// Option 1: Using Split(), provide the seperator as an argument, here we can use space* var array = sentence.**split**(‘ ’); *// output: [‘i’, ‘was’, ‘not’, ‘stringing’, 'him', 'along'];* *// Option 2: Using ... spread syntax* var array = […string]; *// output: [‘w’, ‘o’, ‘r’, ‘d’]**// Option 3: Using Array.from* var array = **Array**.**from**(string); *// output: [‘w’, ‘o’, ‘r’, ‘d’]*
```

**将数组转换为字符串！**你可能想用一个数组组成一个句子，或者将字符串连接到一个数组中

*   **连接(‘分离器’)；**

```
const newStringFromArray = [‘Twas’, ‘the’, ‘night’, ‘before’, ‘Christmas’].**join**(‘ ‘);*// output: ’Twas the night before Christmas’*const newStringUrlFromArray = [‘masteringjs.io’, ‘tutorials’, ‘fundamentals’, ‘string-concat’].**join**(‘/’);*// output: ‘masteringjs.io/tutorials/fundamentals/string-concat’*
```

你喜欢颠倒的东西，还是相反的东西？:D

请继续关注下面的编码挑战！

# **【EASY】编码挑战，字符串操作#1:反转字符串**

所以要反转一个字符串，我们要讨论字符串中的所有字符，可能是一个单词，也可能是一个完整的句子。我马上想到了一些主意…

*   想法一:如果我们做一个从字符串末尾到开头的循环会怎么样？！
*   **想法二:**如果我们以前用 **reverse()** …但是它只对数组有效呢..嗯..我们如何才能做到这一点。

好的..让我们发展这些想法

**创意 1:反向循环**

复杂度:o(n)我们对字符串中的每一项循环一次

```
**function reverseString(str) {** let output = '';
  // loop from the very last element in the array all the way to 0 (the first element)   for (let i = str.length-1; i >= 0; i--) { // add letters from the back of the string to the start of this new string output += str[i];   // p, po, poo, pool } return output;**}****reverseString('loop'); // output: pool**
```

想法二:**内置方法，reverse()**

*   首先，我们需要将整个字符串转换成一个单独字符的数组，以利用 reverse()；反转数组的函数！
*   然后我们把数组转换回字符串！简单的柠檬挤在一条线上。

```
**function reverseString(str) {***// convert to an array, reverse the array and then join* **return str.split("").reverse().join("");**}**reverseString**("love"); // 'evol'  YUP JUST LIKE EMINEM SAID!!!
```

# [简单]编码挑战，字符串操作#2: Pangram

*   盘符是一个包含字母表中所有 26 个字母的句子
*   给定一个字符串输入，找出该字符串是否是一个盘符，并返回 true 或 false

```
function isPangram(str) {}
```

好吧，让我们一起**想想这个:**

*   可以使用正则表达式来检测一个字符是否属于一个字母表，或者你可以自己定义字母表(不需要)
*   显然，句子需要至少 26 个字符才能满足这个要求

那么我们的**伪码**是什么呢..还是我们的策略？我们可以把它写在代码的注释中

*   我们可以使用一个集合或一个散列来存储我们遇到的所有独特的字母。如果这是一个七巧板，应该有 26 个字母
*   定义一个正则表达式来查找字母字符
*   将字符串转换成小写，这样我们就不会有大小写问题了
*   如果字符串小于 26 个字符，就不用循环了
*   遍历字符串中的所有字符，检查它是否是字母表的一部分
*   使用我们的正则表达式，如果字符在字母表中，我们将它添加到我们的集合中(我们的集合将忽略重复的)
*   如果我们的集合的大小或长度为 26(与字母表相同)，这意味着我们返回 true，否则，我们返回 false。

**解决方案 1:使用集合和正则表达式**

```
function **isPangram**(string) { // Convert to lowercase
 string = string.**toLowerCase**(); *// Define our set which will store the alphabet* let uniqueLetters = new **Set**(); *// Define our regex to test for alpha characters* const regex = /[a-z]g/; *// Short circuit - not enough characters* if (string.length < 26) { return false; } *// Loop through all characters in the string to check if it is part of the alphabet* for (let i = 0; i < string.length; i++) { *// using our regex, if character is in the alphabet, we add it to our set (our set will ignore duplicates)* if (regex.**test**(string[i])) { uniqueLetters.**add**(string[i]); *// store it in our set* } }*// if our set has a size or length of 26 (same as the alphabet) it means we return true, otherwise, we return false.* return uniqueLetters.size === 26;}console.**log**(**isPangram**('Bawds jog, flick quartz, vex nymphs.')); *// true*console.**log**(**isPangram**('Bawds jog, flick quartz, vex nymphs.')); *// true*console.**log**(**isPangram**('Roses are red, violets are blue, sugar is sweet, and so are you.')); *// false*
```

我们可以在这个**替代**方法中使用散列，而不是在这里使用集合:

**解决方案 2:使用散列和正则表达式**

```
function **isPangram**(string) { let counter = 0; const hash = {}; for (let i = 0; i < string.length; i++) { if (string[i].**match**(/[a-z]/i) && !hash[string[i]]) { hash[string[i]] = true; counter += 1; } } return counter === 26;}
```

# [MEDIUM]编码挑战，字符串操作#2: *字谜*

*   变位词是通过重新排列不同单词的字母而形成的单词，通常只使用所有原始字母一次。
    * cat、act、atc、tca、atc
    * listen”和“silent”
*   给定两个字符串输入，找出字符串是否是变位词，并返回 true 或 false

```
function **areAnagrams**(strA, strB) {}
```

好吧，让我们**一起想想这个…**

*   重排装置..如果我们按字母顺序排列单词，它们在技术上看起来应该是一样的？
*   这些字符串需要有相同的长度
*   如果我们不分类..我们可以试着用哈希……嗯

**解决方案 1:按字母顺序排列单词**

那么我们的**伪码**是什么呢..还是我们的策略？我们可以把它写在代码的注释中

*   我们将字符串都转换成小写
*   我们从它们中删除空格(它们不会被处理)..我们可以使用 replace()来做到这一点
*   我们可以通过将两个字符串转换成数组并排序，然后再将它们变回字符串来对它们进行排序
*   如果字符串是相同的…他们是字谜！！！

```
function **areAnagrams**(strA, strB) { *// A regex to look for all spaces globally and replace them* const spaceRegex = / /g; *// Convert both strings to lowercase and remove whitespace from them* strA = strA.replace(spaceRegex, "").toLowerCase();
    strB = strB.replace(spaceRegex, "").toLowerCase(); // Short circuit.. these strings need to be the same length if (strA.length !== strB.length) { return false; } *// Convert into arrays and sort
  // Return if they are equal* return strA.**split**("").**sort**().**join**("") ===      strB.**split**("").**sort**().**join**("");} // Test casesconsole.**log**(**areAnagrams**("aFdl e  ", "adle F "));  // true
console.**log**(**areAnagrams**("aFdl e  ", "adle XX ")); // false
```

**解决方案 2:散列和循环**

那么我们的**伪码**是什么呢..还是我们的策略？我们可以把它写在代码的注释中

*   定义一个散列来存储字母
*   将两个字符串都转换成小写，并删除其中的空格
*   短路..这些字符串需要有相同的长度
*   将字符串组合成一个字符串，这样我们就可以循环
*   遍历合并后的字符串，将它们添加到哈希中，并记录它们出现的次数
*   检查哈希以查看每个字母是否存在两次以上

```
function areAnagrams(strA, strB) {// Define our hash to store the letters
    let hash = {};// A regex to look for all spaces globally and replace them
    const spaceRegex = / /g;// Convert both strings to lowercase and remove whitespace from them
    strA = strA.replace(spaceRegex, "").toLowerCase();
    strB = strB.replace(spaceRegex, "").toLowerCase();// Short circuit.. these strings need to be the same length
    if (strA.length !== strB.length) {
        return false;
    }

    // Combine the strings into one string
    const combinedString = strA.concat(strB);// Loop through the combined string and add them to the hash
    for (let i = 0; i < combinedString.length; i++) {// if it doesn't already exist in the hash
        if (!hash[combinedString[i]]) {
            // add it to the hash with a value of 1
            hash[combinedString[i]] = 1;
        } else {
            // update the occurrence
            hash[combinedString[i]] += 1; 
        }
    }// Now if it is an anagram, each letter in our hash will occur at least twice
    for (let [key, value] in hash) {
        if (value < 2) {
            return false;
        }
    }return true;

}
```

# [MEDIUM]编码挑战，字符串操作#2:回文

*   回文是一个单词或句子，前后读起来都一样
*   给定一个字符串输入，找出该字符串是否为回文，并返回 true 或 false

```
function **isPalindrome**(string) {}
```

好吧，让我们**一起想想这个…**

*   如果我们向后循环，字符串应该是相同的
*   我们需要一个正则表达式来检查字母字符
*   我们当然应该转换成小写

**方案一:反向循环！**

那么我们的**伪码**是什么呢..还是我们的策略？我们可以把它写在代码的注释中

*   我们定义了空的反向字符串，我们将在后面添加它
*   我们将字符串转换成小写
*   我们从它们中删除空格(它们不会被处理)..我们可以使用 replace()来做到这一点
*   遍历字符串并反转字符串
*   将反转的字符串与原始字符串进行比较

```
function isPalindrome(string) { const spaceRegex = / /g;
    string = string.replace(spaceRegex, "").toLowerCase();

    let backwardsString = ''; for (let i = string.length-1; i >= 0; i--) {
       backwardsString += string[i];
    } return backwardsString == string;}console.log (isPalindrome('Never odd or even'));  // true
```

*更多内容看* [***说白了. io***](http://plainenglish.io)