# 如何在 React 中创建五星评级系统

> 原文：<https://javascript.plainenglish.io/react-5-star-rating-system-4fa81b71cac9?source=collection_archive---------2----------------------->

为用户评论建立一个评级系统。

![](img/d29b595165b81ab7ea28447eedb462b1.png)

photo credit: [pngall.com](http://www.pngall.com/5-star-rating-png)

## 说来容易做起来难

科技产品公司真的很看重用户体验。了解可以做出哪些改进来取悦消费者的最佳方式是收集反馈。星级系统是一个美丽的东西，因为它为用户提供了一个简单快捷的方式来传达他们对我们的网站、应用程序或产品的整体体验有多满意。

虽然这些可以在电子商务网站上看到，审查应用程序，等等，但不要让你的熟悉程度欺骗你认为它很容易创建和使用。负责实现可靠评级系统的开发人员面临着一些挑战。

也就是说，这是加深您对 React 中的条件呈现和状态的理解的一个很好的实践。在这个过程中，我们可以学到很多宝贵的经验。

## 分解它

第一步是真正了解我们需要什么来达到我们的最终目标。以下是我们获得最终结果所需的交付件:

1.渲染 5 颗星。
2。当用户悬停在星星上时，填充该星星。
3。当一颗星星被填满时，确保它之前的所有星星也被填满。
4。如果点击一个填充的星星，它会变成空的。

获得这些可交付成果的伪代码可能如下所示:

1.  应用程序呈现一个带有星级属性的分级系统组件。
2.  分级系统为用户返回一个标题和说明，以及一个名为 Stars 的组件，该组件接收 star count 属性。
3.  Stars 将当前评级保持为该州的一个数字。
4.  Stars 从其 star count 属性渲染正确的星星数。
5.  每颗星都需要一个属性来反映它的位置，这样我们就知道通过比较它的位置和当前的等级来呈现一颗填充的或空的星。
6.  最后，为了更改评级，我们需要添加一些当用户悬停或点击星星时触发的功能。

## 出发点

当面临挑战时，我喜欢做的第一件事是先从最简单的部分开始，然后在浏览器上显示一些东西。因此，让我们首先创建所需的组件，并检查它们是否呈现在页面上。

```
import React, {Component} from 'react';
import EmptyStar from './assets/empty-star.svg';
import FilledStar from './assets/filled-star.svg';
import './styles.css'; class Stars extends Component {
render(){
  return(
    [...Array(this.props.starCount).keys()].map((index) => {
     return (<img src={EmptyStar} alt={"empty star"} />)
     })
    )
  }
}const RatingSystem = (props) =>  {
 return (
   <div>
     <h1>5 star rating system</h1>
     <h2>Select a rating:</h2>
   <div className='rating'>
     <Stars starCount={props.starCount}/>
   </div>
   </div> 
 );
}export default function App() {
return (
  <div className="App">
    <RatingSystem starCount={5} />
  </div>
)
};
```

我们已经完成了第一个可交付成果。我们有应用程序渲染一个评级系统，返回一个星级组件。在 Stars 组件中，我们创建了一个长度等于 star count 属性的数组，并将一个空星星的图像映射到每个元素。目前我们只有空星，没有办法更新。

有条件地渲染一颗空的或填充的星星的一种方法是在星星的状态中存储一个数值等级，并添加到我们的映射方法中，以便在星星在线的位置小于或等于数值等级时渲染一颗填充的星星。让我们添加一些修改…

```
class Stars extends Component {
 constructor(props) {
   super(props);
   this.state = {currRating : 0}
 }render(){
  return(
  [...Array(this.props.starCount).keys()].map((index) => {
  return (
   <img
   data-value={index + 1}
   className="star"
   src={index + 1 <= this.state.currRating ? 
       FilledStar : EmptyStar}
   alt={index + 1 <= this.state.currRating ? 
       "filled star" : "empty star"} />)
   })
  )
 }
}
```

将当前等级初始化为零，我们开始时只有空星。将数据集值分配给恒星的索引加 1 将定义恒星在线的位置。我们可以通过确定星星的位置是大于、小于还是等于当前评级来有条件地分配图像源和替代文本。如果我们将当前评级指定为 2，我们的 map 方法将返回前 2 个元素作为填充星，其余的为空。

我们快到了！到目前为止，这看起来很棒，但我们需要为我们的用户的行动创造一种方式来更新当前的评级。让我们加入一些事件。

```
class Stars extends Component {
 constructor(props) {
   super(props);
   this.state = {currRating : 0}
   this.onHover = this.onHover.bind(this)
   this.onClick = this.onClick.bind(this) 
 }onHover(e) {
 if (e.target.className === 'star') {
  this.setRating(e.target.dataset.value)
 }
}onClick(e) {
 if (e.target.dataset.value === this.state.currRating){
  this.setRating(e.target.dataset.value - 1)
 }
}setRating(value) {
  this.setState({currRating : value})
}render(){
  return(
  [...Array(this.props.starCount).keys()].map((index) => {
  return (
   <img 
   onMouseOver={this.onHover}
   onClick={this.onClick}
   data-value={index + 1}
   className="star"   
   src={index + 1 <= this.state.currRating ? 
       FilledStar : EmptyStar}
   alt={index + 1 <= this.state.currRating ? 
       "filled star" : "empty star"} />)
   })
  )
 }
}
```

呜哇！我们的功能需求现在通过向每个被呈现的星形图标添加 onMouseOver 和 onClick 动作来满足。请注意，状态已经更新为将“this”绑定到这些操作调用的函数。别忘了这一步！

当用户将鼠标悬停在一颗星星上时，onHover 方法检查目标是否是一颗星星，然后将其位置传递给 setRating 方法，在该方法中，它成为当前评级的新赋值。如果当前评级高于星星的位置，单击星星会将评级降低一级。

## 复习和进一步练习

有几种不同的方法来实现这个特性。您可以尝试使用像 useState 这样的 React 挂钩，仅使用功能性组件来获得相同的结果。您也可以使用一个空的星形图像，并利用 CSS 类有条件地用颜色填充星形。一些评级系统也让用户选择提交部分填充的星。

我希望这篇教程对你有所帮助，并能激发你尝试自己的想法。请随意使用我下面的代码！

[codesandbox.io](https://codesandbox.io/embed/5-star-react-k4n0q?autoresize=1&fontsize=14&hidenavigation=1&theme=dark)

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)