# 我用 ConvertKit 为 Gatsby 创建了一个时事通讯表单

> 原文：<https://javascript.plainenglish.io/building-a-newsletter-form-for-gatsbyjs-with-convertkit-aa31d3a991c6?source=collection_archive---------15----------------------->

## 我正在建立一个电子邮件列表，并开始时事通讯。我选择 ConvertKit 是因为它是由独立黑客为…

![](img/41c424b1a808615e11f6716392346b62.png)

“Photo by [Florian Klauer](https://unsplash.com/@florianklauer?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText) on [Unsplash](https://unsplash.com/s/photos/newsletter?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText)”

自 2020 年以来，时事通讯风靡一时！每个人都认为已经灭绝的媒介又回来了，而且比以前更强大！

这个事实在一定程度上促使我决定从零开始建立一个网站。

它将成为我订阅时事通讯的“漏斗顶端”。

技术细节。

## 与电子邮件营销工具集成

我选择 ConvertKit 是因为我可以免费开始并及时构建它。它是由一个[独立黑客](https://www.indiehackers.com/interview/convertkit-2fcb58f1fa)用小创造者的想法建造的。

我想开始建立我的电子邮件列表。然而，由于我还没有太多的内容，所以采取过于激进的立场并向我的用户推广时事通讯注册是没有意义的。

我决定在我网站的页脚添加一个时事通讯表单。

GatsbyJS 没有一种直接的方法来集成电子邮件营销工具(或显式 ConvertKit)。

我有两个选择:

*   自己写一个简单的 HTML 表单，直接发布到 ConvertKit
*   编写一个 [React](https://reactjs.org/) 组件来显示 ConvertKit 的基于 JavaScript 的表单

我选择了后者，因为它有更好的 UX 和一些额外的内置功能，我将在下面讨论。

由于 Gatsby 预先呈现了所有页面，所以您不能直接包含脚本标记——它会在构建时被解释，并且对最终用户无效。

解决方案是使用 DOM 创建一个脚本元素并显示它。

下面是组件的代码:

```
import * as React from "react";
import { Component } from "react";

class Newsletter extends Component {
  componentDidMount() {
    const script = document.createElement("script");
    script.src = "CONVERTKIT-FORM-URL";
    script.async = true;
    script.setAttribute("data-uid", "CK-UID");
    this.instance.appendChild(script);
  }

  render() {
    return (
      <div>
        <h3>Subscribe to my newsletter</h3>
        <div ref={(el) => (this.instance = el)}></div>
      </div>
    );
  }
}

export default Newsletter;
```

## 转换工具

一旦我完成了编码部分，我必须定制 ConvertKit。

我不想使用我的个人 Gmail 作为简讯的发件人，但我也不想设立一个单独的帐户或支付电子邮件托管费用。

## 电子邮件转发

我在 https://forwardemail.net 创建了一个简单的邮件转发规则，将所有邮件转发到我的 Gmail 账户。

该过程的第一步是验证您是否拥有该域名。创建帐户后，我更新了我的域名的 DNS 记录。

我通过[https://cloudflare.com](https://cloudflare.com)管理我所有的域名，并且我使用[https://www.terraform.io/](https://www.terraform.io/)自动化任何管理操作。

我不会深入探讨 Terraform 的底层(他们的文档非常好)，但下面是我使用的配置:

```
variable "zone_id_com_mihaibojin" {
  default = "GET-THIS-FROM-CLOUDFLARE"
}

resource "cloudflare_record" "com_mihaibojin_mx1" {
  zone_id  = var.zone_id_com_mihaibojin
  name     = "@"
  value    = "mx1.forwardemail.net"
  priority = 10
  type     = "MX"
}

resource "cloudflare_record" "com_mihaibojin_mx2" {
  zone_id = var.zone_id_com_mihaibojin
  name     = "@"
  value    = "mx2.forwardemail.net"
  priority = 20
  type     = "MX"
}

resource "cloudflare_record" "com_mihaibojin_forwardemail_spf" {
  zone_id = var.zone_id_com_mihaibojin
  name    = "@"
  value   = "v=spf1 a mx include:spf.forwardemail.net -all"
  type    = "TXT"
}

resource "cloudflare_record" "com_mihaibojin_forwardemail_ver" {
  zone_id = var.zone_id_com_mihaibojin
  name    = "@"
  value   = "forward-email-site-verification=GET-THIS-FROM-FORWARDEMAIL"
  type    = "TXT"
}
```

更新您的域名的 DNS，然后是一个简单的命令了！

```
terraform plan && terraform apply
```

## 正在配置转换器

在我配置了邮件转发并确认我可以接收邮件后，是时候设置 ConvertKit 了。在[添加了我的邮箱](https://app.convertkit.com/account/edit#email_settings)后，我等待确认邮件并点击了提供的链接。

## SPF 和 DKIM

我还建立了“发件人策略框架”(SPF)和“域密钥识别邮件”(DKIM)。[在这里阅读更多](https://help.convertkit.com/en/articles/2502558-using-a-verified-domain-for-email-sending)关于为什么验证你发送的电子邮件是必要的(剧透:主要是为了让你的电子邮件不会变成垃圾邮件)。

我再次使用 Terraform 来自动化这个步骤:

```
resource "cloudflare_record" "om_mihaibojin_convertkit_cname1" {
  zone_id = var.zone_id_com_mihaibojin
  name    = "ckespa.mihaibojin.com"
  value   = "spf.dm-2m2gkx6y.sg7.convertkit.com"
  type    = "CNAME"
}

resource "cloudflare_record" "com_mihaibojin_convertkit_cname2" {
  zone_id = var.zone_id_com_mihaibojin
  name    = "cka._domainkey.mihaibojin.com"
  value   = "dkim.dm-2m2gkx6y.sg7.convertkit.com"
  type    = "CNAME"
}
```

## DMARC

我做了额外的工作，还配置了 [DMARC](https://help.convertkit.com/en/articles/4534360-dmarc-what-is-it-and-should-you-use-it) 。总的来说，当你没有发送大量的电子邮件时，你不应该感到烦恼，但我想正确地开始，并为未来的成功做好准备！

DMARC 的策略设置之一是`p=none`，这意味着数据将被收集但不会被处理——这是您在这个场景中想要的。

为了监控收集到的数据，我在[https://dmarcian.com/](https://dmarcian.com/)上创建了一个账户。他们提供分析您的数据并报告任何威胁的服务。

下面是 DMARC 的 DNS 记录配置在 Terraform 中的样子:

```
resource "cloudflare_record" "com_mihaibojin_dmarc" {
  zone_id = var.zone_id_com_mihaibojin
  name    = "_dmarc.mihaibojin.com"
  value   = "v=DMARC1; p=none; rua=mailto:GET-THIS-FROM-DMARCIAN;"
  type    = "TXT"
}
```

您可以通过以下资源了解更多信息:

*   [https://www.newslettercrew.com/blog/what-is-dmarc](https://www.newslettercrew.com/blog/what-is-dmarc)
*   [https://dmarcian.com/start-dmarc/](https://dmarcian.com/start-dmarc/)

## GDPR 和时事通讯注册

我在我的[隐私友好分析](https://mihaibojin.com/personal-site/privacy-friendly-analytics-in-gatsbyjs?utm_source=Medium&utm_medium=organic&utm_campaign=rss)文章中写了欧盟的隐私和 GDPR。

ConvertKit 有一个选项，允许用户明确选择加入 GDPR 指导方针下的功能。然而，结果是用户在注册后会被重定向到一个单独的页面。

默认情况下，ConvertKit 会将用户发送到[https://app.convertkit.com/confirm-subscription](https://app.convertkit.com/confirm-subscription)。因为这会让用户离开我的网站，所以我在[https://mihaibojin.com/confirm-subscription](https://mihaibojin.com/confirm-subscription?utm_source=Medium&utm_medium=organic&utm_campaign=rss)复制了同样的信息，这样用户就可以导航回主页或其他文章了！

通过转到`Settings -> Incentive`并添加 URL，可以为在 ConvertKit 中创建的每个表单配置 URL。

## 结论

我希望这篇文章对你有用。如果你有任何想法或评论，请在这个帖子上分享你的想法[。](https://twitter.com/mihaibojin/status/1406043106915594241)

目前就这些。将来，我可能会放弃 ConvertKit JavaScript 代码，实现一个 HTML 表单，因为我不是特别喜欢跟踪我的站点上运行的 JS。

在那之前，注意安全！

如果你喜欢这篇文章，并想阅读更多类似的文章，请订阅我的时事通讯。我每隔几周就发一封！

*本文最初发布在我的网站上，*[*MihaiBojin.com*](https://MihaiBojin.com/personal-site/newsletter-convertkit?utm_source=external&utm_medium=organic&utm_campaign=rss)*。*

**延伸阅读**

[](https://circuit.ooo/blog/the-key-ingredient-behind-high-newsletter-open-rates) [## 高简讯打开率背后的关键因素

### 在这篇文章中，我们将讨论我们 9 个月前的时事通讯《简明英语上周》是如何一直…

电路. ooo](https://circuit.ooo/blog/the-key-ingredient-behind-high-newsletter-open-rates) 

*更多内容看* [*说白了。报名参加我们的*](https://plainenglish.io/) [*免费每周简讯*](http://newsletter.plainenglish.io/) *。关注我们* [*推特*](https://twitter.com/inPlainEngHQ) ，[*LinkedIn*](https://www.linkedin.com/company/inplainenglish/)*，*[*YouTube*](https://www.youtube.com/channel/UCtipWUghju290NWcn8jhyAw)*，以及* [*不和谐*](https://discord.gg/GtDtUAvyhW) *。对增长黑客感兴趣？检查* [*电路*](https://circuit.ooo/) *。*