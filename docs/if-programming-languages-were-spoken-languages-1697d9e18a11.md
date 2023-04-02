# 如果编程语言是口语

> 原文：<https://javascript.plainenglish.io/if-programming-languages-were-spoken-languages-1697d9e18a11?source=collection_archive---------4----------------------->

编程语言和普通语言之间蹩脚的比较。

![](img/d182d23867b8f25c72315eeb2be1d83e.png)

Photo by [Vladislav Klapin](https://unsplash.com/@lemonvlad?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

许多编程语言与常规口语有相似之处。其中一些有相似的结构、句法或语法；其他人则有类似的历史或社区。

这篇文章只是为了好玩，所以不要往心里去。

## Python 和英语

这两种语言拥有几乎相同的语法。它们都是非常灵活的语言，因为它们不需要任何关于形容词性别或可变数据类型的规范，而且词序有时并不重要。

甚至有短语字面上相同的情况:

```
if my_age is 10: print("You are 10!")
```

此外，两人都喜欢用破折号来连接单词，不管是传统的高破折号`-`还是下划线`_`。

此外，Python 和英语都是跨平台语言，因为它们可以在任何国家使用，几乎每个人都会说。由于他们的社区很大，所以有许多不同的方言和口音。当每个人都按照自己想要的方式编写时，很难写出标准化的、可维护的代码。

尽管它们很受欢迎，但它们通常不用于大型复杂系统，如哲学论文，对于哲学论文，更精确的语言，如德语或拉丁语是首选。

## C++和拉丁语

它们都是非常有能力的语言。根据[案](https://en.wikipedia.org/wiki/Latin_declension)，你可以非常详细地表达任何概念，并且通过调整几个字母就可以很好地控制句子的意思。

```
unsigned int a = pointer;
unsigned int a = *pointer;
```

他们有很多单词，你一辈子也学不完。此外，你可能需要一本字典(【cppreference.com】)来翻译一些表达。尽管如此，还是有少数人能不假思索地自然地说英语。

它经常在学校被教授，学生讨厌它。此外，他们中的大多数人不会在他们的职业生涯中使用它，除非他们不得不处理复杂的文本，如哲学或医学论文。

尽管事实上大多数人跳过学习它，但它的语法和概念是许多现代语言的基础，学习它的人能够理解他们从未见过的单词，仅仅因为他们的词源。

## Java 和德语

Java 和德语都是古老且特别结构化的语言。它的语法极其冗长，你无法在不重复自己的情况下将多个句子连接在一起。

```
ArrayList<String> list = new ArrayList<String>();
```

单词被连接在一起形成具有更具体意义的复杂词位。比如“科学”这个词，你在学校学习的科目，就是“Naturwissenschaft”(Natur+wissen+schaft)。Java 有一个类似的命名约定:

```
public ArrayList<String> getFirstNamesList() {/* ... */}
```

另一个相似之处是，由于语言严格的语法，即使简单的概念也通常用长类来表达。出于同样的原因，动词必须在主句中占据第二个位置，在关系从句中占据最后一个位置，就像 Java 程序员会对你大喊大叫，如果你写`static public void main`而不是`public static void main`。

## C#和法语

虽然它的灵感来自 Java/德语，但这种语言也来源于 c++/拉丁语。

由于各种原因，德国在历史上与法国有冲突。Java 和 C#也是如此，它们的开发者声称他们的语言比同类语言更好。

```
internal static HttpRequest CreateConnectRequest (Uri uri)
{
  var host = uri.DnsSafeHost;
  var port = uri.Port;
  var authority = String.Format ("{0}:{1}", host, port);
  var req = new HttpRequest ("CONNECT", authority);
  req.Headers["Host"] = port == 80 ? host : authority;
  return req;
}
```

法语/C#和德语/Java 有许多相似之处，因为它们是在同一个领域开发的，但是前者在设计上更简单，也不那么严格。尽管如此，Java 一直比 C#更受欢迎，就像德国在历史上和实际上都比法国更强大，在经济上更优越。

## 杀伤人员地雷和阿拉伯语

大多数人听不懂这种语言。 [APL](https://en.wikipedia.org/wiki/APL_(programming_language)) 和阿拉伯语都基于非常规字符集，与推荐的 ASCII 有很大不同。

```
∇ inst **MoveRequestData** REQ;data;m;i;lcp;props;args;mask
  :Access public shared
  inst._PageData←⎕NS''
  :If 0≠1↑⍴data←{⍵[⍋↑⍵[;1];]}REQ.Arguments⍪REQ.Data
    :If 0∊m←1,2≢/data[;1]
      data←(m/data[;1]),[1.5]m⊂data[;2]
    :EndIf
    i←{⍵/⍳⍴⍵}1=⊃∘⍴¨data[;2]
    data[i;2]←⊃¨data[i;2]
    :If 0≠⍴lcp←props←('_'≠1⊃¨props)/props←(inst.⎕NL-2)
    :AndIf 0≠1↑⍴args←(data[;1]∊lcp)⌿data
      args←(2⌈⍴args)⍴args
      i←lcp⍳args[;1]
      ⍎'inst.(',(⍕props[i]),')←args[;2]'
    :EndIf
    :If ∨/mask←'_'≠1⊃¨data[;1]
      args←mask⌿data
      :Trap 0
        args[;1]←inst._PageData PrepareJSONTargets args[;1]
        ⍎'inst._PageData.(',(⍕args[;1]),')←(⊃⍣(1=⍬⍴⍴args))args[;2]'
      :EndTrap
    :EndIf
  :EndIf
∇
```

只有使用它的内部人员才能阅读和编写它。此外，它只在世界的一部分被采用，因为它的实际用例相当有限。它通常用于数学计算，而阿拉伯人非常倾向于数学计算。

## JavaScript 和西班牙语

这种语言最初学起来很简单，但实际上很难掌握。只有少数人能够真正以适当的标准化方式使用它，并编写可维护的代码。

随着西班牙语在全球的普及，JavaScript 几乎已经渗透到了各个领域，从 web 和桌面应用程序到服务器端程序。因为它的社区很大，所以有许多不同的方言和浏览器规范。另外，每个人都有自己的编码风格，因为格式和方法的约定并不严格。

```
function acceptParams(str, index) {
  var parts = str.split(/ *; */);
  var ret = { value: parts[0], quality: 1, params: {}, originalIndex: index };
  for (var i = 1; i < parts.length; ++i) {
    var pms = parts[i].split(/ *= */);
    if ('q' === pms[0]) {
      ret.quality = parseFloat(pms[1]);
    } else {
      ret.params[pms[0]] = pms[1];
    }
  }
  return ret;
}
```

## 去用世界语

围棋和世界语都是非常年轻的语言。它们是专为效率而设计的。它们被设计成易于编写和理解，没有不寻常的字符集和来自现有流行语言的语法位。

```
func (u User) Allowed(url string, noModification bool) bool {
  var rule *Rule i := len(u.Rules) - 1 
  for i >= 0 {
    rule = u.Rules[i]
    isAllowed := rule.Allow && (noModification || rule.Modify)
    if rule.Regex {
      if rule.Regexp.MatchString(url) {
        return isAllowed
      }
    } else if strings.HasPrefix(url, rule.Path) {
      return isAllowed
    }
    i--
  }
  return noModification || u.Modify
}
```

由于 Go/Esperanto 的稳定性和良好的结构，它具有成为主流语言的不可思议的潜力。尽管如此，它从未真正起飞。

## 汇编和印欧语

它们似乎是每一种语言的根源。每本历史书都提到古代人口说印欧语，但实际上没有人知道它。汇编语言也是如此，它是所有现代编程的基础，每个人都知道它，但只有少数精英才能理解它。

```
shl ebx, 16
shl ecx, 8
mov bx, cx
shl edx, 2
mov bl, dl
and ebx, 0x00ffffff
or ebx, 0x80000000
mov eax, ebx
mov dx, PCI_CONFIG_ADDRESS
out dx, eax
pop rax
mov dx, PCI_CONFIG_DATA
out dx, eax
```

## 硬件编程和岩石刻字

它们是最早出现的书写形式。硬件编程和岩石铭文都将信息永久存储在物理材料中，无论是焊接在一起的特定晶体管配置还是岩石上雕刻的符号。

![](img/eb528644f6b519dc437fa06ca3da00c3.png)

Photo by [Valentin Petkov](https://unsplash.com/@thefreak1337?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

如今，这些历史片段被陈列在博物馆里供人们欣赏。尽管如此，仍然有艺术家出于热情在石头上雕刻或从零开始建造 8 位计算机。

我希望你喜欢这篇文章。我想知道你对这些比赛有什么看法，你还有其他好的比赛吗？

**感谢阅读！**

*更多内容看* [***说白了。报名参加我们的***](http://plainenglish.io/)***[***免费每周简讯这里***](http://newsletter.plainenglish.io/) *。****