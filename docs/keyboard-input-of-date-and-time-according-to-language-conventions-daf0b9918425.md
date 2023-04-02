# 根据语言约定的日期和时间的键盘输入

> 原文：<https://javascript.plainenglish.io/keyboard-input-of-date-and-time-according-to-language-conventions-daf0b9918425?source=collection_archive---------9----------------------->

![](img/b5f572a7bf66c91571b812297d55d959.png)

一个用于日期键盘输入的 React 组件，它遵循浏览器语言的区域设置约定。

# 理由

在用于编辑的表单字段中，日期通常与一个*日期* *选取器*相关联。

日期和时间的选择由选择器的不同元素直观地驱动。

然后，所选择的日期将按照浏览器所用语言的约定显示在字段中。

但是，字段还应该提供键盘输入，以便那些由于各种原因而无法使用定点设备的用户可以使用它。

键盘输入还可以加速数据输入应用程序的表单填写。

日期应以每种语言的适当格式编辑。在下文中，JavaScript *日期*对象方法和国际化 API ( *Intl* )将用于实现提供该特性的字段。

在现场实施中，语言约定的正确应用有三个要点:

*   日期和时间的显示
*   对用户输入的解析
*   占位符的可视化(这对于告知用户可识别的语言约定非常重要)

# 假设

在处理日期和时间输入时，以下假设相当常见:

*   日期和时间部分以数字形式输入
*   日期部分由以下字符之一分隔: */* 、 *-* 或空白 *'*
*   日期和时间部分由空格分隔
*   时间成分由 *:* 分隔
*   年份总是用 4 位数表示

# 日期格式的可变性

根据之前的假设，格式可变性仅限于以下两个方面:

*   日期部分的位置:日/月/年，年/月/日或月/日/年
*   带/不带白天的时间(上午/下午)

# 日期构造函数

虽然很容易判断日期格式是将年份放在第一个位置还是最后一个位置，但是无法区分月份位置不同的两种格式(日/月/年和月/日/年)。

接受字符串作为输入的 date 构造函数只以一种方式解释日期“1/2/2022”:它是一月二日(不是二月一日)。
构造函数不能用于以日期作为第一部分的日期格式(DD/MM/YYYY)。

为了避免这个问题，解析器(见下文)将使用日期构造函数，它将所有日期部分的数值作为输入。

# 浏览器语言

该字段将按照浏览器采用的语言惯例来管理日期。

该语言由全局变量 *navigator.language* 定义。

要更改该值，只需修改浏览器的*语言*选项。

# 认识地区惯例

给定一种语言，使用 Intl API 很容易识别它的区域设置约定。

第一步是声明我们想要使用的日期和时间字符串的类型和部分。因此，根据前面的假设，我们对每个日期和时间部分的数值感兴趣:

```
**const** opt = {
  year: ‘numeric’,
  month: ‘numeric’,
  day: ‘numeric’,
  hour: ‘numeric’,
  minute: ‘numeric’,
  seconds: 'numeric'
}
```

使用这些选项，可以创建能够处理日期区域设置约定的 DateTimeFormat 对象:

```
**const** dateTimeFormat = 
  **new** **Intl**.**DateTimeFormat**(navigator.language, opt)
```

从 DateTimeFormat 对象中，我们可以检索任何日期字符串的日期和时间部分:

```
**const** dateParts = localeFormat.**formatToParts**(**new** **Date**(0)) ** ||
                     \/**[{type: ‘day’, value: ‘1’},
  {type: ‘literal’, value: ‘/’},
  {type: ‘month’, value: ‘1’},
  {type: ‘literal’, value: ‘/’},
  {type: ‘year’, value: ‘1970’},
  {type: ‘literal’, value: ‘, ‘},
  {type: ‘hour’, value: ‘01’},
  {type: ‘literal’, value: ‘:’},
  {type: ‘minute’, value: ‘00’}
]
```

注意，pc 时区是 UTC+1:00，所以小时是 01 而不是 00。

根据前面的向量，可以构建日期部分索引的映射(在这种情况下，我们对分隔符文字不感兴趣):

```
**const** partIndex = dateParts
  .**reduce**((acc, e, i) => ({ ...acc, [e.type]: i + 1 }), {}) **               ||
                       \/**{
  day: 1,
  month: 3,
  year: 5,
  hour: 7,
  minute: 9,
  literal:8
}
```

# 无效日期

日期字段的状态变量之一(见下文)是对应于输入字符串的日期对象。

当输入字符串不代表有效日期时，该状态变量的值应为*无效日期*。

要创建无效日期，只需用不代表日期的字符串调用构造函数即可。但是为了使意图明确，将使用下面的惯用表达:

```
new Date(undefined)
```

检测无效日期的测试非常简单:

```
**isNaN**(date.getTime())
```

或者用更简洁的方式来说:

```
**isNaN**(date)
```

# 显示日期和时间

这是开头列出的三项任务中最简单的一项:将日期转换成地区字符串完全由 *Date* 方法支持:

```
**export** **const** dateToLocaleString = (date) =>
  !date || **isNaN**(date.**getTime**())
    ? ''
    : date.**toLocaleDateString**(navigator.language) + ' ' +
       date.**toLocaleTimeString**(navigator.language)
```

# 日期占位符

使用之前定义的 *dateParts* 对象可以很容易地构建占位符字符串。

日期部分将显示为四位数字表示年份，两位数字表示月和日，而不考虑前导零上的区域设置指示。
相反，解析器(见下文)将只在分钟和秒钟内强制前导零。

```
**const** toUpper = (t, v) => t === 'literal'
  ? v
  : t[0] === 'y'
    ? 'YYYY'
    : t[0].**toUpperCase**() + t[0].**toUpperCase**()**const** DATE_FORMAT_NO_TIME = dateParts
  .**slice**(0, 5)
  .**reduce**((a, e) => a + toUpper(e.type, e.value), '')**const** DATE_FORMAT = DATE_FORMAT_NO_TIME +
  ( dateParts.**length** < 13
      ? ' HH:mm:ss'
      : ' hh:mm:ss A'
  )
```

# 区域日期和时间分析器

与更复杂的编译器/传输器一样，解析本地日期字符串并将其转换为日期对象是一个两步过程:

*   令牌识别
*   语义检查、翻译和语法错误管理

## 令牌识别

对于像这样的简单情况，使用一个简单的正则表达式就可以一举实现标记化。实际上，为了正确处理年份位置，使用了两种方法:

```
const dateReg = /^(\d?\d)([-/. ])(\d?\d)([-/. ])(\d{4})( +(\d?\d):(\d?\d)(:(\d?\d))?( +([AP]M))?)?$/const dateRegYearFirst = /^(\d{4})([-/. ])(\d?\d)([-/. ])(\d?\d)( +(\d?\d):(\d?\d)(:(\d?\d))?( +([AP]M))?)?$/
```

在日期部分，捕获组还包括分隔符，以便与 *partIndex* 对象保持一致(例如，匹配向量中的日组位于 *partIndex.day* 位置)。

秒的输入不是强制的`(:(\d?\d))?`。同样的技术可以用来使会议记录不是强制性的。

也可以省略整个时间子字符串(参见 reg exps 中由最后一个问号控制的可选组)。在这种情况下，解析器的*翻译*部分(简单地说就是*日期*构造器)会将时间设置为`00:00:00`。

## 语义检查、翻译和错误管理

使用对象 *partIndex* 和从区域设置字符串中提取的标记数组，很容易执行检查、翻译正确的字符串或管理错误。

完整的解析器如下所示:

第 4–6 行调用标记器。

第 9–17 行包含语义检查。第 14、16 行在分钟和秒时强制使用前导零(如果需要的话)。

第 19 行是错误管理:只返回一个无效的日期。

第 22–29 行将标记集翻译成解析器结果。

# 反应场

既然我们已经定义了管理区域设置字符串(包含数字元素)所需的日期特性，我们就可以在 react 组件中使用它们了。

## 状态变量

该组件使用三个状态变量:

*   输入元素中显示的字符串。输入元素将是一个受控组件，因此我们需要一个变量来存储输入值。
*   表示导出到父组件(通常是管理一组字段的表单组件)的字段值的 date 对象。
*   错误状态。它是显示来通知错误的字符串，也是字段错误状态的指示符:空字符串= >无错误；非空字符串= >字段出错

```
**const** [date, setDate] = **useState**(**new** **Date**(**undefined**))
**const** [value, setValue] = **useState**('')
**const** [error, setError] = **useState**('')
```

## 事件回调

字段的行为由两个回调定义:处理字段更改的回调和当字段失去焦点时调用的回调。

```
const changeDate = useCallback(
  (ev) => {
    const date = localeStringToDate(ev.target.value)
    setDate(date)
    setValue(ev.target.value)
    setError('')
    props.onChange(date)
  },
  [props.onChange]
)const validateDate = useCallback(
  () => {
    if (value && isNaN(date)) {
      setError('error')
    } else {
      setValue(dateToLocaleString(date))
      setError('')
    }
  },
 [date, value]
)
```

*changeDate* 回调清除错误字符串(只有当字段失去焦点时才会显示错误，如果有的话)。

*localestringdate*返回的 date 对象(有效或无效)用于设置内部状态变量，并传递给父组件的回调( *props.onChange)* 。

用户输入的任何内容都用来设置控制输入元素的内部状态变量。

如果日期无效， *validateDate* 回调会设置一条错误消息，否则它会用正确的区域设置字符串替换用户输入。

## 渲染组件

应将以下代码片段添加到前面的代码片段中，以创建功能性 React 组件:

```
const stateToColor = error
  ? 'red'
  : value && isNaN(date.getTime())
     ? 'orange'
     : 'black'return (
  <>
    <input
      type="text"
      placeholder={DATE_FORMAT}
      value={value}
      onChange={changeDate}
      onBlur={validateDate}
      style={{ borderColor: stateToColor,
               outlineColor: stateToColor}}
    />
    <div style={{ color: 'red' }}>{error}</div>
  </>
)
```

## 自己试试

你可以在[https://codesandbox.io/s/localedatefield-87cdh](https://codesandbox.io/s/localedatefield-87cdh)上试试前面的代码

# 当秒是无用的

很容易修改前面的代码，使区域设置字符串、占位符和解析器适应不同的需求。

例如，在秒不重要且不应使用的情况下(在内部，日期构造函数会将它们设置为 0)，应应用以下简单的更改:

*   区域设置字符串:考虑到两种不同的区域设置时间变量(带/不带时间段)，可以删除秒:

```
date.**toLocaleTimeString**(navigator.language)
 **.replace(/:00( [AP]M)?$/, '$1')**
```

*   占位符的修改很简单:

```
**const** DATE_FORMAT = DATE_FORMAT_NO_TIME +
  ( dateParts.**length** < 13
      ? ' HH:mm'
      : ' hh:mm A'
  )
```

*   应该修改解析器的语义检查，以测试*秒*令牌是否为*真值*:第 15、16 行应该替换为`dateToken[10]||`

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)*。在这里注册我们的* [*免费周报*](http://newsletter.plainenglish.io/) *。*