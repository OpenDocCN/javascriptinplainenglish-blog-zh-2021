# 第 1 部分 JavaScript 中 LinkedList 操作的介绍

> 原文：<https://javascript.plainenglish.io/all-operations-of-linked-list-in-javascript-9958a4d3cb07?source=collection_archive---------8----------------------->

![](img/280e26b7dc6b575c413934eb1b6e9ed0.png)

Photo by [Markus Spiske](https://unsplash.com/@markusspiske?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/javascript?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当在面试中谈到数据结构和算法时，JavaScript 开发人员会面临问题。并不是说 JavaScript 极客不擅长开发逻辑，而是 JavaScript 作为一种语言在使用数据结构编写复杂逻辑时并不那么友好。

原因很简单。JavaScript 是一种解释型语言，所以它不像 C、C++等直接处理系统内存。

因此，在对象的帮助下，我们需要模拟不同数据结构的行为，如树、LinkedList、HashMap 等。我已经决定写一系列的文章来讨论这些话题。在本文中，让我们看看如何在 JavaScript 中创建和执行不同的 LinkedList 操作。

## 什么是链接列表？

[维基百科](https://en.wikipedia.org/wiki/Linked_list)定义如下:

> 在计算机科学中，链表是数据元素的线性集合，其顺序不是由它们在内存中的物理位置给出的。相反，每个元素指向下一个。它是一种数据结构，由共同代表一个序列的节点集合组成。

## 如何用 JavaScript 创建 LinkedList？

我们需要为 LinkedList 创建的第一件事是 node。我们可以通过创建一个类来实现。

```
class Node {// constructorconstructor(element){**this**.element = element;**this**.next = **null**}}
```

接下来，创建 LinkedList。

```
class LinkedList {constructor(){**this**.head = **null**; // By default there will be just one node, so it's //head will be null**this**.size = 0; // By default size of Linked list is zero}
// All linkedin operations like add, delete, find node goes here}
```

方法在 LinkedList 中添加/移除元素。

```
class LinkedList {constructor(){**this**.head = **null**; **this**.size = 0; } add(element){ **var** node = **new** Node(element); // Create a node before adding **var** current; **if** (**this**.head == **null**) //For first element **this**.head = node; **else** { // Iterate till the last item and add value current = **this**.head; **while** (current.next) { current = current.next; } current.next = node; } **this**.size++; }removeFrom(index){
// There has to be element before removal**if** (index < 0 || index >= **this**.size) { **return** console.log("Please Enter a valid index");
}**else** { // We don't delete any value, we just remove reference to it **var** curr, prev, it = 0; curr = **this**.head; prev = curr; **if** (index === 0) { **this**.head = curr.next; } **else** { **while** (it < index) { it++; prev = curr; curr = curr.next; } prev.next = curr.next;} **this**.size--; **return** curr.element;}}
printList(){**var** curr = **this**.head;**var** str = "";**while** (curr) {str += curr.element + " ";curr = curr.next;}console.log(str);}}
```

要创建 LinkedList 并访问其中的方法，请在上述两个类之外编写下面的代码。

```
// creating an object for the// Linkedlist class**var** ll = **new** LinkedList();// adding element to the listll.add(10);// prints 10ll.printList();// adding more elements to the listll.add(20);ll.add(30);ll.add(40);ll.add(50);// returns 10 20 30 40 50ll.printList();
ll.removeFrom(0);// returns 20 30 40 50ll.printList();
```

面试时会问很多与 LinkedList 相关的重要问题。我将在下一篇文章中讨论这些内容。此外，我将在这一系列文章中解释 LinkedList 如何在 JavaScript 中工作。敬请期待，阅读愉快。

不要错过当前文章的后续部分:

第 2 部分—[JavaScript 中链表操作的介绍—第 2 部分(JavaScript 中链表的工作原理)](/an-introduction-to-linkedlist-operations-in-javascript-part-2-how-linkedlist-works-in-ee8452f0fa3f)

同一作者的其他文章:

1.  [JavaScript 中的一切都是对象吗？](https://mevasanth.medium.com/how-everything-is-object-in-javascript-a4164d7e6a2d)
2.  [JavaScript 吊装:访谈热点](https://mevasanth.medium.com/hoisting-in-javascript-hot-topic-for-interview-43b463a6a77?source=follow_footer---------0----------------------------)
3.  [JavaScript 中的记忆化——采访热门话题](https://mevasanth.medium.com/memoization-in-javascript-hot-topic-for-interview-815475544ab0)

点击[此处](https://mevasanth.medium.com/)查看作者所有文章。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)