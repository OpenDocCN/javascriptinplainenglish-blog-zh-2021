# 5 个故事可以帮助你更好地理解 JavaScript 闭包

> 原文：<https://javascript.plainenglish.io/5-stories-that-may-help-you-to-understand-javascript-closures-better-14e5e5c992a8?source=collection_archive---------16----------------------->

## 这就是一些聪明的开发人员试图向一个 6 岁的孩子解释 JavaScript 闭包的方式！

![](img/38a8f4d63f6886a6d77c99b986e7c7da.png)

Photo by [PNG Design](https://unsplash.com/@_pngdesign?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/magic-box?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

## 这是传统的解释方式

> 一个**闭包**是一个函数的组合，该函数被捆绑在一起(被封装)并引用其周围的状态(**词法环境**)——Mozila 开发者网络

所以，这里涉及到两件事:

```
- A Function
- A Reference to that function's outer scope
```

这里有一小段代码可以解释闭包:

```
function makeFunc() {
 var name = 'Mozilla';
 function displayName() {
   console.log(name)
 } 
 return displayName;
}var myFunc = makeFunc();
myFunc() // Mozilla
```

> JavaScript 表单闭包中的函数。*闭包*是函数和声明该函数的词法环境的组合。这个环境由创建闭包时在作用域内的所有局部变量组成。

在这种情况下，`myFunc`是对运行`makeFunc`时创建的函数`displayName`实例的引用。`displayName`的实例维护一个对其词法环境的引用，变量`name`存在于该环境中。因此，当调用`myFunc`时，变量`name`仍然可用，并且`Mozilla`被传递给`Console.log()`。

## 很无聊，对吧？让我们听一些开发者试图讲述的关于 Javascript 闭包的故事。

> 如果不能简单的解释，说明你理解的不够好。——阿尔伯特·爱因斯坦

# 1.古代公主和她的**童话**

![](img/05a6e5f8b915fbd247ba22ad12578e6f.png)

Photo by [Raychan](https://unsplash.com/@wx1993?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

从前，有一位公主。

```
function princess() {
```

她生活在一个充满冒险的奇妙世界里。她遇到了她的白马王子，骑着独角兽环游了她的世界，与龙搏斗，遇到了会说话的动物，以及其他许多不可思议的事情。

```
var adventures = [];

    function princeCharming() { /* ... */ }

    var unicorn = { /* ... */ },
        dragons = [ /* ... */ ],
        squirrel = "Hello!";

    /* ... */
```

但是她总是不得不回到她无聊的家务活和成年人的世界。

```
return {
```

她会经常告诉他们她最近作为公主的惊人冒险。

```
story: function() {
            return adventures[adventures.length - 1];
        }
    };
}
```

但是他们只会看到一个小女孩...

```
var littleGirl = princess();
```

...讲述关于魔法和幻想的故事。

```
littleGirl.story();
```

即使大人们知道真正的公主，他们也永远不会相信独角兽或龙，因为他们永远看不到它们。大人们说他们只存在于小女孩的想象中。

但是我们知道真正的真相；那个肚子里有公主的小女孩。

让我们为雅各布·斯沃伍德 **给我们讲述这个故事鼓掌。**

# 2.皮诺曹历险记

《匹诺曹历险记》中匹诺曹被一条超大的狗鱼吞下的部分

![](img/26050f1a15a4daeca4f07fe2038e0e0d.png)

Photo by [Jametlene Reskp](https://unsplash.com/@reskp?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

```
var tellStoryOfPinocchio = function(original) {

  // Prepare for exciting things to happen
  var pinocchioFindsMisterGeppetto;
  var happyEnding;

  // The story starts where Pinocchio searches for his 'father'
  var pinocchio = {
    name: 'Pinocchio',
    location: 'in the sea',
    noseLength: 2
  };

  // Is it a dog... is it a fish...
  // The dogfish appears, however there is no such concept as the  belly
  // of the monster, there is just a monster...
  var terribleDogfish = {
    swallowWhole: function(snack) {
      // The swallowing of Pinocchio introduces a new environment (for the
      // things happening inside it)...
      // The BELLY closure... with all of its guts and attributes
      var mysteriousLightLocation = 'at Gepetto\'s ship';

      // Yes: in my version of the story the monsters mouth is directly
      // connected to its belly... This might explain the low ratings
      // I had for biology...
      var mouthLocation = 'in the monsters mouth and then outside';

      var puppet = snack;

      puppet.location = 'inside the belly';
      alert(snack.name + ' is swallowed by the terrible dogfish...');

      // Being inside the belly, Pinocchio can now experience new adventures inside it
      pinocchioFindsMisterGeppetto = function() {
        // The event of Pinocchio finding Mister Geppetto happens inside the
        // belly and so it makes sence that it refers to the things inside
        // the belly (closure) like the mysterious light and of course the
        // hero Pinocchio himself!
        alert(puppet.name + ' sees a mysterious light (also in the belly of the dogfish) in the distance and swims to it to find Mister Geppetto! He survived on ship supplies for two years after being swallowed himself. ');
        puppet.location = mysteriousLightLocation;

        alert(puppet.name + ' tells Mister Geppetto he missed him every single day! ');
        puppet.noseLength++;
      }

      happyEnding = function() {
        // The escape of Pinocchio and Mister Geppetto happens inside the belly:
        // it refers to Pinocchio and the mouth of the beast.
        alert('After finding Mister Gepetto, ' + puppet.name + ' and Mister Gepetto travel to the mouth of the monster.');
        alert('The monster sleeps with its mouth open above the surface of the water. They escape through its mouth. ');
        puppet.location = mouthLocation;
        if (original) {
          alert(puppet.name + ' is eventually hanged for his innumerable faults. ');
        } else {
          alert(puppet.name + ' is eventually turned into a real boy and they all lived happily ever after...');
        }
      }
    }
  }

  alert('Once upon a time...');
  alert('Fast forward to the moment that Pinocchio is searching for his \'father\'...');
  alert('Pinocchio is ' + pinocchio.location + '.');
  terribleDogfish.swallowWhole(pinocchio);
  alert('Pinocchio is ' + pinocchio.location + '.');
  pinocchioFindsMisterGeppetto();
  alert('Pinocchio is ' + pinocchio.location + '.');
  happyEnding();
  alert('Pinocchio is ' + pinocchio.location + '.');

  if (pinocchio.noseLength > 2)
    console.log('Hmmm... apparently a little white lie was told. ');
}

tellStoryOfPinocchio(false);
```

**让我们一起为** [**罗恩·戴克斯**](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work/33279345#33279345) **鼓掌。**

# 3.编码器先生和神奇棒球

![](img/919e822572e1648bee23eb9126d5a01e.png)

Photo by [Jose Francisco Morales](https://unsplash.com/@franciscomorales?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

想象一下，在你们镇上有一个非常大的公园，你看到一个叫编码器先生的魔术师在公园的不同角落开始玩棒球游戏，用的是他的魔杖，叫做 JavaScript。

自然，每场棒球比赛都有完全相同的规则，而且每场比赛都有自己的记分牌。

很自然，一场棒球比赛的分数和其他比赛的分数是完全分开的。

结束是编码器先生保持他所有神奇的棒球比赛得分分开的一种特殊方式。

**感谢** [**b_dev**](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work/24944994#24944994)

# 4.一个小孩和他们的家

![](img/00b703c829f748474341c80cea8154ea.png)

Photo by [Anita Jankovic](https://unsplash.com/@dslr_newb?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你知道成年人怎么能拥有一栋房子，他们称之为家？当一个妈妈有了一个孩子，这个孩子并不真正拥有任何东西，对吗？但是孩子的父母是有房子的，所以每当有人问孩子“你家在哪里？”，他/她可以回答，“那个房子！”，并指向他们父母的房子。“封闭”是孩子总是(即使在国外)能够说他们有一个家的能力，即使实际上是父母拥有房子。

**又一轮掌声送给** [**马格纳**](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work/21839381#21839381) **。**

# 5.丹和 Xbox

![](img/d0bbab12038680f1fc5a05be36a7682d.png)

Photo by [Louis-Philippe Poitras](https://unsplash.com/@lppoitras?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

你要举办一个通宵派对，你邀请了丹。你告诉丹带一个 Xbox 控制器。

丹邀请保罗。丹让保罗带一个控制器来。多少控制者被带到聚会？

```
function sleepOver(howManyControllersToBring) {var numberOfDansControllers = howManyControllersToBring;return function danInvitedPaul(numberOfPaulsControllers) 
 { var totalControllers = numberOfDansControllers +  numberOfPaulsControllers;
  return totalControllers;
 }}
var howManyControllersToBring = 1;
var inviteDan = sleepOver(howManyControllersToBring);// The only reason Paul was invited is because Dan was invited.
// So we set Paul's invitation = Dan's invitation.
var danInvitedPaul = inviteDan(howManyControllersToBring);console.log("There were " + danInvitedPaul + " controllers brought to the party.");
```

**拜**[**stews hack**](https://stackoverflow.com/questions/111102/how-do-javascript-closures-work/6756814#6756814)**所赐。**

编码快乐，感谢阅读！

*更多内容请看*[***plain English . io***](http://plainenglish.io/)