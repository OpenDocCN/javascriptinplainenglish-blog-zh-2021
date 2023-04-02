# 函数式 JavaScript:编写简单的命令行游戏(第 5 部分)

> 原文：<https://javascript.plainenglish.io/functional-javascript-writing-a-simple-command-line-game-part-5-ac9b298d7ecd?source=collection_archive---------12----------------------->

![](img/1272a4d65e141b240b8ced108aea3bbc.png)

Photo by [Dan Asaki](https://unsplash.com/@danasaki?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

目前，我们已经到了旅程的终点。在这最后一部分，我们将快速查看迷宫代码。这里的计划不是深入细节，而是关注一些基本方面。首先，我们创建一个房间类型。

```
// room.js
const room = function( attrib ){

    attrib = attrib || {};
    const dv = (value,def ) => (typeof value === "undefined")?def:value;
    const _name = dv( attrib.name, "<lost>");
    const _msg = dv( attrib.msg, "");
    const _doors = dv( attrib.doors, {} );
    let _monster = dv( attrib.monster, null );
    let _item = dv( attrib.item, null );

    function name() {
        return _name;
    }
    function monster() {
        const m = _monster;
        _monster = null;
        return m;
    }
    function doors() {
        return _doors;
    }
    function message() {
        return _msg;
    }
    function item() {
        const i = _item;
        _item = null;
        return i;
    }
    return { name, monster, doors, item, message, isRoom : true };
}

module.exports = room;
```

到这个时候，图案应该感觉非常自然；我们已经创建了一个封装房间私有数据的对象，并且实现了一组助手方法。我们只希望冒险者和房间里的怪物战斗一次，所以怪物方法‘清空’了怪物。房间里的物品也是如此。

接下来，我们看看动作处理程序。

```
const actions = function( maze ) {
    const hits = [ "head", "arm", "leg" ]
    function hit() {
        const i = ***Math***.floor(***Math***.random() * hits.length);
        return hits[i];
    }

    function move(direction) {
        return function (room, player) {
            return _move(room, direction, player)
        }
    }

    function _move(room, direction, player) {
        const door = room.doors()[direction];
        if (!door) {
            ***console***.log("You walk and hit your " + hit() + " ouch!");
        } else if (typeof door == "object") {
            const itm = player.use( door.item);
            if ( itm ) {
                return maze[door.room];
            } else
            {
                player.stash( itm );
            }
            ***console***.log("You need the " + door.item + " to go that way");
        } else {
            ***console***.log( "you walk towards the " + maze[door].name())
            return maze[door];
        }
        return room;
    }

    function list(room, player) {
        const bag = player.getBag();
        if (bag.items().length) {
            ***console***.log("Your bag contains " + bag.items());
        } else {
            ***console***.log("You have nothing in your bag");
        }
        ***console***.log("You have a " + player.getWeapon().name() + " to defend with");
        ***console***.log("You have " + player.getHP() + " health left");
        return room;
    }

    function help(room) {
        ***console***.log("Type n,s,e,w,u,d,l");
        return room;
    }

    function quit(room, player) {
        ***console***.log("Goodbye...");
        ***process***.exit(0);
    }

    const command = {
        list: list,
        l: list,
        east: move("e"),
        e: move("e"),
        west: move("w"),
        w: move("w"),
        north: move("n"),
        n: move("n"),
        south: move("s"),
        s: move("s"),
        up: move("u"),
        u: move("u"),
        down: move("d"),
        d: move("d"),
        o: move("o"),
        open: move("open"),
        c: move("c"),
        close: move("close"),
        q: quit,
        quit: quit,
        "?": help,
        "help": help
    };
    function action( name ) {
        return command[name]
    }
    return { action };
}
module.exports = actions;
```

动作定义了冒险者可以发出的一组动词。现在，我们将动词限制为移动、列出、退出和帮助。移动是基于标准的北、南、东、西运动方式发生的。所以当我们在一个房间里时，我们可以在一面或多面墙上看到“门”。我们也用动作来让自己向上或向下。也许令人惊讶的是，我们也可以用一个动作来代表打开或关闭胸腔。从游戏代码来看，当你打开一个箱子时，你在箱子里；当你合上胸腔，你就离开了胸腔。

值得看一下 move 函数，因为这是一个闭包；调用 move( "e ")会返回一个关闭" e "的函数，并接受两个参数" room "和" player "。所有动作共享相同的函数签名。

```
function move(direction) {
    return function (room, player) {
        return _move(room, direction, player)
    }
}
```

位于 maze.js 中的是迷宫遍历逻辑的核心。我们还在这个文件中设置了迷宫和小怪。有很多机会可以重构这些代码。让我们看看迷宫中的第一个房间。

```
const maze = {
    1: room({ name: "The Entrance Room",
        msg: "There is an old rusty chest in the corner",
        doors: {
            n: 2,
            e: 3,
            w: 4,
            u: { item: "ladder", room: 6 },
            o: "chest1"
        }
    })
}
```

我们在地图/物体中定义迷宫。键 1 代表“房间 1”的数据。从门厅的“1 号房间”开始，你可以向东到 3 号房间，向北到 3 号房间，等等。如果你有物品“梯子”，那么你可以去 6 号房间。也可以开胸。我们还为房间提供了第二行描述。这个描述可以详细到你想要的程度；在这种情况下，它告诉我们，在角落里有一个生锈的箱子。

```
"chest1": room( {
    name: "Rusty chest",
    msg:"",
    item: ***weapons***.short_sword,
    doors: {
        c: 1
    }
}),
```

迷宫对象中的以下关键点描述了箱子内部的内容。只有一个出口，关闭箱子。这个出口让我们回到“1 号房间”如果我们想，我们可以让这个箱子有一个传送点！

```
"chest1": room( {
    name: "Rusty chest",
    msg:"",
    item: ***weapons***.short_sword,
    doors: {
        c: 1, d: 6
    }
}),
```

通过添加向下移动选项，我们可以跳到房间 6。这取决于迷宫的设计者。另一个值得注意的是这个箱子里有一把短剑。这个武器是至关重要的，因为在这个迷宫中的怪物没有任何挑衅的攻击。你不会想不带武器四处游荡的。当角色进入箱子时，剑被藏在他们的包里并装备好。我们总是装备冒险者拥有的最强大的武器。

我们关注的代码的最后一部分是主循环。我们使用 Node.js readline 模块作为我们的循环。该模块允许我们从控制台读取并显示提示，用户可以与该提示进行交互。每次用户键入命令时，我们都会将它传递给会话结束。正是这种封闭跟踪了迷宫中的位置。我们从迷宫中的第一个房间，1 号房间开始定位。

```
let where = maze[1];
let session = ( command ) => where = _run( where, player, command );
session( "l");
```

每次我们向会话传递命令时，我们都会更新“在哪里”。有时我们会呆在同一个地方，例如，如果我们给“l”列表。

从会话中调用的 _run 例程主要负责向用户打印出一条好消息，并处理房间的独特功能，比如物品和怪物。

```
function _run( room, player, command ) {
    const action = actions.action(command);
    if (!action) {
        ***console***.log("I do not know how to '" + command + "' type ? or help for help");
        return room;
    }
    room = action(room, player);
    ***console***.log("You are in " + room.name());
    ***console***.log(room.message());
    // Empty doors mark the end
    const doors = ***Object***.keys(room.doors());
    if (doors.length === 0) {***process***.exit(0);
    }
    ***console***.log("You see doors to the " + doors );
    let mob = room.monster();
    if (mob) {
        ***console***.log("There is a " + mob.name() + " in here!!!");
        ***console***.log("it starts to attack you");
        ***console***.log("you use your " + player.getWeapon().name() + " to attack it");
        // fight returns true if the first listed dies
        if (fight(player, mob)) {
            ***console***.log("you lost, goodbye!");
            ***process***.exit(0);
        }
    }
    const i = room.item()
    if (i != null) {
        player.stash(i);if (i.isWeapon && i.strength() > player.getWeapon().strength()) {
            player.use(i.name());
        }
    }
    player.levelUp();
    return room;
}
```

这就结束了。我已经把完整的工作代码推给了 GitHub。

[https://github.com/mdcfrancis/adventurejs](https://github.com/mdcfrancis/adventurejs)

请随意提交修复；很可能有一些角落的情况错过了。缺少一些测试，并且有可能重构代码。

我希望您喜欢这个系列，并感受一下在不使用大量第三方库的情况下，您可以在 JavaScript 中实现什么。我强烈鼓励使用功能风格作为封装行为的一种方式。您可以阅读我对此的介绍:

[](/functional-javascript-classes-without-the-class-keyword-6e2de50a3698) [## 函数式 JavaScript:没有“class”关键字的类

### 了解如何使用函数式 JavaScript 来定义类，而不使用 class 关键字。基于…中使用的风格

javascript.plainenglish.io](/functional-javascript-classes-without-the-class-keyword-6e2de50a3698) 

让我知道你的想法，如果这是人们会发现有帮助的事情，我很乐意将这段代码分解得更详细。

[](/functional-javascript-writing-a-simple-command-line-game-335ab9fcc005) [## 函数式 JavaScript:编写一个简单的命令行游戏(1)

### 使用 JavaScript 和功能对象模型，我们为 Node.js 创建了一个简单的命令行游戏的第一部分。

javascript.plainenglish.io](/functional-javascript-writing-a-simple-command-line-game-335ab9fcc005) 

[*更多内容参见*](http://plainenglish.io/)