# 提高 JavaScript 可读性的 10 个技巧

> 原文：<https://javascript.plainenglish.io/10-tips-to-improve-readability-in-javascript-382eb287437?source=collection_archive---------2----------------------->

![](img/aa663d9ddc62a6457678daae400721b3.png)

# 1.日志级别和语义方法

📚[控制台文档](https://nodejs.org/api/console.html#console_console_log_data_args)

```
console.log("hello world")
console.warn("this is a warning")
console.error("this is an error")
console.info("this is info")
console.debug("this is debug")
console.trace("show trace")
```

如果您尝试`console.warn`，您将获得跟踪，这意味着调试代码更容易。

你自己试试其他的主机功能吧。

⚠️原始代码

```
console.log("Error: API key should not be empty")
```

👉重构

```
console.error("Error: API key should not be empty")
```

# 2.避免布尔变量的负数名称

很难读懂双重否定

已启动🤜 🤛isNotStarted

⚠️原始代码

```
const isInvalidApiKey = apiKey === nullif (isInvalidApiKey) {}
```

👉重构

```
const isValidApiKey = apiKey != nullif (!isValidApiKey) {}
```

# 3.避免标志参数

直到您必须阅读函数声明时，您才知道标志参数的用途。

⚠️原始代码

```
renderResult(true)function renderResult(isAuthenticated) {
    if (isAuthenticated) {
       return <p>App</p>
    } else {
        return <p>Please login</p>
    }}
```

👉使用对象参数

```
renderResult({isAuthenticated: true})function renderResult({isAuthenticated}) {
    if (isAuthenticated) {
        return <p>App</p>
    } else {
        return <p>Please login</p>
    }}
```

👉使用两种功能

```
function renderAuthenticatedApp() {
    return <p>App</p>
}function renderUnAuthenticatedApp() {
    return <p>Please login</p>
}isAuthenticated ? renderAuthenticatedApp() : renderUnAuthenticatedApp()
```

# 4.使用保护条款

筑巢地狱

🐨让我们的代码很快失败
🐨自然流动

⚠️原始代码

```
if (statusCode === 200) {
    // success
} else {
    if (statusCode === 500) {
        // Internal Server Error
    } else if (statusCode === 400) {
        // Not Found
    } else {
        // Other error
    }
}
```

👉重构

```
if (statusCode === 500) {
    // Internal Server Error
}if (statusCode === 400) {
    // Not Found
}if (statusCode !== 200) {
    // Other error
}// success
```

# 5.使代码不言自明

*   容易理解
*   可重复使用的
*   一个长的描述性名称比一个长的注释更好

```
// verify that user has added a credit card
function verify(user) {}function verifyThatUserHasAddedCreditCard(user) {}
```

⚠️原始代码

```
if (country !== 'finland' &&
    country !== 'germany' &&
    country !== 'vietnam' &&
    country !== 'russia' &&
    type !== '💣'
) {
    return Promise.reject('Not available')
}
```

👉重构

```
const isInAvailableCountries = (
    country === 'finland' ||
    country === 'germany' ||
    country === 'vietnam' ||
    country === 'russia'
)const hasBoom = type === '💣'if (!isInAvailableCountries || hasBoom) {
    return Promise.reject('Not available')
}
```

🎁较好的

```
const availableCountries = ['finland', 'germany', 'vietnam', 'russia']
const isInAvailableCountries = availableCountries.includes(country)const hasBoom = type === '💣'if (!isInAvailableCountries || hasBoom) {
    return Promise.reject('Not available')
}
```

# 6.让不可能的状态变得不可能

*   容易理解
*   防止大量的错误

📚[停止使用 isLoading 布尔值](https://kentcdodds.com/blog/stop-using-isloading-booleans)

```
isLoading: true
isError: falseisLoading: false
isError: true// imposible states
isLoading: true
isError: trueconst LOADING_STATE = 'LOADING_STATE'
const ERROR_STATE = 'ERROR_STATE'const state = LOADING_STATE
```

⚠️原始代码

```
const [isLoading, setIsLoading] = React.useState(false)
const [error, setError] = React.useState(null)
const [coffee, setCoffee] = React.useState(null)function handleButtonClick() {
    setIsLoading(true)
    setError(null)
    setCoffee(null) getCoffee('cappuccino', 'small', 'finland', true).then(coffee => {
        setIsLoading(false)
        setError(null)
        setCoffee(coffee)
    }).catch(error => {
        setIsLoading(false)
        setError(error)
    })
}
```

👉重构

```
const state = {
    idle: 'idle',
    loading: 'loading',
    error: 'error',
    success: 'success',
}const [error, setError] = React.useState(null)
const [coffee, setCoffee] = React.useState(null)
const [status, setStatus] = React.useState(state.idle) function handleButtonClick() {
    setStatus(state.loading) getCoffee('cappuccino', 'small', 'finland', true).then(coffee => {
        setStatus(state.success)
        setCoffee(coffee)
    }).catch(error => {
        setStatus(state.error)
        setError(error)
    })
}
```

# 7.将对象用于长参数列表

*   参数顺序无关紧要
*   易于传递的可选参数

```
function getBox(type, size, price, color) {}getBox('carry', undefined, 10, 'red')function getBox(options) {
    const {type, size, price, color} = options
}getBox({
    type: 'carry',
    price: 10,
    color: 'red'
})
```

⚠️原始代码

```
export function getCoffee(type, size, country, hasIce) {getCoffee('cappuccino', 'small', 'finland', true)
}
```

👉重构

```
function getCoffee(options) {
    const {type, size, country, hasIce} = options
}getCoffee({
    type: 'cappuccino',
    size: 'small',
    country: 'finland',
    hasIce: true
})
```

# 8.使用 Object.assign 作为默认值

```
function getBox(options) { options.type = options.type || 'carry'
    options.size = options.size || 'small'
    options.price = options.price || 10
    options.color = options.color || 'red' const {type, size, price, color} = options
}function getBox(customOptions) { const defaults = {
        type: 'carry',
        size: 'small',
        price: 10,
        color: 'red',
    } const options = Object.assign(defaults, customOptions) const {type, size, price, color} = options
}
```

⚠️原始代码

```
export function getCoffee(type, size, country, hasIce) { type = type || 'cappuccino'
    size = size || 'small'
    country = country || 'finland'
    hasIce = hasIce || false
}
```

👉重构

```
function getCoffee(customOptions) {
    const defaultOptions = {
        type: 'cappuccino',
        size: 'small',
        country: 'finland',
        hasIce: false
    } const options = Object.assign(defaultOptions, customOptions)
}function getCoffee(options = {}) {
    const {
        type = 'cappuccino',
        size = 'small',
        country = 'finland',
        hasIce = false
    } = options
}function getCoffee({
    type = 'cappuccino', 
    size = 'small',
    country = 'finland',
    hasIce = false
} = {}) {
}
```

# 9.用对象文字替换 switch 语句

老实说，我也喜欢 switch，但我不知道什么时候应该使用 switch 语句而不是对象文字。我的感觉只是告诉我该走哪一条。

看看这两个博客，决定哪一个更适合你:

📚[用对象文字替换 switch 语句](https://ultimatecourses.com/blog/deprecating-the-switch-statement-for-object-literals#object-literal-fall-through)
📚[开关正常](https://dev.to/macsikora/switch-is-ok-336l)

```
const handleSaveCalculation = ({key}) => {
    switch (key) {
        case 'save-copy': {
            saveCopy()
            break
        }
        case 'override': {
            override()
            break
        }
        default:
            throw Error('Unknown action')
    }
}handleSaveCalculation({key: 'save-copy'})const handleSaveCalculation = ({key}) => {
    const actions = {
        'save-copy': saveCopy,
        'override': override,
        'default': () => throw Error('Unknown action')
    } const action = key in actions ? actions[key] : actions['default']
    return action();
}handleSaveCalculation({key: 'save-copy'})
```

⚠️原始代码

```
let drink
switch(type) {
    case 'cappuccino':
        drink = 'Cappuccino';
        break;
    case 'flatWhite':
        drink = 'Flat White';
        break;
    case 'espresso':
        drink = 'Espresso';
        break;
    default:
        drink = 'Unknown drink';
}
```

👉重构

```
const menu = {
    'cappuccino': 'Cappuccino',
    'flatWhite': 'Flat White',
    'espresso': 'Espresso',
    'default': 'Unknown drink'
}const drink = menu[type] || menu['default']
```

# 10.避免草率的抽象

> 我不知道如何创建一个好的抽象，但我已经创建了许多糟糕的抽象。

比起错误的抽象，我更喜欢复制。

“没有什么是免费的。代码牺牲了改变需求以减少重复的能力，这不是一个好的交易。”— *丹·阿布拉莫夫*

📚 [AHA 编程](https://kentcdodds.com/blog/aha-programming)

📚[再见，干净的代码](https://overreacted.io/goodbye-clean-code/)

⚠️ [我的反应样本](https://github.com/vinhlee95/awesome-react-typescript-boilerplate)

下面的代码用于获取订单，我使用 Redux 进行状态管理。真是个样板！让我们做一个我以后会后悔的抽象。

获取订单:

```
// Action Type
const FETCH_ORDERS_START = "FETCH_ORDERS_START";
const FETCH_ORDERS_SUCCESS = "FETCH_ORDERS_SUCCESS";
const FETCH_ORDERS_FAILED = "FETCH_ORDERS_FAILED";// Action
export const fetchOrder = (token) => {
    return dispatch => {
        dispatch(fetchOrdersStart);
        axios.get('/orders.json?auth=' + token).then(res => {
            dispatch(fetchOrdersSuccess(res));
        }).catch(err => {
            dispatch(fetchOrdersFailed(err));
        });
    };}export const fetchOrdersSuccess = (orders) => {
    return {
        type: FETCH_ORDERS_SUCCESS,
        orders: orders,
    };
};export const fetchOrdersFailed = (error) => {
    return {
        type: FETCH_ORDERS_FAILED,
        error: error,
    };
};export const fetchOrdersStart = () => {
    return {
        type: FETCH_ORDERS_START,
    };
}
```

👉️ [抽象](https://github.com/vinhlee95/awesome-react-typescript-boilerplate/blob/develop/src/modules/commons/moduleActions.ts)

我敢说你不用点击链接就能理解抽象代码。即使在链接之后，您也必须阅读所有代码来理解这个抽象概念。

如果您想深入了解这一点，请查看 [AHA 编程](https://kentcdodds.com/blog/aha-programming)和[再见，干净代码](https://overreacted.io/goodbye-clean-code/)

```
// Action
const moduleName = 'order'
const path = '/order'const {moduleActionTypes, moduleActions} = useModuleActions(moduleName, path)function fetchOrder() {
    moduleActionTypes.getModel()    
}function updateOrder(data) {
    moduleActionTypes.updateModel(data)
}
```

# 资源

[Github](https://github.com/HuyAms/ReadabilityPresentation)

**感谢您的阅读！**

*我很想听听你的想法和反馈。请在下面自由发表评论！*

# ✍️写的

**虎符**🔥 🎩 ♥️ ♠️ ♦️ ♣️ 🤓

*软件开发人员|魔术爱好者*

# 在以下时间说“你好”:

✅ [Github](https://github.com/HuyAms)

✅ [领英](https://www.linkedin.com/in/huy-trinh-dinh-253534131/)

✅ [中](https://medium.com/@trnhnhhuy)

✅ [德夫托](https://dev.to/dinhhuyams)

*更内容见于* [*中*](http://plainenglish.io/)