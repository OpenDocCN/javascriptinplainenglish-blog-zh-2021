# 如何在 React 中创建搜索栏

> 原文：<https://javascript.plainenglish.io/how-to-implement-a-search-bar-in-react-js-8cf8f5513b8e?source=collection_archive---------0----------------------->

![](img/00209a5d14332df414ed20cbaaddeda8.png)

Image by [istockphoto](https://www.istockphoto.com/illustrations/search-box)

在许多网站上，搜索栏是一种非常常见的输入方式。它改善了任何 web 应用程序的用户体验。它通过减少从很长的列表中查找数据所花费的时间来做到这一点。对于一些开发人员来说，在单页应用程序中添加搜索栏是一项挑战。本文将一步一步向您展示如何使用 React js 中的搜索栏过滤一长串数据。

## **第一步**

创建一个全新的 React 应用程序。称之为搜索应用。[在这里阅读 React 安装步骤](https://reactjs.org/docs/create-a-new-react-app.html)

```
npx create-react-app search-app
```

## **第二步**

在应用程序项目的 */src* 文件夹中创建一个名为 components 的文件夹。在 components 文件夹中，创建一个名为 *searchBar.js* 的文件。导入 React，并将 ***useState*** 挂钩到该文件。

```
import React, {useState} from 'react'
```

## **第三步**

使用 ES6 语法创建一个名为 *searchBar* 的功能组件。

```
import React, {useState} from 'react'

const searchBar = () => {}
```

## **第四步**

使用 useState()钩子创建一个变量。

```
*const* [searchInput, setSearchInput] = useState("");
```

## 第五步

现在，用*名称*和*大陆*属性创建一个国家的常量数组

```
*const* [searchInput, setSearchInput] = useState("");const countries = [ { name: "Belgium", continent: "Europe" },
  { name: "India", continent: "Asia" },
  { name: "Bolivia", continent: "South America" },
  { name: "Ghana", continent: "Africa" },
  { name: "Japan", continent: "Asia" },
  { name: "Canada", continent: "North America" },
  { name: "New Zealand", continent: "Australasia" },
  { name: "Italy", continent: "Europe" },
  { name: "South Africa", continent: "Africa" },
  { name: "China", continent: "Asia" },
  { name: "Paraguay", continent: "South America" },
  { name: "Usa", continent: "North America" },
  { name: "France", continent: "Europe" },
  { name: "Botswana", continent: "Africa" },
  { name: "Spain", continent: "Europe" },
  { name: "Senegal", continent: "Africa" },
  { name: "Brazil", continent: "South America" },
  { name: "Denmark", continent: "Europe" },
  { name: "Mexico", continent: "South America" },
  { name: "Australia", continent: "Australasia" },
  { name: "Tanzania", continent: "Africa" },
  { name: "Bangladesh", continent: "Asia" },
  { name: "Portugal", continent: "Europe" },
  { name: "Pakistan", continent"Asia" },];
```

## **第六步**

创建一个处理函数来读取搜索栏中的变化。然后创建一个 if 语句，返回与搜索栏中输入的内容相匹配的国家。

```
*const* handleChange = (*e*) => {
  e.preventDefault();
  setSearchInput(e.target.value);
};if (searchInput.length > 0) {
    countries.filter((country) => {
    return country.name.match(searchInput);
});
}
```

## **第七步**

接下来，在用户将要输入的 searchBar 的 return 语句中创建一个 search 类型的输入。

```
<input
   *type*="text"
   *placeholder*="Search here"
   *onChange*={handleChange}
   *value*={searchInput} />
```

## **第 8 步**

最后，创建一个表格元素来显示国家的完整列表。它应该有两列。这是“姓名”列和“洲”列。

```
<div><input
   *type*="text"
   *placeholder*="Search here"
   *onChange*={handleChange}
   *value*={searchInput} /><table>
  <tr>
    <th>Country</th>
    <th>Continent</th>

  </tr>{countries.map((country, *index*) => { <tr>
    <td>{countries.name}</td>
    <td>{countries.continent}</td>

  </tr>})}
</table></div> 
```

最终的 ***searchBar.js*** 文件必须如下图所示。

```
import React, {useState} from 'react'

const searchBar = () => { *const* [searchInput, setSearchInput] = useState(""); const countries = [ { name: "Belgium", continent: "Europe" },
  { name: "India", continent: "Asia" },
  { name: "Bolivia", continent: "South America" },
  { name: "Ghana", continent: "Africa" },
  { name: "Japan", continent: "Asia" },
  { name: "Canada", continent: "North America" },
  { name: "New Zealand", continent: "Australasia" },
  { name: "Italy", continent: "Europe" },
  { name: "South Africa", continent: "Africa" },
  { name: "China", continent: "Asia" },
  { name: "Paraguay", continent: "South America" },
  { name: "Usa", continent: "North America" },
  { name: "France", continent: "Europe" },
  { name: "Botswana", continent: "Africa" },
  { name: "Spain", continent: "Europe" },
  { name: "Senegal", continent: "Africa" },
  { name: "Brazil", continent: "South America" },
  { name: "Denmark", continent: "Europe" },
  { name: "Mexico", continent: "South America" },
  { name: "Australia", continent: "Australasia" },
  { name: "Tanzania", continent: "Africa" },
  { name: "Bangladesh", continent: "Asia" },
  { name: "Portugal", continent: "Europe" },
  { name: "Pakistan", continent"Asia" },];*const* handleChange = (*e*) => {
  e.preventDefault();
  setSearchInput(e.target.value);
};if (searchInput.length > 0) {
    countries.filter((country) => {
    return country.name.match(searchInput);
});
}return <div><input
   *type*="search"
   *placeholder*="Search here"
   *onChange*={handleChange}
   *value*={searchInput} /><table>
  <tr>
    <th>Country</th>
    <th>Continent</th>  
  </tr>{countries.map((country, *index*) => {<div>
  <tr>
    <td>{country.name}</td>
    <td>{country.continent}</td>
  </tr>
</div>})}
</table></div> };export default searchBar;
```

## **第 9 步**

将 ***searchBar*** 组件导入到 ***app.js*** 文件中，并添加到返回语句 JSX 中，如下所示。

```
import React from 'react'
import './App.css'
import SearchBar from './components/searchBar'*function* App() {
  return (
     <div *classname*='App'>
       <SearchBar/>
     </div>
)}export default App
```

运行应用程序。

# 结论

现在我们有了。我希望你已经发现这是有用的。我会带着更多有趣的文章回来。感谢您的阅读。

*更多内容请看*[***plain English . io***](http://plainenglish.io)