# 用 React 呈现大型列表的方法

> 原文：<https://javascript.plainenglish.io/ways-to-render-large-lists-with-react-82421b7498a6?source=collection_archive---------7----------------------->

![](img/731be3cfe1c0b67661018238678175af.png)

Photo by [Jenny Smith](https://unsplash.com/@chasingafterdear?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

我们经常要在 React 应用中渲染大型列表。

在本文中，我们将研究在 React 应用程序中呈现大型列表的方法。

# 页码

我们可以使用 react-paginate 库向 react 列表添加分页。

要安装它，我们运行:

```
npm i react-paginate
```

然后我们可以通过写来使用它:

```
import React, { useEffect, useState } from "react";
import ReactPaginate from "react-paginate";export default function App() {
  const [pagination, setPagination] = useState({
    data: new Array(1000).fill().map((value, index) => ({
      id: index,
      title: index,
      body: index
    })),
    offset: 0,
    numberPerPage: 10,
    pageCount: 0,
    currentData: []
  });
  useEffect(() => {
    setPagination((prevState) => ({
      ...prevState,
      pageCount: prevState.data.length / prevState.numberPerPage,
      currentData: prevState.data.slice(
        pagination.offset,
        pagination.offset + pagination.numberPerPage
      )
    }));
  }, [pagination.numberPerPage, pagination.offset]);
  const handlePageClick = (event) => {
    const selected = event.selected;
    const offset = selected * pagination.numberPerPage;
    setPagination({ ...pagination, offset });
  };
  return (
    <div>
      {pagination.currentData &&
        pagination.currentData.map((item, index) => (
          <div key={item.id} className="post">
            <h3>{item.title}</h3>
            <p>item {item.body}</p>
          </div>
        ))}
      <ReactPaginate
        previousLabel="previous"
        nextLabel="next"
        breakLabel="..."
        pageCount={pagination.pageCount}
        marginPagesDisplayed={2}
        pageRangeDisplayed={5}
        onPageChange={handlePageClick}
        containerClassName={"pagination"}
        activeClassName={"active"}
      />
    </div>
  );
}
```

组件让我们可以将分页控件添加到 React 应用程序中。

我们使用`handlePageClick`方法从数组中获取数据，并对其进行切片，以获得给定页码的所需项目。

`currentData`拥有当前页面的数据。

我们从`event.selected`属性中获取页码。

使用分页，我们每页加载少量数据。

# 无限卷轴

加载大量数据的另一种方法是使用无限滚动。

当我们向下滚动时，我们将更多的数据附加到列表中。

为了增加无限滚动，我们可以使用`react-infinite-scroll-component`库。

我们可以通过运行以下命令来安装它:

```
npm i react-infinite-scroll-component
```

然后我们可以通过写来使用它:

```
import React, { useState } from "react";
import InfiniteScroll from "react-infinite-scroll-component";export default function App() {
  const data = new Array(1000).fill().map((value, id) => ({
    id: id,
    title: id,
    body: id
  })); const [count, setCount] = useState({
    prev: 0,
    next: 10
  });
  const [hasMore, setHasMore] = useState(true);
  const [current, setCurrent] = useState(data.slice(count.prev, count.next)); const getMoreData = () => {
    if (current.length === data.length) {
      setHasMore(false);
      return;
    }
    setTimeout(() => {
      setCurrent(current.concat(data.slice(count.prev + 10, count.next + 10)));
    }, 2000);
    setCount((prevState) => ({
      prev: prevState.prev + 10,
      next: prevState.next + 10
    }));
  }; return (
    <InfiniteScroll
      dataLength={current.length}
      next={getMoreData}
      hasMore={hasMore}
      loader={<h4>Loading...</h4>}
    >
      <div>
        {current &&
          current.map((item, index) => (
            <div key={index} className="post">
              <h3>{item.title}</h3>
              <p>item {item.body}</p>
            </div>
          ))}
      </div>
    </InfiniteScroll>
  );
}
```

我们添加了`InfiniteScroll`组件来添加无限滚动容器。

`dataLength`当我们向下滚动时，有多少项目要加载。

我们用`getMoreData`方法从数组中获得更多的数据。

我们加载新数据并将其添加到`setTimeout`回调中的`current`数组中。

然后更新`count.prev`和`count.next`属性来更新我们想要获取的项目的索引。

# 结论

我们可以在 React 应用程序中添加分页和无限滚动，以高效的方式加载大量数据。

喜欢这篇文章吗？如果有，通过 [**订阅我们的 YouTube 频道**](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw?sub_confirmation=true) **获取更多类似内容！**

*更多内容请看*[***plain English . io***](https://plainenglish.io/)