# 你需要知道的关于 YAML 档案的一切

> 原文：<https://javascript.plainenglish.io/everything-you-need-to-know-about-yaml-files-5423358cc5c9?source=collection_archive---------3----------------------->

## 了解 YAML 让你比你的同行更有优势，因为它确实让编程和配置云计算资源更容易。

![](img/d4c28093e9ff311a0579c3143996c1e7.png)

Photo by [Ryan Tang](https://unsplash.com/@ryz0n?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/infrastructure-cloud?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)

当我在大学开始学习编码时，XML 在创建 web 服务和 SOAP 服务时非常流行。然而，学习或习惯 XML 并不容易。这导致了 JSON 的流行，它不仅易于掌握和学习，而且开始与 RESTful 服务很好地集成。于是，JSON 来了，征服了 XML，开始统治 web 开发。

然而，解释 JSON 可能具有挑战性，因为有时它不是那么容易被人理解。因此，我们需要类似 JSON 的东西，但人类可读。YAML 就这样诞生了。

# YAML 到底是什么？

YAML 是一种数据序列化语言，像 JSON 一样，允许以人类可读的格式存储信息。它是“ *YAML 不是标记语言*”的缩写(一个递归缩写)，强调 YAML 是用于数据而不是文档。它也可以与其他编程语言结合，并且被认为是 JSON 的超集。

> *YAML 是一种对所有编程语言都友好的数据序列化语言。*——*[官方文件](https://yaml.org/)*

*YAML 可以自我引用，支持复杂的数据类型，包含块文字，支持注释，等等。最近，YAML 被广泛用于基础设施即代码(IoC)系统，如 Helm Charts 或 Kubernetes，以构建配置文件或管理 DevOps 管道中的容器。*

# *YAML 语法*

*YAML 文件的结构是一个映射或列表。YAML 使用 Python 风格的缩进来显示嵌套。只允许空格，因此没有制表符。没有像大括号、方括号、结束标记或引号这样的标准格式符号。*

*的。yml 或者。yaml 扩展名用于 YAML 文件。*

# *语法说明*

*如前所述，YAML ( [*最新版本* )](https://yaml.org/) 是 JSON 的超集。因此，YAML 是由冒号和空格分隔的键值组合。*

*YAML 文件通常包含由冒号和空格表示的标量或变量。在句首使用#可以给出注释。*

*键总是一个字符串，但是值是一个标量，就像 Python、JavaScript 和 Perl 等编程语言一样。因此，它们可以是任何数据类型，如整数、字符串、浮点数等。如下图。*

```
***name: Vivek Naskar
designation: "Software Developer"
age: 29***
```

*可以使用|字符指定字符串，这样可以保持换行符不变。*

```
***cerifications: | 
  4 Google certifications 
  2 Best employee awards 
  Bachelors in Computer Science & Engineering***
```

*也可以使用>字符指定字符串作为段落打印。*

```
***mission: >
  My mission is
  to learn newer
  technologies***
```

*序列是数据结构，像列表或数组一样，在同一个键下存储许多值。*

```
***frameworks:
  - Spring Boot
  - Django
  - nodeJs***
```

*在上面的代码片段中，您还可以看到空格被用来以块格式组织文档。这是更容易阅读，但没有流动风格紧凑。*

# *YAML 的用途*

*当谈到为基础设施代码(IaC)开发配置文件时，YAML 是一个受欢迎的选择。这些文件为预期的云环境提供参数和配置。*

*Docker 使用被称为 Dockerfiles 的 YAML 文件，这些文件实质上是执行应用程序所需的一切的蓝图，如代码、运行时、工具、设置和库。*

*甚至自动化工具 [*Ansible*](https://www.ansible.com/) 也使用 YAML 来构建自动化流程。Ansible 用户用 YAML 代码编写 [*剧本*](https://www.redhat.com/en/topics/automation/what-is-an-ansible-playbook) 来自动化供应和部署云环境的繁琐操作。*

*YAML 文件也用于创建 Kubernetes 资源，如 pod、服务和部署。见鬼，你还可以使用 YAML 创建 [*机器学习管道。*](https://docs.microsoft.com/en-us/azure/machine-learning/reference-pipeline-yaml)*

# *最后*

*YAML 是一种强大的语言，它对学习非常重要。它的应用范围很广，而我们仅仅触及了皮毛。当然，你可以从他们的 [*官方文档页面阅读完整的文档和语法。*](https://yaml.org/spec/1.2.2/)*

*如果你喜欢读这篇文章，那么你可能也会发现下面的故事值得你花时间去读。*

*[](https://levelup.gitconnected.com/linux-turns-30-here-are-16-facts-that-make-linux-the-most-important-os-ever-created-5c854455d06c) [## Linux 30 岁了——这里有 16 个事实让 Linux 成为有史以来最重要的操作系统

### 今天，Linux 驱动了一切，包括智能手机、股票市场、潜水艇、电影《VFX》等等…

levelup.gitconnected.com](https://levelup.gitconnected.com/linux-turns-30-here-are-16-facts-that-make-linux-the-most-important-os-ever-created-5c854455d06c) [](/8-essential-web-development-tools-that-you-must-know-as-a-developer-cdbb7f6b59ce) [## 作为一名开发人员，你必须知道的 8 个基本的 Web 开发工具

### "很明显，我们拥有的最宝贵的资源是时间。"—史蒂夫·乔布斯

javascript.plainenglish.io](/8-essential-web-development-tools-that-you-must-know-as-a-developer-cdbb7f6b59ce) 

*如果你喜欢阅读有助于你更好地学习、生活和工作的故事，可以考虑* [*成为订阅者*](https://viveknaskar.medium.com/subscribe) *。成为会员后，你可以无限制地阅读 10000 篇故事、文章和作家。每月只要 5 美元。* [*如果你用我的链接*](https://viveknaskar.medium.com/membership) *注册，我会赚一点佣金，帮助我写更多的文章。*

*更多内容看*[***plain English . io***](http://plainenglish.io/)*