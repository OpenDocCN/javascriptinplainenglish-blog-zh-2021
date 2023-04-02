# 如何用 Next.js 做动态路由

> 原文：<https://javascript.plainenglish.io/how-to-do-dynamic-routing-with-next-js-9cd85abd9083?source=collection_archive---------10----------------------->

![](img/106ae9ecaeb4d6e90283b44fd0c655f0.png)

动态路由意味着我们不想为页面指定静态路由；它将使用来自 API 或其他方式的数据动态生成。考虑你建立一个组合网站，它可能有网页，如关于，联系，和主页，我们需要为每个网页静态定义路线。然而，在博客的情况下，每篇文章都有一个主页、分类页面和详细页面；这个详细的页面不能用静态路由器定义，因为可能会找到数百个博客帖子，并且不可能为每个帖子定义单独的路由器。在这种情况下，我们为每个 post 使用一个动态路由器，然后在运行时为每个 post 生成一个路由器。

# 实施动态路由

我们将借助一个示例项目来实现动态路由。该项目将不得不显示一个特定的股票名称及其价格。在这个例子中，每只股票都有其相应的页面，这意味着如果你导航到这个链接[http://localhost:3000/Apple](http://localhost:3000/apple)，该页面将显示苹果公司的股票名称和价格。

第一步是设置在终端上运行相应代码的项目。

```
npx create-next-app
```

之后，您的工作区中将会有一个 Next.js 样板文件。在项目的文件结构中，您可以看到一个名为 pages 的文件夹，在 pages 内部创建一个名为[stock].js 的文件。

将下面的代码片段复制到[stock]中。js 文件；您可以看到两个函数，getStaticPaths 和 getAllStockPaths。Next.js 提供了用于实现动态路由的函数 getStaticPaths，函数 getAllStockPaths 获取所有要在 URL 上显示的路径名。

```
export async function getStaticPaths() {
    const paths = getAllStockPaths()
    return {
      paths,
      fallback: false
    }
  }/*
 *  File Name: [stock].js
 *  Description: This function retrieves all the stock name from
 *  API.                                  
 */const getAllStockPaths = () => {
      return    [
          {
            params: {
              stock : 'apple'
            }
          },
          {
            params: {
              stock: 'facebook'
            }
          }
        ];
  }
```

将下面的代码片段添加到[stock]中。这里有两个函数，getStaticProps 和 getStockData。Next.js 提供了 getStaticProps 函数，用于在初始页面加载期间调用函数，这里我们调用 getStockData 函数，它将获取所有股票信息。

```
export async function getStaticProps({ params }) {
    const postData = getStockData(params.stock)
    return {
      props: {
        postData
      }
    }
  }/*
 * File Name: [stock].js
 * Description: This function retrieves all the stock information
 * from API. 
 */
  const getStockData = (stock) => {
    const stockInfo =     {
        apple : {
            stock : 'apple',
            price : '100$'
        },
        facebook : {
            stock: 'facebook',
            price : '200$'
        }
    };return stockInfo[stock];
}
```

最后，我们可以添加 render 方法，并将所有这些代码片段打包到一个文件中。编译完代码后，当你访问[http://localhost:3000/Facebook](http://localhost:3000/facebook)时，你可以看到脸书的股票价格，而访问[http://localhost:3000/Apple](http://localhost:3000/apple)时，你可以看到苹果公司的股票价格。

```
export default function Home({ postData }) {
    return (
      <div>
        {`Stock is ${postData.stock}`}
        <div/>
        {`price is ${postData.price}`}
      </div>
    )
  }export async function getStaticPaths() {
    const paths = getAllStockPaths()
    return {
      paths,
      fallback: false
    }
  }export async function getStaticProps({ params }) {
    const postData = getStockData(params.stock)
    return {
      props: {
        postData
      }
    }
  }/*
 * File Name: [stock].js
 * Description: This function retrieves all the stock name from API. 
 */
  const getAllStockPaths = () => {
      return    [
          {
            params: {
              stock : 'apple'
            }
          },
          {
            params: {
              stock: 'facebook'
            }
          }
        ];
  }/*
 * File Name: [stock].js
 * Description: This function retrieves all the stock information
 *  from API. 
 */
  const getStockData = (stock) => {
    const stockInfo =     {
        apple : {
            stock : 'apple',
            price : '100$'
        },
        facebook : {
            stock: 'facebook',
            price : '200$'
        }
    };return stockInfo[stock];
}
```

## 结论

感谢您的阅读。我希望您发现这很有用，并且对了解如何使用 Next.js 创建动态路线有所了解。

*更多内容请看*[***plain English . io***](https://plainenglish.io/)