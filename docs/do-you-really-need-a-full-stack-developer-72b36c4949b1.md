# 你真的需要一个全栈开发者吗？

> 原文：<https://javascript.plainenglish.io/do-you-really-need-a-full-stack-developer-72b36c4949b1?source=collection_archive---------2----------------------->

![](img/beaee51ded19ae5c4f48cdd95e643c3a.png)

Photo by [Oskar Yildiz](https://unsplash.com/@oskaryil?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

Web 应用程序开发涉及许多活动，例如:

*   捕捉用户故事
*   创建实体模型
*   开发核心组件
*   构建原型
*   开发工作应用程序
*   部署
*   测试
*   并最终被商业用户接受。

在 web 应用程序开发的整个生命周期中，涉及到许多技能。最近，我们看到了对全栈开发人员的高需求。

> 考虑一个板球队(或任何运动队)。我们需要专业的投球手、专业的击球手和少数全才。有时候，全才有助于赢得一场比赛甚至一个系列赛。但是，没有没有专家的团队*。*全栈开发者是必要的，但还不够。
> 
> Wicket-keeper batsman/batswoman 是您的开发人员，他们可以设置 CI/CD 管道。

为什么我们需要全栈开发人员？一个简单的答案是，开发者可以同时处理后端 API 和 UI 组件。很公平，它们在以下场景中可能是有益的:

*   小团队——最多 3 或 4 名成员
*   有预算限制的增强项目
*   支持和维护项目，其中开发人员可以选择各种票证

但是如果你有更多的团队成员，全栈开发人员充其量只能提供一个**中性或负面效果**。想知道为什么吗？

服务/API 的基本原则是**服务抽象:**

> 包含有关其封装内容的细节(例如，用于构建服务的逻辑、实现和技术)的服务契约可能会通过向服务消费者提供有关服务工作的更多知识而以特定的方式被使用 ***。*** [来源:维基](https://en.wikipedia.org/wiki/Service_abstraction)

现在，如果你想一想，一个做端到端实现的全栈开发人员很容易被他自己的行为和责任误导。代码库中会有几个坑爹的地方。该团队稍后将能够发现它们。

相反，让全栈开发人员参与进来，给他们贴上 UI 或后端专家的标签，让他们扮演相反的角色。在随后的冲刺中换一个不同的角色。

从开发生命周期的角度来看，有几个简单的技术可以消除全栈开发人员的依赖性:

1.  API 合同
2.  模拟服务

如果你认为以上两点微不足道，我不会感到惊讶。反过来，如果你觉得这两点很费时间，很好拥有，请注意以下几点。

*   API 合同并不一定意味着你应该把 OpenAPI / Swagger 文档放在紧张的状态下发布。它可能只是 API 和 UI 开发人员之间的书面或电子邮件协议。
*   采用测试驱动开发(TDD)是一个项目/产品最好的事情。但是理解并正确地去做并不是一件容易的事情。相反，从模拟服务开始开发，这最终会帮助您的单元测试和/或端到端测试。

> [React](https://github.com/facebook/react) 有 168k， [Vue](https://github.com/vuejs/vue) 有 183k GitHub 星。
> [幻影](https://github.com/miragejs/miragejs)有 4k， [MSW](https://github.com/miragejs/miragejs) 有 5k GitHub 星。这些数据点表明前端开发社区刚刚开始采用测试驱动的方法。

[Mirage](https://github.com/miragejs/miragejs) (同样 MSW)减少了对 real API 的依赖，加快了 Web 应用开发。

> 不要过分强调 Mirage 的 ORM 特性。

**结论**

我是一个全栈开发者，我自己也是一个架构师。博客的想法并不是规定，而是帮助你认识到可能的陷阱。我希望这里的想法能帮助你的团队。欢迎在评论中告诉我们。

*更多内容请看*[*plain English . io*](http://plainenglish.io/)