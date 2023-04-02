# 我如何使用 React Native Expo 构建我的第一个移动应用程序项目

> 原文：<https://javascript.plainenglish.io/how-i-built-my-first-mobile-app-project-using-react-native-expo-a17832aee612?source=collection_archive---------14----------------------->

## 使用 React Native Expo 的爱情百分比计算器应用程序

当您开始学习如何编码时，构建您的第一个应用程序可能会有点让人不知所措。我将分享我的第一次手机应用体验，以及我是如何创建它的。我在一个名为 Expo 的本地平台上开发了我的第一个移动应用程序。在这里，您可以创建一个在 IOS 和 Android 设备上都可以运行的移动应用程序。

![](img/88986aa524cc0a502530ec0745e8f04e.png)

Love percent Calculator: React native expo project

# 规划

当你开始学习一个新的事物时，你脑海中会有很多问题，比如学什么，从哪里学？我的承运人可以吗？结果会怎样？诸如此类。这里简单的建议是不要考虑结果，只要做你喜欢做的事情。它迟早会给你带来好处的。

当我们谈论 react-native 时，你可以从 Youtube、Coursera 或其他地方的免费课程中开始学习。我的建议是不要在课程初期花费太多。先看一眼课程。当你开始理解事情，并准备好跳远，那么你就可以继续进行付费课程。我开始从 YouTube 和博客上了解 react-native expo。

每次迈出简单的一步。但是不要停下来。众所周知，计划很重要，你必须计划好一切，以保持学习的速度。当我开始学习的时候，我开始做一些小的项目，比如制作一个简单的页眉、一张卡片和简单的 UI。你可以从教程开始学习，但不要从制作 Instagram 克隆之类的忙乱项目开始。这会影响你的学习。

制作一个日历，在日历上写下本周你必须完成的事情。这是最简单有效的坚持下去的方法。这里最有趣的部分是你每天都会学到新的东西。

# 起草工作

当我去年(2020 年)开始学习时，我犯了一个开发人员最常犯的错误。我没有起草代码和工作。不要这样。起草你的工作总是一个好习惯。让我假设我正在做一个新项目，我必须添加几行代码，这些代码是我在之前的项目中已经添加的。但那个项目不是我起草的。然后万一新项目出现错误，我还得在网上搜索错误和代码，这要花很多时间。很烦吧？你可以用 Github 来存储你的代码，这是开发者的天堂。您可以注释掉代码，也可以编写完整的代码文档。在早期阶段，可能会有点忙乱，但 6 个月后，或者更晚，你会看到结果。这是个好习惯。

如果你从第一天就开始起草你的作品，那么几个月后，你就有了从初学者到专业人士的全套内容。不仅仅是内容，更多的是学习和探索的东西。

开始新的生活你不兴奋吗？

# 关于我的项目(爱情百分比计算器)

爱情百分比计算器是一个简单的反应式应用程序，你可以用百分比来检查你和你的伴侣的关系。你必须输入你和你搭档的名字。当你点击计算按钮，它会显示你的债券有多强的百分比。你的债券的百分比越高。

我们正在使用一个 API 来构建这个项目。这里的链接是[这里的](https://rapidapi.com/ajith/api/love-calculator)。你必须做一个帐户，然后你会得到你的 API 密匙。

这是一个具有简单用户界面的单页应用程序。我为这个项目做了两个组件。一个是取输入数据，另一个是计算恋爱百分比。

**Result_love.js** 代码:

```
const Result_love = (prop) =>{if(prop.data == "Loading"){
        return <Text style={{fontSize:20, textAlign:'center'}}>Please Enter Your and Patner Name</Text>
    }
    if (prop.data.message) {
        return <Text style={{fontSize:20, textAlign:'center'}}>Somthing Went Wrong Please Try Again !</Text>
    } 
    else {   
    return(
        <View style={styles.component}>
                <Text style={styles.text} >{prop.data.percentage}%</Text>
                <Text style={styles.text} >{prop.data.result}</Text>
        </View>
    );
    }
}
```

**Input_love.js**

```
export default class App extends Component{
    state={
        male:'',
        female:'',
        result:'Loading'
    }
    submited(){
        fetch(`[https://love-calculator.p.rapidapi.com/getPercentage?fname=${this.state.male}&sname=${this.state.female}`,{](https://love-calculator.p.rapidapi.com/getPercentage?fname=${this.state.male}&sname=${this.state.female}`,{)
            headers:{
                "X-RapidAPI-Host":"love-calculator.p.rapidapi.com",
                "X-RapidAPI-Key":"ENTER_YOUR_API_KEY"
            }
        })
        .then(data=>data.json())
        .then(data2 => {
            this.setState({
                result:data2
            })
        })
    }
    render() {
        return(
            <View>
            <Appbar.Header>
                <Appbar.Content
                style={{alignItems:'center'}}
                title="Love % Calculator"
                />
            </Appbar.Header>
            <TextInput
                style={{margin:10}}
                label='Male'
                value={this.state.text}
                onChangeText={text => this.setState({ male:text })}
            />
            <TextInput
                style={{margin:10}}
                label='Female'
                value={this.state.text}
                onChangeText={text => this.setState({ female:text })}
            />
            <Button 
            icon="heart" 
            style={{margin:20}}
            mode="contained"
            onPress={this.submited.bind(this)} >
                Calculate
            </Button>
              <Result_love data={this.state.result} />
            </View>
        );
    }
}
```

在第 16 行用 API 键更新 **Input_love.js** 。在 **App.js** 中导入 **Input_love.js** 。您将看到您的项目在运行。虽然不是完整的代码。

[**Github 爱的代码百分比计算器**](https://github.com/imrohit007/Love-Percent-Calculator)

[**API 访问**](https://rapidapi.com/ajith/api/love-calculator)

答对了。你现在是开发商了。

不仅仅是代码。都是过程的问题。你经历的过程越多，你就会变得越强大。如果你打算开始学习母语，那就开始吧。不要想太多。从今天的一天开始，一个是非常大的一步。

感谢您的阅读。如果这篇文章听起来信息量很大，那就鼓掌直到你的手流血，并与你的社区分享。

你好，我叫 Rohit Kumar Thakur。我对自由职业者持开放态度。我构建了 **react 原生项目**，目前正在开发 **Python Django** 。随时联系我(**freelance.rohit7@gmail.com**)