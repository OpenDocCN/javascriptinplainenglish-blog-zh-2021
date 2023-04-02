# 用 p5.js 制作基于 Web 的 Flappy Bird 克隆体|第 3 部分

> 原文：<https://javascript.plainenglish.io/making-a-web-based-flappy-bird-clone-with-p5-js-part-3-32d4e96b8737?source=collection_archive---------16----------------------->

![](img/76f346c8e4d0ec32b885df850db8c5e6.png)

## 概述

这是 flappy 鸟克隆系列的第 3 部分。你可以在这里找到第一部分[，在这里](/how-to-make-a-web-based-flappy-bird-clone-with-p5-js-part-1-2913fde25c8a)找到第二部分[。在上一篇文章中，我讲述了如何将地面和管道对象添加到屏幕上，并使它们像 Flappy Bird 中那样移动。](/making-a-web-based-flappy-bird-clone-with-p5-js-part-2-c554254881b1)

## 鸟的物体

现在，我们将研究著名的扑翼鸟本身。同样，这个游戏中的鸟在整个游戏过程中保持水平方向不动，只在屏幕上上下移动。因此，鸟的位置更新将只在上下方向。游戏中的鸟也在拍打它的翅膀，因此我们需要找到一种机制来显示鸟的不同图像，使它看起来像鸟在拍打翅膀。

首先是鸟类图像的导入。在提供的起始代码中，我包含了 3 张鸟的图片，它们之间唯一的区别是翅膀的位置。为了在我们的代码中使用这些，我们将把图像预加载到一个数组中。

```
let BIRD_IMG;function preload() {
 BIRD_IMG = [
  loadImage(“assets/bird1.png”),
  loadImage(“assets/bird2.png”),
  loadImage(“assets/bird3.png”),
 ];
}
```

在我们深入到主要代码之前，让我们收集一下我们需要对这只鸟做些什么的想法。第一件事是让鸟能够跳跃。然后，每当这只鸟跳跃时，它就把自己向上旋转。当它向上旋转时，它扇动翅膀。当鸟不飞行时，它失去高度，指向地面下方。

## 该上来的一定要下来

```
function Bird() {
 this.SCALE = 1.75; this.y = WIN_HEIGHT / 2;
 this.x = WIN_WIDTH / 3;
 this.tilt = 0; //Physics variables
 this.tick_count = 0;
 this.gravity = 0.2;
 this.velocity = 0; //Jump velocity — NOT CONSTANT VELOCITY
 this.jump_height = this.y + 20; this.show = (i) => {
  imageMode(CENTER); 
  // NOTE: we change the image mode here to make sure the bird
  // rotates around it's center. 
  image(
   BIRD_IMG[i],
   0,
   0,
   this.SCALE * BIRD_IMG[i].width,
   this.SCALE * BIRD_IMG[i].height
  );
 }; this.update = () => {
  let displacement = this.getDisplacement();
  this.y -= displacement;
  this.updateTiltBasedOnDisplacement(displacement); //Limiting y position of the bird
  if (this.y > height — GROUND_HEIGHT) {

   this.y = height — GROUND_HEIGHT;
   displacement = 0;
  } if (this.y < -30) {
   this.y = -30;
   displacement = 0;
  } translate(this.x, this.y);
  rotate(this.tilt);
 } this.getDisplacement = () => {
  // Displacement means the amount of y position change every update
  this.tick_count += 1;
  //kinematics equation — initial velocity is 0 in most cases except
  //for jump event
  let displacement = this.velocity — 0.5 * this.gravity * this.tick_count ** 2;
  this.velocity -= this.gravity * this.tick_count; //Limiting velocity and displacement so fall rate doesn’t get 
 //too high
  if (this.velocity < 0) {
   this.velocity = 0;
  } if (displacement >= 5) {
   displacement = 5;
  } //Positive displacement means we are jumping
  if (displacement > 0) {
   displacement += 10;
  }
  return displacement;
 }; this.updateTiltBasedOnDisplacement = (displacement) => {
  if (displacement > 0 || this.y < this.jump_height) {
   // Negative means tilt up because counter-clockwise
   this.tilt = -25;
  } else {
   if (this.tilt < 76) {
    this.tilt += 20;
   }
   if (this.tilt > 90) {
    this.tilt = 90;
   }
  }
 }; this.hitGround = () => {
  return this.y > height — GROUND_HEIGHT — BIRD_IMG[0].width;
 };
}
```

这有很多代码，看起来可能有点复杂，但是让我们一点一点来。首先，让我们看看 getDisplacement 方法。这种方法用于获得鸟在每一个间隔经历的垂直距离。在鸟物体内部，我们有一个内部时钟，我们称之为 tick _ count——这是我们运动学方程中的时间变量，你可以通过位移计算看到。

在 update 方法中，我们获得了添加到鸟的 y 位置的位移。在这里，我们没有像处理地面和管道一样，在 x 和 y 位置显示鸟的图像。相反，我们使用 p5 提供的 translate 函数来移动这只鸟——老实说，我不太记得我为什么决定以这种方式编写代码，但了解一种不同的做事方式应该很有趣。updateTiltBasedOnDisplacement 也非常简单明了，但是如果你有任何问题，请在评论区提问。

## 什么东西落下来…有时会冒出来？

```
function Bird() {
 this.FLAP_INTERVAL = 2;
 ... this.update = () => {
  ...
  this.updateImage()
 };this.updateImage = () => {
  if (this.tilt > 80) {
   //If bird is pointing down, don’t animate flapping
   this.show(1);
  } else {
   if (this.img_count <= this.FLAP_INTERVAL) {
    this.show(0);
   } else if (this.img_count <= this.FLAP_INTERVAL * 2) {
    this.show(1);
   } else if (this.img_count <= this.FLAP_INTERVAL * 3) {
    this.show(2);
   } else if (this.img_count <= this.FLAP_INTERVAL * 4) {
    this.show(1);
   }
  }
 };this.updateImgCount = () => {
  //Updates to keep track of flapping mechanism
  this.img_count += 1;
  if (this.img_count > this.FLAP_INTERVAL * 4) {
   this.img_count = 0;
  }
 }; this.jump = () => {
  this.velocity = 10; //add positive velocity to simulate a jump
  this.tick_count = 0; //tick count reset
  this.jump_height = this.y;
 };this.getDisplacement = () => {
  ...
 };this.updateTiltBasedOnDisplacement = (displacement) => {
  ...
 };this.hitGround = () => {
  ...
 };
}
```

updateImage 方法包含“动画”逻辑，其中显示的图像取决于鸟的 image_count。FLAP_INTERVAL 是图像在特定位置停留多少帧的调整因子。FLAP_INTERVAL 为 2 意味着每幅图像显示 2 帧。这里的跳跃仅仅意味着给鸟增加一点正速度，getDisplacement 方法将处理位置更新。

```
// index.js...
let bird;function setup(){
 ... 
 bird = new Bird()
}function draw() {
 ...//don't need to show bird because show is called inside update
 bird.update(); 
}function keyPressed() {
 if (key === " ") {
  bird.jump();
 }
}function mouseClicked() {
 bird.jump()
}
```

最后，keyPressed 和 mouseClicked 是监听用户事件的 p5 函数。在这里，我想让小鸟在我点击空格键或鼠标时跳起来。正如您可能已经猜到的，keyPressed 和 mouseClicked 是检测用户事件的 p5 函数。

## 暂时就这样了

嗯，这是一个密集的，但我们现在在最后冲刺阶段。如果有任何问题，请在评论中告诉我。下一次，我们将添加一个简单的碰撞检测机制，并添加分数跟踪。以下是第四部分的链接。

*更多内容尽在*[***plain English . io***](http://plainenglish.io/)