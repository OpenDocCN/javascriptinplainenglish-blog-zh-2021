# NGXS 是什么，如何在 Angular 中使用？

> 原文：<https://javascript.plainenglish.io/what-is-ngxs-and-how-to-use-it-in-angular-f975f5cfac40?source=collection_archive---------5----------------------->

![](img/36e51c3fd89f9917bc768c8394ace74a.png)

Photo by [Mohammad Rahmani](https://unsplash.com/@afgprogrammer?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

> 任何现代的 web 应用程序都需要一种现代的方式来处理反应式编程的挑战。在本指南中，我们将看看 NGXS 如何帮助您实现这一点。

现在，您已经准备好了 web 应用程序，您开始觉得有一种方法可以更好地处理反应式编程问题。好消息是，有一种东西可以解决这个问题，那就是 NGXS。

但是，你可能想知道 NGXS 是什么。简单地说，它是一个库，使您的应用程序能够以一种可预测的方式拥有一个真实的来源。

因此，本教程的第一部分将介绍什么是 NGXS，第二部分将展示在角度状态管理时使用它所需的移动部件。

最后，我们将看看如何将 Angular NGXS 添加到您的 Angular 应用程序中，以及如何使用它来更新您的应用程序。

## NGXS 是什么？

如上所述，它是一个角度状态管理库。好吧，这是正确的，但它是什么？好吧，要理解它是什么，最好是理解是什么让它滴答作响，就像，什么是运动的部分。

定义 ngx 有三个核心部分:

*   状态。
*   模型。
*   行动。

嗯，我知道如果你使用过其他的状态管理库，比如 NgRx，你一定想知道为什么我们没有选择器和缩减器。简单地说，NGXS 比 NgRx 有更少的样板文件。

## NGXS 的活动部件。

因此，有了核心部分，接下来的事情是了解它们实际上是什么。

**状态**

是的，你猜对了，这定义了你的 web 应用程序的当前地位。它包含了应用程序可用的最新更新，因此也保持了用户界面的同步。

另一个**重要的**区别是**不像 NGXS** 那样，我们有单独的减速器用于创建下一个状态，而**有角度的 NGXS** ，下一个状态实际上是在状态本身内创建的！

好吧，这可能是一个很大的接受，但不要担心，我们将在底部看到一个例子。

**型号**

这只是你的商店看起来像什么的一个简单定义。

**动作**

嗯，似乎在 ngxs 和 ngrx 中，动作都是不变的特性。正如您可能已经猜到的那样，动作决定了应用程序中紧接着需要做什么**。**

当然，一次可能会发生多个动作，例如，您有 Websockets。现在，为了区分这些动作，每个动作都以一种独特的方式定义，正如您将在提供的示例中看到的那样。

## 所以现在剩下的就是如何使用 NGXS 了。

我们将使用一个假设的应用程序，例如从 spotify 这样的地方获取艺术家。然后我们的组件将完全由 Angular NGXS 更新，因此不再依赖于 **rxjs observables** 等。

**第一步**

我们将创建一个模型文件和一个接口文件。这些接口将定义我们的数据属性的外观。至于模型文件，我们将只有模型定义。

定义接口:

```
export interface IArtist {
  image: string;
  name: string;
  genres: Array;
  albums: Array;
  uuid: string;
}
```

定义我们的角度 NGXS 模型:

```
import { IArtist } from "./interfaces";

export interface ArtistsStateModel {
    searchResults: Array;
}
```

**第二步**

我们将创建一个动作文件，并添加一个获取艺术家的动作。

```
export namespace ArtistsActions {
    export class SearchForArtist {
        static readonly type = '[Artists] Search For Artist';
        constructor (
            public searchTerm: string
        ) {}
    }
}
```

所以，解释一下上面的代码:

```
export namespace ArtistsActions
```

在这里，我们命名空间这个动作文件，并包装我们所有的动作，所以我们只是作为一个单元导入命名空间的名称，而不是导入单个的动作。这减少了出错的可能性，并使代码看起来更整洁。

```
static readonly type
```

这一行将定义我们操作的名称。你可以把它想象成你希望应用程序如何识别你的动作。

这个名字可以是你想要的任何名字，但是最好是这样的:

```
'[Component calling the action] Name of the action'
```

因为这将更容易排除故障。

另一个重要部分是:

```
constructor (
    public searchTerm: string
) {}
```

嗯，你猜对了。这是要传递给操作的参数。在这种情况下，我们传递的是 searchTerm。但是如果您不需要这个 NGXS 操作来接收任何参数，那么它是可选的。

**第三步**

现在，我们定义我们的角度 NGXS 状态，像这样:

```
import { Injectable } from "@angular/core";
import { Action, State, StateContext, StateToken } from "@ngxs/store";
import { ArtistsActions } from "./actions";
import { ArtistsStateModel } from "./model";
import { produce } from 'immer';
import { ApiService } from "../services/api.services";
import { tap } from "rxjs/operators";

const ARTIST_STATE_TOKEN = new StateToken('artists');

@State({
    name: ARTIST_STATE_TOKEN,
    defaults: {
        searchResults: []
    }
})
@Injectable()
export class ArtistsState {
    constructor(
        private apiService: ApiService
    ) {}

    @Action(ArtistsActions.SearchForArtist)
    searchForArtist(ctx: StateContext, action: ArtistsActions.SearchForArtist) {
        return this.apiService.get('search', {q: action.searchTerm, type: 'artist'}).pipe(
            tap(r => ctx.setState(produce(draft => {
                draft.searchResults = r;
            })))
        )
    }
}
```

逐行破解这段代码:

```
const ARTIST_STATE_TOKEN = new StateToken('artists');
```

在这里，我们定义了如何在整体角度状态管理中识别整个应用状态的这个**片段**。 **StateToken** 接受的类型是状态的模型定义，在本例中是**artiststatemodel**，名称是状态的**片段**的字符串标识。

下一部分是这样的:

```
@State({
    name: ARTIST_STATE_TOKEN,
    defaults: {
        searchResults: []
    }
})
```

这只是简单地设置由我们的状态令牌标识的名称，以及初始状态(作为 **defaults** 传入)，它应该类似于模型定义。

```
@Injectable()
```

嗯，Angular NGXS 状态是一种服务。这就是为什么我们使用**@ injectible()**装饰器来定义它。

```
constructor(
    private apiService: ApiService
) {}
```

在这里，我们注入将要使用的服务，在我们的例子中，因为我们正在发出外部请求，所以我们添加了我们的 ApiService。

```
@Action(ArtistsActions.SearchForArtist)
```

还记得我们说过行动说明需要做什么吗，嗯，就是这样。这个 **@Action** 装饰器将接受一个它需要监听的动作参数，并在这样一个动作被**分派**时执行。

```
searchForArtist(ctx: StateContext, action: ArtistsActions.SearchForArtist) {
    return this.apiService.get('search', {q: action.searchTerm, type: 'artist'}).pipe(
        tap(r => ctx.setState(produce(draft => {
            draft.searchResults = r;
        })))
    )
}
```

所以，上面的方法是修饰类方法，它接受一个上下文(状态模型)和一个动作(修饰它的动作)。

请注意，我们正在将融入其中。这是因为我们需要调用 api 上的实际获取。

```
action.searchTerm
```

记住这段代码，我们在我们的动作中定义了它，现在我们将像这样得到它。

```
tap(r => ctx.setState(produce(draft => {
    draft.searchResults = r;
})))
```

这实际上是最重要的一点，因为这使得用新的结果更新状态成为可能。

我们有从 **immerjs** 导入的 **produce** 方法(这不在本教程范围内)。它的作用是可以更新当前状态的草稿版本，并返回它，这样**草稿的**更新的**属性**就可以映射到与之匹配的状态**属性**上，从而更新状态。这是因为直接更新 ngxs 状态是不可取的。

因此，您可以看到 **tap** 给我们的内容，我们现在将它设置为我们想要更新的状态的属性。

**第四步**

现在，让我们定义我们的组件:

```
import { Component } from '@angular/core';
import { IArtist } from "./interfaces";
import { ArtistsActions } from './actions';

@Component({
  moduleId: 'module.id',
  selector: 'lib-artists',
  templateUrl: 'artists.component.html',
  styleUrls: [
    'artists.component.scss'
  ]
})
export class ArtistsComponent {
  private searchResults$: Observable> = new Observable>();

  /**
   * 
   */
   public getSearchResults$(): Observable> {
    return this.searchResults$;
  }

  constructor(
    private store: Store
  ) {
    this.searchResults$ = this.store.select(state => state.artists.searchResults || of([]))
  }

  /**
   * 
   * @param searchTerm 
   */
  public emitSearchEvent(searchTerm: string): void {
    this.store.dispatch(new ArtistsActions.SearchForArtist(searchTerm));
  }
}
```

上面的大部分代码都是简单的 Angular，所以我们将重点放在与 Angular 状态管理相关的部分。

```
private searchResults$: Observable> = new Observable>();
```

这部分定义了我们可观察的搜索结果。结果将是一个艺术类型的列表。

```
/**
* 
*/
public getSearchResults$(): Observable> {
    return this.searchResults$;
}
```

这是一个 getter 方法，我们将在 html 中使用。

```
constructor(
    private store: Store
) {
    this.searchResults$ = this.store.select(state => state.artists.searchResults || of([]));
}
```

我们需要定义存储，以便我们可以使用它的方法。第一种方法是**。选择**方法，这将返回一个可观察到的最新搜索结果。注意，因为搜索结果可能是空的，所以我们使用操作符的 **RxJS 返回一个空数组的初始可观察值。**

```
/**
 * 
 * @param searchTerm 
 */
public emitSearchEvent(searchTerm: string): void {
  this.store.dispatch(new ArtistsActions.SearchForArtist(searchTerm));
}
```

这个方法将在用户搜索时监听，然后分派动作。

第五步

最后，在我们的搜索组件 html 文件中，我们将添加以下内容:

因此，在这里，我们使用一个异步管道从我们的 **getSearchResults$()** 方法中读取最新发出的值。

## 结论

如您所见，使用 NGXS 解决角度状态管理问题非常简单。

好了，现在就这样。

**快乐编码！**

> 有没有兴趣学习**国家管理**？在我的网站上查看类似的精彩文章:[沉迷于代码>状态管理](https://bingeoncode.com/category/state-management)