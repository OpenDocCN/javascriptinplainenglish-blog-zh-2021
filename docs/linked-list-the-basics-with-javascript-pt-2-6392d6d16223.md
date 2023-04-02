# JavaScript 中的链表基础

> 原文：<https://javascript.plainenglish.io/linked-list-the-basics-with-javascript-pt-2-6392d6d16223?source=collection_archive---------24----------------------->

## 如何在 JavaScript 中实现链表(第 2 部分)

![](img/555a3292c44f07c93729604608fa5389.png)

Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

*这是* [*Part 1*](https://dhruvmohapatra.medium.com/linked-list-the-basics-with-javascript-pt-1-60404df9ed) *的后续。*

欢迎回来！让我们开始解决一些问题。

我用 head 来指代链表。因为我们是通过一个 head 指针来引用这个列表的，所以它在我的…head(😅).

我将继续重用这些类，这就是为什么我将它们写在这里，这样我就不必把其余的笔记弄乱了。

```
class Node {
 constructor(data, next) {
    this.data = data;
    this.next = null;
 }
};

 class SinglyLinkedList {
 constructor() {
    this.head = null;
    this.tail = null;
 }
};
```

下面是我们如何**反转一个链表**。

1.创建一个变量“当前”和一个等于 null 的变量“先前”。

2.将标题分配给当前

3.将 head 的 next 的 referral 赋值给 head(我想说的是将 head 之后的节点标注为 head)

4.现在让当前的紧挨着前一个——实际上是把它变成零(想象把参考旋转 180 度)

5.现在将 current 赋值给 previous(现在将标签从 null 移动到它所连接的节点)

6.现在继续这样做，直到到达链表的末尾

```
const reverseList (head) => { let previous = null; let current; while (head != null) { current = head; head = head.next; current.next = previous; previous = current; } return current;}
```

**反向打印列表**非常简单。有几种方法可以做到这一点，但我最喜欢的是这个简单的递归调用。

1.如果我们不在头上，告诉程序结束

2.在下一个节点上递归调用 reversePrint 函数

3.和打印头数据

```
const reversePrint = (head) => { if (!head) { return; } reversePrint(head.next); console.log(head.data);}
```

本质上，我们要求程序自己运行这个函数。它通过第一个节点。显然还剩下更多的链表，所以它不会‘返回’/停止运行函数，它会将控制发送到下一个节点，直到我们到达末尾。现在它转过来开始执行 console.log，所以它打印最后一个，倒数第二个…一直到开头。递归不是很有意义，但是我正在学习使用它，它确实对简化程序有很大帮助。

下一个很有趣。我花了一段时间才弄明白，当我弄明白的时候，我觉得肩上的重担卸了下来。让我们试着**从一个特定的位置获取节点值，从尾节点**开始倒数。

我想到的最明显的地方是浏览列表，将值存储在一个数组中，然后检索答案。但是后来，我觉得用掉更多的内存是一种浪费，也是对不理解如何正确操作链表的一种逃避。这是我想到的。

让我们假设一个包含 6 个节点的列表。如果我们想要从尾部 2 开始的节点的值，那么一直到尾部，然后从那里回溯到 2 是有意义的。两个变量只向前比一个变量先向前后向后更有意义。我们通过迭代将两个变量分开，使得它们等于尾节点到我们寻找的节点的距离。我们通过使用初始化为 0 的索引来实现这一点。因此，当当前节点为 2 时，我们开始递增 index，并将其下一个节点赋给 result——当前节点与 result 的差值为 2，当到达列表末尾时，它会给出答案。

1.创建一个变量索引并初始化为零

2.创建变量“当前”和“结果”,并初始化为 head

3.将其下一个节点分配给当前节点

4.每移动一次就增加一个索引，每次它大于从尾部开始的位置时，就把它的下一个节点赋值给结果。-

5.这样做，直到列表结束，然后打印结果的数据

```
const nodeFromTail = (head, positionFromTail) => { let index = 0; let current = head; let result = head; while (current != null) { current = current.next; if (index++ > positionFromTail) { result = result.next } } return result.data;}
```

**比较两个链表**非常简单。

1.如果数据不相等，检查第一个节点，那么它不是重复的。

2.现在移动到下一个节点，重复第一步

3.如果我们遍历了列表，其中一个列表还没有到达末尾，那么它们就不是重复的

```
const compareLists (head1, head2) { while (head1 != null && head2 != null) { if (head1.data != head2.data) { return false; } head1 = head1.next; head2 = head2.next; } if (head1 != null || head2 != null) { return false; } return true;}
```

**合并两个有序列表**就是创建一个 if 条件和另一个递归调用。

1.如果其中一个列表为空，则返回另一个列表

2.如果 list2 的节点数据大于 list1 的，那么在 list1 的下一个节点上运行这个完全相同的函数。所以当数据实际上更大时，它会把它发送出去

3.列表 2 也是如此。

```
const mergeLists (head1, head2) { if (head1 == null || head2 == null) { return (head1 == null) ? head2 : head1; } if (head1.data < head2.data) { head1.next = mergeLists(head1.next, head2) return head1; } else { head2.next = mergeLists(head1, head2.next); return head2; }}
```

现在的问题是，如果你有两个列表和一些相同的数据点，那么这个列表将会有所有的副本。所以接下来我们尝试**从列表**中删除重复的值节点。

1.如果第一个或后面一个是空的，那么我们返回头节点

2.如果数据不等于下一个节点中的数据，则将它的下一个节点分配给头部

3.否则，将其下一个节点分配给头部的下一个节点，实际上跳过了重复的节点

4.在整个列表上运行循环

```
const removeDuplicates = (head) => { if (head == null || head.next == null) return head; let root = head; while (head.next != null) { if (head.data != head.next.data) { head = head.next; } else { head.next = head.next.next; } } return root;}
```

在我结束之前，我想解决最后一个非常有趣的问题。为了**到达链表的中间**，有两种方法:

第一，线性遍历列表，将列表切成两半，然后返回，这对于非常大的数据集来说会很慢。第二，有两个指针，一个移动 1 步，另一个移动 2 步。当第二个指针到达终点时，第一个指针将位于中间

```
const findMiddle = (head) => { let slow_ptr = head; let fast_ptr = head; if (head == null) return; if (head != null) { while (fast_ptr != null && fast_ptr.next != null) { fast_ptr = fast_ptr.next.next; slow_ptr = slow_ptr.next; } } return slow_ptr.data;}
```

基本情况就是这样。我会尽快解决更多的问题和写更多的笔记。✌️

*更多内容看*[***plain English . io***](http://plainenglish.io/)