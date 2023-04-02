# 如何在 Vanilla JS 中创建和更新列表

> 原文：<https://javascript.plainenglish.io/working-with-the-dom-in-vanilla-js-apps-part-2-ebd9a8064f6c?source=collection_archive---------3----------------------->

## 在普通 JS 应用程序中使用 DOM(第 2 部分):创建和更新列表

![](img/1556cf3a94082679594470a1a786427d.png)

我在之前的帖子[中承诺过，我会在这个帖子中涵盖列表。我们将讨论使用列表的几种不同方法，这些方法应该涵盖大多数常见的情况。](https://medium.com/@hayavuk/working-with-the-dom-in-vanilla-js-apps-part-1-bf8ccc0faaed)

然而，这些方法并不是唯一的。我们在这里的目标不是涵盖所有可能的边缘情况，而是提供在大多数时候都有效的解决方案，或者至少作为一个良好的基础。

我将介绍的方法有:

*   带有隐藏元素的静态列表
*   任意长度的动态列表
*   具有未使用节点池的动态列表

我还将介绍列表排序，并分享一个 CSS 小技巧来提高列表呈现性能。

# 静态列表

静态列表最常用于从不改变的列表(例如，预先知道的选择列表中的选项)，但是它们也可以用于本身不是静态的数据。当我们的数据是一个任意长度的列表时，我们仍然可以通过一次只显示列表的一个子集来将其映射到一个静态列表。

例如，在这种情况下，可以使用分页来促进子集的选择。在我们的 HTML 中，我们将创建足够的元素来覆盖单个页面。这些元素最初都是隐藏的。当我们要渲染一些数据的时候，我们会先根据数据更新每个元素，然后显示更新的项目。

因为我提前知道了呈现的项目的数量，并且在 HTML 中有它们，所以我可以提前预选所有的元素。

```
let $$listItems = document.querySelectorAll('.list-item')
```

更新静态列表的技巧是总是迭代元素而不是数据:

```
let data = []let updateList = () => {
  $$listItems.forEach(($item, idx) => {
    let item = data[idx]
    if (itemx) {
      $item.querySelector('.title').textContent = item.title
      $item.querySelector('.price').textContent = item.price
    }
    $item.classList.toggle('hidden', item == null)
  })
}
```

当我检查现有的列表项元素时，我试图将它们与数据进行匹配。如果没有数据，那么我隐藏元素。不然我先填空再揭示。

重要的是重申你要先填空，然后*再*揭示物品。这减少了回流和重画的次数。

我可以对更长的列表使用分页来重用静态列表。上面的例子非常适合这种情况:

```
let data = []
let startPage = 0
let endPage = 10let updateList = () => {
  let shownData = data.slice(startPage, endPage + 1)
  $$listItems.forEach(($item, idx) => {
    let item = shownData[idx]
    if (itemx) {
      $item.querySelector('.title').textContent = item.title
      $item.querySelector('.price').textContent = item.price
    }
    $item.classList.toggle('hidden', item == null)
  })
}
```

对于分页列表，我简单地将`startPage`和`endPage`变量添加到应用程序状态中。(假设我通过用户交互来更新它们。)然后我创建一个`shownData`作为整个数组的一部分，并将列表项映射到它，而不是整个`data`数组。

## 添加事件侦听器

列表的某些部分可能是交互式的。在这种情况下，我们需要添加事件侦听器。我们有几个选择，但是我最常用的方法是给所有列表项添加事件监听器，然后使用`data-*`属性来控制监听器要做什么。

```
let updateList = () => {
  $$listItems.forEach(($item, idx) => {
    let item = data[idx]
    if (itemx) {
      $item.querySelector('.title').textContent = item.title
      $item.querySelector('.price').textContent = item.price
    }
    $item.classList.toggle('hidden', item == null)
    **$item.dataset.index = idx**
  })
} $$listItems.forEach($item => {
  $item.querySelector('.delete').onclick = () => 
    onDeleteItem(**Number($item.dataset.index)**)
});
```

# 动态列表

有时，由于 UX 的原因，我们可能希望避免分页。相反，我们可以使用“加载更多”按钮或使用`[IntersectionObserver](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)`自动加载列表末尾的附加项目。

在这种情况下，我发现在 JavaScript 中创建 DOM 节点比在 HTML 中创建更简单。我称这种方法为“动态列表”

虽然如果初始项目的数量总是相同的话，这种方法可以与静态列表相结合，但是我发现如果我在简单的情况下坚持使用这种或那种方法，代码总体上会更简单。我还将在后面介绍混合方法，在那里我将介绍一个更合适的例子。

当使用动态列表方法时，我通常有一个单独的函数来创建列表项元素。我们可以将元素创建为字符串或 DOM 节点。至于使用字符串和使用`document.createElement`创建顶级 DOM 节点之间的性能差异，应该没有太大的区别。主要区别在于您是立即获得对列表项节点的引用，还是必须在以后选择它们。

让我们来看看这两种方法。

## 仅使用字符串创建列表项

下面是一个仅使用字符串的示例:

```
const ITEMS_PER_PAGE = 10let data = []
let nShown = 0let nextPage = () => nShown += ITEMS_PER_PAGElet $list = document.getElementById('list')
let $loadMore = document.getElementById('load-more')let createItem = item => `
  <li class="list-item">
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
  </li>
`
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  let $t = document.createElement('template')
  $t.content.innerHTML = itemsToShow.map(createItem).join('')
  $list.append($t.content)
}let onLoadMore = () => {
  appendItems()
  nextPage()
}$loadMore.onclick = onLoadMoreonLoadMore()
```

需要注意一些事情:

我使用模板字符串将数据嵌入到生成的 HTML 中。这意味着你必须小心数据的来源。如果是用户提供的数据，你有可能成为 XSS 攻击的牺牲品，所以你应该采取额外的措施来确保数据是经过净化的(例如，不包含 HTML)。

我们首先使用一个`template`元素来收集新创建的项目。`template`元素的工作方式类似于[文档片段](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment)，除了它支持`innerHTML`属性，而后者不支持。

## 使用字符串和 DOM 节点创建列表项

下面是一个使用组合字符串和 DOM 节点的示例:

```
const ITEMS_PER_PAGE = 10let data = []
let nShown = 0let nextPage = () => nShown += ITEMS_PER_PAGElet $list = document.getElementById('list')
let $loadMore = document.getElementById('load-more')let createItem = item => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
  `
  return $el
}
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  $list.append(...itemsToShow.map(createItem))
}let onLoadMore = () => {
  appendItems()
  nextPage()
}$loadMore.onclick = onLoadMoreonLoadMore()
```

与只有字符串的版本不同，我们不必使用`template`元素来创建 DOM 节点。作为一种折衷，我们不能将顶级列表项元素本身定义为字符串。

## 添加事件侦听器

这两种方法之间的区别不仅仅是表面上的。使用第二种方法，我们可以引用列表项节点，而不必选择它。因此，在我可能需要添加事件侦听器和类似于列表项节点或其子节点的情况下，我更喜欢第二种方法。

也就是说，选择节点通常是一种优化良好的操作，所以我不期望它会对性能产生明显的影响。

让我们看看如何在这两种情况下添加事件侦听器。

首先是只有字符串的方法:

```
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  let $t = document.createElement('template')
  $t.content.innerHTML = itemsToShow.map(createItem).join('')
  **$t.content.querySelectorAll('.buy-now')**.forEach(($btn, idx) => {
    let dataIdx = nShown + idx
    **$btn.onclick = () => onBuyNow(dataIdx)**
  })
  $list.append($t.content)
}
```

使用混合方法:

```
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  $list.append(...itemsToShow.map((item, idx) => {
    let $el = createItem(item)
    let dataIdx = nShown + idx
    **$el.querySelector('.buy-now').onclick = () => onBuyNow(dataIdx)**
  }))
}
```

对于这两种方法，我们也可以使用延迟事件处理程序。延迟处理程序被绑定到所有列表项的公共祖先(通常是直接的父节点)，我们计算侦听器中的实际目标是什么。

在基于字符串的节点创建中，我们可以避免使用延迟事件处理程序选择创建的节点，因此延迟事件侦听器有时可以稍微简化代码。不过，延迟事件处理程序没有那么高效，所以这是一种权衡。

```
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  let $t = document.createElement('template')
  $t.content.innerHTML = itemsToShow.map(createItem).join('')
  $list.append($t.content)
}$list.onclick = ev => {
  let $realTarget = ev.target.closest('.buy-now')
  if ($realTarget) onBuyNow($realTarget.dataset.index)
}
```

在这个例子中，我正在进行检查，以确定是否需要对 click 事件做出反应。使用`Element.closest()`的检查测试被点击的元素是或者包含在一个`.buy-now`元素中。为了让上面的例子正常工作，我将在按钮上使用一个`data-index`属性来计算出我们正在谈论的项目，否则事件监听器将无法访问这些信息。

# 带有节点池的动态列表

前面的动态列表示例只实现了在末尾添加新的条目。如果我们需要删除项目或者在中间插入新的项目呢？如何将物品从一个位置移动到另一个位置？为此，我将使用稍微不同的方法来维护节点池。

节点池只是一个数组，包含对 DOM 节点的引用，这些引用与底层数据的顺序相同。这类似于我们对静态列表所做的，在静态列表中，我们为 HTML 页面中的元素创建了一个对节点集合的引用，但是我们是为动态创建的元素创建的。

向列表中添加节点的基本操作与前面的例子相同，即使用列表元素的 DOM 节点创建动态列表。唯一的区别是，我们还在创建时将节点添加到节点池中。

```
const ITEMS_PER_PAGE = 10// State
let data = []
let nShown = 0// State manipulation
let nextPage = () => nShown += ITEMS_PER_PAGE// DOM references
let $list = document.getElementById('list')
**let $$listItems = []**
let $loadMore = document.getElementById('load-more')// DOM manipulation
let createItem = (item) => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
  `
  return $el
}
let appendItems = () => {
  let itemsToShow = data.slice(nShown, nShown + ITEMS_PER_PAGE)
  let $$items = itemsToShow.map(createItem)
  $list.append(...$$items)
 **$$listItems.push(...$items)**
}// Event handlers
let onLoadMore = () => {
  appendItems()
  nextPage()
}// Event bindings
$loadMore.onclick = onLoadMore// Initial view
onLoadMore()
```

删除项目时，我会同时从数据和节点池中删除它们:

```
// State manipulation **let deleteItem = idx => {
  data.splice(idx, 1)
  nShown--
}**// DOM manipulation
let createItem = (item) => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
 **<button class="delete">Delete</button>**
  `
  **$el.querySelector('.delete').onclick = () => onDeleteItem($el)**
  return $el
}
**let removeListItem = $item => {
  $list.removeChild($item)
  $$listItems.splice($$listItems.indexOf($item), 1)
}**// Event handlers **let onDeleteItem = $item => {
  deleteItem($$listItems.indexOf($item))
  removeListItem($item)
}**
```

因为我总是确保`$$listItems`阵列中的节点池与数据同步，所以我可以通过查找池中节点的索引来查找底层数据的索引。我还减少了显示的项目数，因为一个显示的项目被删除了。我也可以显示一个项目，而不是减少项目的数量。

```
// State manipulationlet deleteItem = idx => **data.splice(idx, 1)**// DOM manipulation
let removeListItem = $item => {
  $list.removeChild($item)
  $$listItems.splice($$listItems.indexOf($item), 1)
 **let newItem = data[nShown - 1]
  let $newItem = createItem(newItem)
  $list.append($newItem)
  $$listItems.push($newItem)**
}
```

当插入或移动项目时，我们将再次对数据和节点池执行相同的操作。下面是一个插入的例子:

```
// State manipulation
**let insertItem = (idx, title, price) => {
  data.splice(idx, 0, { title, price })
  nShown++
}**// DOM references
**$titleField = document.getElementById('title-field')
$priceField = document.getElementById('price-field')**// DOM manipulation
let createItem = (item) => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
 **<button class="insert">Insert new item here</button>**
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
    <button class="delete">Delete</button>
  `
  $el.querySelector('.delete').onclick = () => onDeleteItem($el)
 **$el.querySelector('.insert').onclick = () => onInsertItem($el)**  return $el
}
**let insertListItemBefore = $item => {
  let idx = $listItems.indexOf($item)
  let item = data[idx]
  let $newItem = createItem(item)
  $list.insertBefore($newItem, $item)
  $$listItems.splice(idx, 0, $newItem)
}**// Event handlers
**let onInsertItem = $item => {
  insertItem(
    $$listItems.indexOf($item),
    $titleField.value
    $priceField.value
  )
  insertListItemBefore($item)
}**
```

# 使用节点池交换列表

还有另一种情况，我会使用节点池。如果列表不断用全新的数据集更新，我会保留池并更新现有的项目，而不是每次都创建全新的项目。这是一种结合了前面例子中使用的各种技术的方法。

在下面的例子中，我们从 HTML 页面中的一个静态列表开始，有足够的元素来覆盖通常的情况。这些列表项元素会立即添加到池中。然后，随着数据集的增长，池会扩展，但元素不会被删除，而是被隐藏。为了简单起见，我们不做“加载更多”的部分。

```
let $list = document.getElementById('list')
let $$listItems = []let createItem = item => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price}</span>
    <button class="delete">Delete</button>
  `
  $el.querySelector('.delete').onclick = () => onDeleteItem($el)
  return $el
}
let updateItem = ($item, item) => {
  $item.querySelector('.item-title').textContent = item.title
  $item.querySelector('.item-price').textContent = item.price
  $item.classList.remove('hidden')
}
let updateList = () => {
  let $$createdItems = []data.forEach(function (item, idx) {
    let $item = $$listItems[idx]
    if ($item == null) {
      $item = createItem(item)
      $$listItems.push($item)
      $$createdItems.push($item)
    }
    else updateItem($item)
  })
  $list.append(...$createdItems)
for (let i = data.length, l = $$listItems.length; i < l; i++) {
    $$listItems[i].classList.add('hidden')
  }
}
let deleteListItem = $item => {
  $item.classList.add('hidden')
  $$listItems.splice($$listItems.indexOf($item), 1)
  $$listItems.push($item)
}
```

# 排序列表

在对列表进行排序时，我们总是从数据开始，并将排序后的数据同步到 DOM。因为我们有几种不同的方法来管理列表，所以我们也有几种不同的方法来将排序后的数据转换成 DOM 操作。

当我们没有在任何给定的时间显示整个列表时，我通常的做法是简单地做与呈现列表项相同的事情:我对数据进行排序，然后更新所有呈现的列表项以匹配数据。

如果我们要显示整个列表，那么只对 DOM 节点重新排序会更有效。一个简单的实现只是简单地按照节点在数据中出现的顺序添加节点。在大多数情况下，这种方式非常有效。然而，要做到这一点，我们需要一个将数据映射到节点的索引。

```
// State
let data = []// State manipulation
let sortByPrice = () => data.sort((a, b) => 
  a.price - b.price)
let sortByTitle = () => data.sort((a, b) => 
  a.title.localeCompare(b.title))// DOM references
let $list = document.getElementById('list')
let $sortByTitle = document.getElementById('sort-title')
let $sortByPrice = document.getElementById('sort-price')
**let listItemIndex = new Map()**// DOM manipulation
let createItem = item => {
  let $el = document.createElement('li')
  $el.className = 'list-item'
  $el.innerHTML = `
    <span class="item-title">${item.title}</span>
    <span class="item-price">${item.price.toFixed(2)}</span>
  `
  return $el
}
let appendItems = () => {
  let $$items = data.map(item => {
    let $item = createItem(item)
    **listItemIndex.set(item, $item)**
    return $item
  })
  $list.append(...$$items)
}
**let sortListItems = () => {
  let $$sortedItems = data.map(item => listItemIndex.get(item))
  $list.append(...$$sortedItems)
}**// Event handlers
let onSortByTitle = () => {
  sortByTitle()
  sortListItems()
}
let onSortByPrice = () => {
  sortByPrice()
  sortListItems()
}// Event bindings
$sortByTitle.onclick = onSortByTitle
$sortByPrice.onclick = onSortByPrice// Initial view
appendItems()
```

感兴趣的函数是上面代码片段中突出显示的`sortListItems()`。当节点被附加到新位置时，它们会自动从先前的位置移除。我利用了这一点，只是按照正确的(更新后的)顺序将节点附加到父节点。

# 渲染和回流性能改进

使用列表时，如果列表项的大小保持不变，而与内容无关，则可以对列表项使用以下 CSS 规则来提高呈现性能:

```
.list-item {
  contain: content;
}
```

你可以在 MDN 上阅读更多关于`contain`属性[的内容，但它的缺点是它向浏览器表明这些项目可以独立于页面的其余部分重新呈现。这加快了布局计算的速度。](https://developer.mozilla.org/en-US/docs/Web/CSS/contain)

# 结论

这是关于普通 JS 应用程序中 DOM 操作的两部分系列和我的普通 JS 开发系列的结论。不过，这不是我就这个话题写的最后一篇文章。在以后的文章中，我希望分享我在继续追求简化前端开发(对我来说)的过程中遇到的更高级的小细节。

# *你愿意全职和香草 JS 一起工作吗？*

*如果你想加入一个遵循上述原则的团队，你可能会有兴趣了解一下*[*Coin Metrics*](https://coinmetrics.io/)*是* [*招聘*](https://boards.greenhouse.io/coinmetrics/jobs/4031704004) *(香草)JavaScript 开发人员加入他们的前端工程团队。*

*更多内容请看*[*plain English . io*](http://plainenglish.io/)*。报名参加我们的* [*免费周报在这里*](http://newsletter.plainenglish.io/) *。*