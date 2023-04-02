# 语音识别:它是如何工作的？

> 原文：<https://javascript.plainenglish.io/speech-recognition-how-does-it-work-7e275be6b076?source=collection_archive---------20----------------------->

![](img/ed6d669559fa2bc927f9f13d5a11c76e.png)

Photo by [Christina Morillo](https://www.pexels.com/@divinetechygirl?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/person-looking-at-phone-and-at-macbook-pro-1181244/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

“嘿，Siri，今天天气怎么样？”

在 2021 年，我认为可以有把握地假设，每个人都已经与一些使用语音/声音识别的设备进行了交互。虽然还不完美，但语音技术已经成为我们发展中的科技世界的一种规范。作为许多语音识别程序的狂热用户，如 Siri、Alexa、Cortana 和 Google Translate，我们经常认为这些程序的复杂性是理所当然的，我们只是希望它们能够工作。但是，你有没有想过机器实际上是如何理解人类语言的，或者至少在这个过程中会发生什么？

在本文中，我将讨论语音识别工作原理的一般概念。我还将简要介绍计算语言学中研究的一些概念，以及更具体地与自然语言处理(NLP)相关的概念。

# 波动到二进制

你听到的每一个声音都是空气中粒子振动的结果。当有人说话时，我们听到的声音没有什么不同。口语是我们通过迫使和限制空气通过我们的嘴、舌头和喉咙形成的不同形状而产生的声波(粒子的振动)的直接效果。

使用语音识别的设备能够拾取我们创造的声音，以及我们周围的声音，但我们稍后会谈到这一点。这些设备拾取声波/频率，并将它们从模拟声音转换成数字声音。[模拟声音代表波的频率，而数字声音是接近我们所听到的二进制代码。](https://www.recordingconnection.com/reference-library/recording-education/analog-digital-whats-the-difference/#:~:text=When%20we%20capture%20that%20sound,we're%20recording%20in%20digital.)

一旦声音或口语被转换成数字声音，它们可以被进一步分析，通常通过[神经网络](https://www.ibm.com/cloud/learn/neural-networks)使用云处理。

# 音素

每种语言都由音素组成，音素是构成语言的基本或最小的声音单位。每个音素都有一个独特的频率，可以被绘制出来，并在[声谱图](https://en.wikipedia.org/wiki/Spectrogram#:~:text=A%20spectrogram%20is%20a%20visual,they%20may%20be%20called%20waterfalls.)上直观地观察到。

神经网络以及其他算法，如[隐马尔可夫模型](https://web.stanford.edu/~jurafsky/slp3/A.pdf)负责将数字声音转化为可识别的音素。由于人类语音的不一致性，这通常需要大量的数据。神经网络系统不断学习和适应人类语音的变化，如口音、音高和速度。

一旦系统识别并分析了某人说出一个句子时产生的音素，下一步就是识别单词。

![](img/b2e1872b610e1489863213926063a78e.png)

Photo by [Pixabay](https://www.pexels.com/@pixabay?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels) from [Pexels](https://www.pexels.com/photo/time-lapse-photography-of-blue-lights-373543/?utm_content=attributionCopyText&utm_medium=referral&utm_source=pexels)

# 自然语言处理

该设备在神经网络和其他数学算法的帮助下，成功识别出音素后，自然语言处理开始发挥作用。

通过使用 NLP 和语言模型，音素被放在一起以识别可能的单词。语言模型和统计分析允许设备预测哪些单词是有意义的。使用一种语言的[音系](https://all-about-linguistics.group.shef.ac.uk/branches-of-linguistics/phonology/)与关于常见单词对和模式的统计数据配对，使设备能够从识别的音素中创建实际的单词可能性，而不是非单词。

一旦单词被创建，它们将与设备词典中的现有单词进行比较。如果该单词不存在，系统通常会在其预定义的词典中生成一个相似的单词。

但是设备是如何理解句子的意思的呢？

# 语法分析

现在设备已经识别出你所说的话。它必须进行句法分析以形成句子，然后分析意思。

句法分析，在计算机科学界也称为单词和句子标记，包括通过分析词序、词性和语法规则来检查短语是否有意义。为了做到这一点，创建了[解析树或语法树](https://en.wikipedia.org/wiki/Parse_tree)。

解析树是一种工具，用于系统地将句子分解成更小的短语，最终分解成单词。这有助于设备检查句子是否有效。如果这个句子是无效的，系统能够返回并检查产生的音素，然后重新评估哪些单词是组成的。然后重复这个过程，直到创建一个有效的句子。

这个过程确保系统正确理解说话者说出的句子的意思。诸如句法分析之类的语言学概念的使用允许该设备不会弄错同音字并且创建合乎语法的句子。

# 当前的缺点

如果你还没有注意到，你的背景声音越大，你的语音识别设备工作越不准确。这只是工程师们试图解决的关于语音识别的许多问题之一。

尽管这些技术已经取得了很大的进步，但仍有许多东西需要收获。语音技术领域中的一些主要问题包括过滤环境噪声、准确性/错误解释以及缺乏效率。

与人类不同，机器无法自动区分人类语音和背景噪音。这通常会导致设备无法破译实际所说的内容。

同样，很明显，这些设备并不总是准确地解释我们所说的话。这部分可能是由于不正确的音素解析，甚至是不准确的句法分析。语言学家仍在试图理解人类语言，仍然有许多未解之谜。因此，我们还没有开发出最精确的算法和工具来解析句子是有意义的。

同样，由于人类语言中有如此多的差异，我们的系统必须不断适应和学习。这经常会减慢这个过程，而使用传统的基于文本的方法通常会更快。人们一直在研究如何优化已经很快的流程，以提高效率和用户互动。

# 结论

语音识别是一个非常复杂的领域，涉及语言学家、软件工程师、数据工程师和人工智能工程师的多学科工作。尽管很复杂，语音识别以及其他语音技术已经取得了长足的进步，现在已经成为我们社会的一种规范。

虽然这些技术在很多方面帮助了我们，但仍有许多需要改进的地方。然而，这个领域正在不断发展，计算语言学研究和人工智能研究的出现比以往任何时候都多。科学家和工程师继续研究这些领域，并产生新的发展。

很难说这些技术在未来会是什么样的状态，但我相信我们都应该对未来感到兴奋！

# 有用的资源

*   [https://www.youtube.com/watch?v=6altVgTOf9s](https://www.youtube.com/watch?v=6altVgTOf9s)
*   [https://en . Wikipedia . org/wiki/Speech _ recognition #:~:text = Speech % 20 recognition % 20 is % 20 an % 20 跨学科，语言% 20 into % 20 text % 20 by % 20 computers](https://en.wikipedia.org/wiki/Speech_recognition#:~:text=Speech%20recognition%20is%20an%20interdisciplinary,language%20into%20text%20by%20computers)。
*   【https://www.explainthatstuff.com/voicerecognition.html 
*   [https://www.youtube.com/watch?v=iNbOOgXjnzE](https://www.youtube.com/watch?v=iNbOOgXjnzE)

*更多内容尽在*[plain English . io](http://plainenglish.io/)