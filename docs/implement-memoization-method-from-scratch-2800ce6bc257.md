# 如何从头开始实现 JavaScript 记忆化

> 原文：<https://javascript.plainenglish.io/implement-memoization-method-from-scratch-2800ce6bc257?source=collection_archive---------16----------------------->

![](img/1ca83e4c9b7b920afb351ec74e2d86d7.png)

Photo by [david hebert](https://unsplash.com/@piscesdave?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

在我们谈论记忆化之前，让我们先了解计算机中的值是如何转换的。

假设我们有一个将两个数相加的函数。如果我们有一个程序用相同的输入调用这个函数 50 次，我们将会做很多不必要的计算。

进入记忆化。

记忆化是一种优化技术，用于通过存储函数调用的结果来加速计算机程序，而无需重新计算(假设进行函数调用的参数和变量是相同的)。

下面我们来看看:

请注意,“计算结果”仅在结果未被记忆时计算。如果 memoize 函数按预期工作，那么 addFunc 将只被调用一次，此后对 memoizedFn 的任何调用都将返回一个已经存储在内存中的结果。

让我们来看看 memoizedFn 的实现:

我知道这有点冗长，但我们可以这样看。我们有一个 memoizedResults 来缓存所有已经计算的结果。

例如，如果我们在用户调用 memoized 函数时将 addNumber 作为参数传入，它首先检查 memoizedResults 中的函数定义是否可用。如果是，我们通过引用 memoizedResults[func].result 获取缓存的结果。

假设我们已经缓存了结果。我们仍然需要检查论点是否改变了。想象一下，如果我们调用 addNumber(1，2，3)。这很好，我们将把 addNumber 作为一个键存储在 memoizedResult 中，结果字段为 6，args 包含 1，2，3。如果我们调用 addNumber(3，4，5)呢？当然，我们已经存储了 memoizedResult 的结果，但是如果我们使用缓存的结果，那么 addNumber(3，4，5)将不会返回正确的结果。

![](img/612b0149daf5f32575ba2686e03b8f21.png)

Photo by [Jon Tyson](https://unsplash.com/@jontyson?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

那么，我们如何确保正确使用缓存的结果，以及何时根据需要重新计算结果？

比方说，如果我们第一次将 memoizedFn 设置为 addNumber，并调用 memoizedFn(1，2，3)一次。第一次，我们将 args 和 func 名称一起存储到映射中。当我们调用 memoizedFn(3，4，5)时，我们调用 getArgKeysFromMemoized 和 getArgValsFromMemoized 来检查我们记忆的参数是否与最近一次函数调用中传递的参数相同。在这种情况下，如果它们不相同，我们重新计算结果，并再次将它们存储到我们的地图中。最后，我们简单地从地图返回结果。

让我们问自己这个问题:为什么记忆化？早些时候，我们确实说过要获取某个数据 50 次，但这真的是个问题吗？

是的，可以。

如果这些数据包含数百万、数十亿行数据，该怎么办？如果我们记住了它，那么除非需要，否则我们不必检索这些数据。想象一下，有一个应用程序调用 api 来获取一百万行项目，并将它们存储在本地内存中。如果我们实现了一个强大的记忆机制，我们可以在获取最新数据之前检查这些数据是否发生了变化。

请记住，保存 api 的每个操作都是我们不需要的每一百万个数据。在某些情况下，这可能就是拥有一个快速高效的应用程序与一个由于要检索的数据量而无法正常运行的应用程序之间的区别。

*更多内容看*[***plain English . io***](http://plainenglish.io)