# 什么是时间复杂度？

> 原文：<https://javascript.plainenglish.io/what-is-time-complexity-1211eeb70f69?source=collection_archive---------3----------------------->

## 时间复杂性简介

![](img/b781439c397572a4d87676b5ff20b2b7.png)

Photo by [Luke Chesser](https://unsplash.com/@lukechesser?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

时间复杂性的一个简单明了的定义是——“执行程序中每条语句所需的时间**”。**

**我们也可以把时间复杂度描述为程序运行所需的时间。我们用大 O 符号来定义时间复杂度，这是迄今为止表示程序时间复杂度的标准形式。**

****让我们通过例子来看看不同类型的时间复杂性—****

**在开始这篇文章之前，我想让你知道，现在你可以通过电子邮件与我联系。别担心，我只会给你发送与技术相关的文章，让你在整个 2022 年都保持更新。点击这里并添加您的电子邮件。看，这很容易。 (我保证不会给你的收件箱发垃圾邮件)**

**[](https://medium.datadriveninvestor.com/does-elon-musk-hate-the-idea-of-web-3-0-nft-and-blockchain-technology-ff7b28601c17) [## 埃隆·马斯克讨厌 Web 3.0、NFT 和区块链技术吗

### 埃隆·马斯克在 Web3.0 和 NFT 上发布的推文

medium.datadriveninvestor.com](https://medium.datadriveninvestor.com/does-elon-musk-hate-the-idea-of-web-3-0-nft-and-blockchain-technology-ff7b28601c17)** 

## **常数时间 O(1)**

**它基本上以恒定的时间运行程序，并且与任何输入大小无关。在这种情况下，运行时总是相同的。下面是具有恒定时间复杂性的代码示例。**

```
int main()
{
print("This code has time complexity O(1) to run");}
```

## **线性时间 O(n)**

**这取决于输入大小。例如，让我们假设一个代码接受一个大小为 n 的数组。基本上，它需要 n 的时间来接受一个大小为 n 的数组。**

```
int main()
{
int n;
input(n)        //size of array int array[n];for(int i=0;i<n;i++)
{
   input(a[i]);}as we can see that the for loop will run n times hence the time complexity is O(n) of the above code.
```

## **二次时间 O(n)**

**如果一个程序执行一个语句 n*n 次，它将具有二次时间复杂度。例如，让我们假设一个代码片段接受一个 n*n 大小的 2d 数组。在这种情况下，我们将使用 2 个`for`循环，每个循环将运行 n 次。因此，时间复杂度将是二次的。**

```
int main()
{
int array[n][n];for(int i=0;i<n;i++)
    {
     for(int j=0;j<n;j++)
         {
            input(array[i][j]);
          }
     }Here the input statement will get executed for n*n time, hence the time complexity will be O(n^2)
```

**还有不同类型的其他时间复杂度，如 O(n*m)和对数时间复杂度 O(log n)。时间复杂性确实有助于程序员发现他的代码是否足够有效。**

**希望这篇文章对新程序员有帮助。不断学习，不断成长。祝你编程之旅好运。**

**[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

aniketz.medium.com](https://aniketz.medium.com/membership) [](/top-5-technology-related-articles-you-should-read-f9b262558fab) [## 你应该阅读的 5 篇与技术相关的文章

### # 12 月版

javascript.plainenglish.io](/top-5-technology-related-articles-you-should-read-f9b262558fab) 

*更多内容看* [***说白了. io***](http://plainenglish.io/) ***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。*****