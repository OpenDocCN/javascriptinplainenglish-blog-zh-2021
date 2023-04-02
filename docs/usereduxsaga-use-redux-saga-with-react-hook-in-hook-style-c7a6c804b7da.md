# useReduxSaga —使用 Redux-Saga 和钩子样式的 React 钩子

> 原文：<https://javascript.plainenglish.io/usereduxsaga-use-redux-saga-with-react-hook-in-hook-style-c7a6c804b7da?source=collection_archive---------8----------------------->

近年来，React Native 已经成为我最喜欢的移动开发框架。之前和 React-Redux 和 Redux-Saga 合作过一个项目。它影响了对传奇风格逻辑的处理。

在这几个月里，我用 React hooks 开始了另一个项目。Hooks API 很棒，它使得开发速度更快，并且简化了本地状态管理。

有了 React Redux 的 hook API(use selector、useDispatch、useStore)，将 Redux 集成到功能组件中不仅成为可能，而且变得简单。然而，减速器部分取决于开发人员，我们需要应用我们自己的风格。这就是为什么我写了这个库来使集成尽可能简单。

![](img/e78eca1f33e2209a92ea0a304c91b1e7.png)[](https://github.com/springwong/use-redux-saga) [## springwong/use-redux-saga

### react hook + react redux + saga 的扩展库 use-redux-saga 是一个集成 redux 及其侧…

github.com](https://github.com/springwong/use-redux-saga) 

# **设置**

useReduxSaga 必须与您的商店和 sagaMiddleware 集成

```
// Your reducers object before combinedReducers
const reducers = { todosReducer }// ...
// Store.js / ts
// init with createReducerManager
createReducerManager(reducers)const sagaMiddleware = createSagaMiddleware({
  sagaMonitor
});// code to run sagaMiddleware after store creation
sagaMiddleware.run(mySaga);
// setRunSaga with sagaMiddleware.run
setRunSaga(sagaMiddleware.run);
```

# **钩子**

# **useReduxReducer**

useReduxReducer 是一个钩子，用于在功能组件中创建一个 Reducer。在这种情况下，会创建一个 FC useEffect 生命周期绑定缩减器。而还原者会在 FC 被摧毁的时候被清除。

```
const cleanUpWhenDestroy = true;
const SomeScreen: FC = () => {
    const [state] = useReduxReducer((state = {
        value: 0
    }, action : any) => {
        switch (action.type) {
            case 'add':
                return { 
                    ...state,
                    value: state.value + 1
                };
        }
        return state;
    }, "UniqueKey", cleanUpWhenDestroy);
    return <Text>{state.value}</Text>
}// or, reducer from fileconst [state] = useReduxReducer(reducer, "UniqueKey", cleanUpWhenDestroy);
```

# **useReduxReducerLocal**

一个更简单的 useReduxReducer 版本，不需要密钥或清理。
提供 reducerKey 作为回报。如果您需要获得 store 的值，您可以从 state[reducerKey]中获得。xxx

```
const SomeScreen: FC = () => {
    const [state, reducerKey] = useReduxReducerLocal((state = {
        value: 0
    }, action : any) => {
        switch (action.type) {
            case 'add':
                return { 
                    ...state,
                    value: state.value + 1
                };
        }
        return state;
    });
    return <Text>{state.value}</Text>
}
```

# **使用佐贺**

本地 saga 实现，建议在跨屏幕/组件的情况下与 useContext Provider 一起使用。

```
const SomeScreen: FC = () => {
    const dispatch = useDispatch() useSaga(function*(params: any) {
        yield takeLatest("TEST_1", params.add)
    }, {
        add: function* () {
            yield delay(1000)
            yield put({
                type: 'provider_add'
            })
        },
    })
    return <Button onPress={() => { dispatch("TEST_1" }}>{"Click me"}</Button>
}// or, saga from saga file.
    useSaga(someSaga, {})
```

# **使用简单**

一个更简单的钩子变体。只需要一个发生器函数。提供了一个调度方法来调度创建的传奇。

```
const [dispatchPayload] = useSagaSimple(function* (payload: any) {
        yield delay(1000)
        yield put({
            type: 'provider_add'
        })
    });// ...
    return <View onPress={() => {
        dispatchPayload({
            value: 0
        })
    }} />
```

# **useRedux**

一个高级 redux 钩子提供了一组调用 reducers 的方法。

```
const [state, dispatches] = useRedux({
        value: 0
    }, {
        add: (state, payload) => {
            return {
                ...state,
                value: state.value + 1
            }
        },
        minus: (state, payload) => {
            return {
                ...state,
                value: state.value - 1
            }
        },
    });// ..., code hints available in TypeScript for dispatches
    return <View onPress={() => {
        dispatches.add({
            // maybe some value
        })
    }} ><Text>{state.value}</Text> </View>
```

# **限制(7 月 14 日编辑)**

如果与 useState 混淆，内联函数会有一些限制，应该注意这一点。

考虑下面功能组件中的实现。

```
const Component: FC = () => {
    const [index, setIndex] = useState(0);
    const [testCall] = useSagaSimple(function* (action) {
        // it always return initState = 0
        console.log(`index directly from : ${index}`)
        // value change by click
        console.log(`index pass from dispatch: ${action.useStateVariables.index}`)
    }, {index});
    return <TouchableOpacity onPress={
            () => {
                // add a for index from useState
                setIndex(index + 1);
                testCall({});
            }
        } style={style.button}>
            <Text>{"Press to trigger saga"}</Text>
    </TouchableOpacity>
}
```

索引没有因点击而改变，因为使用状态用不同的引用更新值。并且生成器函数将在第一次创建时创建这些值的快照。

为了获得更新后的值，useSagaSimple 允许对象通过 dispatch。

```
{index} as last parameter
get() with action.useStateVariables.index
```

然而，与普通 redux-saga 中的“yield select”不同，该值是在分派有效载荷时决定的。因此，如果该值在调用过程中被更改，该值将不会是最新的值。考虑常规实践中的 saga 文件，“yield select”是获取减速器值最新状态的更“saga”的方式。

另一个显示替代方案的示例:

```
const Component: FC = () => {
    const index = useRef(0);
    const [state, dispatches, reducerKey] = useRedux({value: 0}, {
        add: (state, payload) => { return { ...state, value: state.value + 1}},
    })
    const [testCall] = useSagaSimple(function* (action) {
        // it has most updated value when index.current change.
        console.log(`index directly from : ${index.current}`)
        // or, for any reducer
        const selectorValue = (yield select(state => {
            return state[reducerKey]['value']
        })) as number;
        // it has most updated value also from redux state
        console.log(`index directly from : ${selectorValue}`)
    }) return <TouchableOpacity onPress={
            () => {
                // add 1 for both ref and redux reducer
                dispatches.add({})
                index.current = index.current + 1;
                testCall({});
            }
        } style={style.button}>
            <Text>{"Press to trigger saga"}</Text>
    </TouchableOpacity>
}
```

useRef 会产生一致的值，因为它的 Ref 中有一个一致的 ref 对象。而 ref 本身在 FC 生命周期内是不变的。

yield select 是检索 reducer 值的正确而正常的方法，无论在 saga 文件或内联函数中使用什么都是安全的。

Github readme 将对每种情况和预期行为进行总结。

那是 useReduxSaga 库中 hooks API 的核心部分。更多主题请参考 Github 链接。希望你喜欢 React Hook 的 redux-saga！

[](https://github.com/springwong/use-redux-saga) [## springwong/use-redux-saga

### react hook + react redux + saga 的扩展库 use-redux-saga 是一个集成 redux 及其侧…

github.com](https://github.com/springwong/use-redux-saga) 

*更多内容看*[***plain English . io***](http://plainenglish.io/)