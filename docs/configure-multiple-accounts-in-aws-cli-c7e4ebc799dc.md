# 在 AWS CLI 中配置多个帐户

> 原文：<https://javascript.plainenglish.io/configure-multiple-accounts-in-aws-cli-c7e4ebc799dc?source=collection_archive---------19----------------------->

![](img/628f7f2226eb7d84d6a9389f9a5f0711.png)

AWS CLI 是一个很好的工具，可以做任何与 AWS 相关的事情。我们可以使用访问密钥 ID 和秘密访问密钥来配置帐户的访问密钥。但是如果我们想在同一台电脑上使用多个账户呢？如果我们在多个 AWS 项目上工作，或者对于不同的项目有不同的 IAM 角色？

在设置多个帐户之前，让我们先设置一个帐户。

# 创建 AWS 配置文件

为了验证我们自己，我们需要创建一个 AWS 概要文件，用于所有未来的会话。访问密钥用于签署使用我们的程序向 AWS 发出的请求。我们将首先在 AWS 控制台中创建一个概要文件。然后以. csv 格式下载。(如果丢失，将无法恢复，并且需要重新创建具有权限的新用户)。

如果我们计划在与 AWS 的通信中只使用一个用户配置文件，我们可以使用命令:

```
$ aws configure
AWS Access Key ID [None]: <Enter Access Key>
AWS Secret Access Key [None]: <Enter Secret Access Key>
Default region name [None]: <Enter Region>
Default output format [None]: json
```

这将在~/中创建两个文件。aws(或%USERPROFILE%)。aws/在 Windows 上)目录。一个是凭证，另一个是配置。

```
# ~/.aws/credentials
[default]
aws_access_key_id=<Your Access Key>
aws_secret_access_key=<Your Secret Access Key>

# ~/.aws/config
[default]
region=<Your Region>
output=json
```

# 命名 AWS 配置文件

AWS CLI 允许我们设置命名配置文件(这将帮助我们创建多个帐户)。命名的概要文件只是一个附加了名称的概要文件。为了创建一个命名的概要文件，我们使用:

```
$ aws configure --profile <profile name>
```

假设我们在 AWS CLI 中使用名称 dev 创建了一个概要文件。对配置文件的相应更新将是:

```
# ~/.aws/credentials
[default]
aws_access_key_id=<Your Access Key>
aws_secret_access_key=<Your Secret Access Key>

[dev]
aws_access_key_id=<Dev Access Key>
aws_secret_access_key=<Dev Secret Access Key>

# ~/.aws/config
[default]
region=<Your Region>
output=json

[profile dev]
region=<Dev Region>
output=json
```

# 在 AWS CLI 中配置多个帐户

因为我们可以创建多个概要文件，所以我们可以简单地使用命名概要文件来创建多个帐户。我们可以为任意多的用户创建任意多的配置文件。AWS CLI 按以下顺序查找凭据:

*   **AWS CLI 选项:**调用 CLI 时传入的命令行参数
*   **环境变量:**将 AWS_ACCESS_KEY_ID 和 AWS_SECRET_ACCESS_KEY 作为环境变量导出
*   **AWS 凭证文件:**我们刚刚讨论的文件

并且凭证文件也可以有多个配置文件。如果我们想要使用凭证文件，我们需要在 AWS CLI 中运行命令时添加“-profile”标志。

每次都将配置文件指定为 CLI 参数可能是一项单调乏味的任务。因此，最好使用环境变量。我们甚至可以使用以下方法将概要文件导出到环境变量中:

```
export AWS_PROFILE=dev
```

dev AWS 配置文件将用于所有后续命令，而无需显式指定它。

## 结论

我们使用 AWS CLI 对多个帐户的简单设置到此结束。如果你有任何意见，请在下面留言。

*原载于 2021 年 2 月 20 日 https://www.wisdomgeek.com**[*。*](https://www.wisdomgeek.com/development/aws/configure-multiple-accounts-in-aws-cli/)*