# 9 种最流行的测试工具，从 Bug 跟踪器到 GUI 分析器

> 原文：<https://javascript.plainenglish.io/9-most-popular-testing-tools-from-bug-trackers-to-gui-analyzers-3fb549b3d694?source=collection_archive---------20----------------------->

## 面向程序员各种测试场景的开源工具。

![](img/48461b15d42b338e82d2772ad1361c05.png)

Photo by [Windows](https://unsplash.com/@windows?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

无论是对脚本进行简单的语法测试，还是对复杂的 web 应用程序进行复杂的黑盒测试，使用正确的工具，测试都可以快速而愉快地完成。在这里，我将展示您可以使用的顶级开源工具。

## 1.[硒](https://www.selenium.dev/)

Selenium 是最著名的开源测试工具之一。该工具(或者更确切地说是工具集)用于测试 web 应用程序，并且或多或少地用于自动化管理任务。简而言之，用 Selenium 自己的话说:“Selenium 自动化浏览器。”

Selenium IDE 旨在作为一个纯粹的原型开发工具:作为 Firefox 或 Chrome 插件实现，用户交互可以以宏记录器的方式记录和回放。然而，IDE 不可能作为真正的测试应用程序，因为没有迭代选项或条件语句。然而，Selenium-Grid 可以用于在分布式环境中运行 Selenium-1 测试，例如，同时从几个主机运行，以提高性能。

## 2. [Appium](https://appium.io/)

顾名思义，Appium 专门从事 iOS 和 Android 上的移动应用程序的测试自动化。有趣的是，上面提到的 WebDriver 也在后台来帮忙了。基本上，Appium 是应用程序的 Selenium——即使它没有像类似的存储工具 Selendroid 那样大胆地宣传，它自称为“Android 的 Selenium”

因此，Appium 依赖于自动化黑盒测试，简而言之，模拟真实用户。两个方面使得 Appium 特别有趣:一方面，该项目测试实际发布的最终应用程序——而不是为了内部测试而修改的版本。但是，另一方面，Appium 试图给用户尽可能多的自由。

这些测试使用 Node.js 从 HTTP 服务器运行，可以用 Ruby、C #、Java、JavaScript、Objective-C、PHP、Python、Perl 和 Clojure 编写。整个过程可以在仿真器和模拟器上运行，也可以在真实的终端设备上运行。得益于强大的跨平台功能，Appium 实际上是一个通用的测试工具。

## 3. [Selendroid](http://selendroid.io/)

Selendroid 将自己视为 Android 的 Selenium:测试通过 Selenium API 进行，可以平等地测试移动 web 和原生 Android 应用程序。

测试可以在模拟器上运行，也可以在真正的智能手机和平板电脑上运行。亮点包括真实硬件的热插拔、手势支持、与 Selenium 网格的集成。

## 4.[黄瓜](https://cucumber.io/)

Cucumber 使用了一种令人兴奋的方法——也用于管理。Cucumber 运行以行为驱动开发(BDD)风格编写的测试。这里用小黄瓜语言定义了预期的行为。例如，一个应用程序提供了关于星期几的正确答案。

真正的特别之处:Gherkin 用人类可以理解的语言制定了这样的测试用例，并定义了诸如“When”和“Then”这样的关键字，因此在简单的情况下，它最初看起来几乎像一个典型的伪代码。当然，这些测试用例仍然必须被转换成具体的编程语言，默认情况下是通过 Ruby。但是也有 Java、JavaScript 和 Python 的端口。

这种类型的测试设置旨在简化程序员和应用程序的管理层或技术主管之间的交流。不幸的是，cucumber 本身没有为 web 应用程序/浏览器提供自动化，但是可以与 Selenium 一起工作。

## 5. [JMeter](https://jmeter.apache.org/)

Apache JMeter 是一个纯 Java 应用程序，用于运行功能负载测试和测试性能。可能的测试对象包括 HTTP、FTP、LDAP、邮件协议、TCP 和 Java 对象。JMeter 是这种环境中最成熟的工具，可以回顾 20 多年的发展历程。

Apache 工具是独立于平台的，masters 多线程可以通过插件进行扩展，提供开箱即用的动态 HTML 报告，并且可以通过 GUI 和命令行使用。JMeter 至少应该作为一个参照物而为人所知——但也存在竞争，比如 Grinder。

## 6.[磨床](http://grinder.sourceforge.net/)

有了“研磨机”，可以同时从几个设备上测试所有 Java API 的性能。该工具使用 Jython(Python 的 Java 实现)和 Clojure 语言编写测试脚本，主要面向开发人员。

JMeter 通过复杂性、社区和报告等扩展功能进行评分。Grinder 对于分布式环境中的性能和测试来说更加直观和令人信服，对于深信不疑的 JMeter 用户来说也是一种资产。

## 7. [LDTP — GUI 测试](https://ldtp.freedesktop.org/wiki/)

Linux 桌面测试项目中有一个不太常见的图形用户界面测试软件。自动测试纯脚本和 CLI 程序相对简单 GUIs 看起来复杂得多。

任何尝试过用鼠标记录宏的人都知道许多问题的秘诀。因此，为了解决 GUI 问题，LDT 项目使用了 Gnome 应用程序、Mozilla、OpenOffice.org 以及基于 Qt 4 和 KDE 4 的程序所能提供的辅助功能。

还有 Mac OS X 和 Windows 的版本。这样，GUI 也可以使用 Python 脚本以标准化的方式来处理。不可否认，这个项目并不像大型(半)商业测试套件那样完美，也没有那么广泛的文档记录，但绝对是测试图形应用程序的一个令人兴奋的方法。

## 8.Bugzilla

20 多年来，Bugzilla 一直是许多开发人员的忠实伙伴，与其说它是一种测试工具，不如说它是一种辅助工具——然而，它不应该在任何开发或测试环境中缺失。使用 bug tracker，即使在大型团队和组织中，也可以管理和跟踪各种类型的 bug。因此，Bugzilla 可以说是实际测试结果的安全网；毕竟，通过自动化测试发现的弱点和错误很少会立即得到修补。

## 9.[计量自动化框架](https://qmetry.github.io/qaf/index.html)

最后，在您的开源工具收藏中不应该缺少另一个不进行自我测试的免费工具:QMetry Automation Framework 是一个用于执行和编写测试的复杂框架。实际测试是在后台完成的，其中包括 Selenium 和 Appium 等老朋友。

这个选择包括来自不同领域的工具，从 bat 的“简单”shell 脚本测试到 LDTP GUI 的可评估性需求，再到 Cucumber 的管理兼容行为模拟。所有提供的工具都是开源版本。有些还提供扩展的商业版本。

*更多内容尽在*[*plain English . io*](http://plainenglish.io/)