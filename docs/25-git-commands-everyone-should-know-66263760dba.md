# 每个人都应该知道的 25 个 Git 命令

> 原文：<https://javascript.plainenglish.io/25-git-commands-everyone-should-know-66263760dba?source=collection_archive---------27----------------------->

## 我们日常需要的有用命令清单

![](img/4377c453088f0e736cabcebcf3ac9e2d.png)

Photo by [Aaron Burden](https://unsplash.com/@aaronburden?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)

因为我们确实大多使用 IDE 和其他软件来避免编写命令和使用 GIT，但是我们最好随身携带命令，以备不时之需。

下面是我们在开发任何东西时最常用的命令。

> *创建项目*

# 1.初始化本地 Git 存储库

```
git init
```

# 2.创建远程存储库的本地副本

```
git clone ssh://git@github.com/[username]/[repository-name].git
```

> *基本拍摄*

# 3.检查状态

```
git status
```

# 4.将文件添加到临时区域

```
git add [file-name.txt]
```

# 5.将所有新的和已更改的文件添加到临时区域

```
git add -A
```

# 6.提交更改

```
git commit -m "[commit message]"
```

# 7.删除文件(或文件夹)

```
git rm -r [file-name.txt]
```

> *分支&合并*

# 8.列出分支(星号表示当前分支)

```
git branch
```

# 9.创建新分支

```
git branch [branch name]
```

# 10.删除分支

```
git branch -d [branch name]
```

# 11.创建一个新的分支并切换到它

```
git checkout -b [branch name]
```

# 12.克隆远程分支并切换到该分支

```
git checkout -b [branch name] origin/[branch name]
```

# 13.重命名本地分支

```
git branch -m [old branch name] [new branch name]
```

# 14.切换到一个分支

```
git checkout [branch name]
```

# 15.将分支合并到活动分支中

```
git merge [branch name]
```

# 16.将分支合并到目标分支中

```
git merge [source branch] [target branch]
```

# 17.将更改存储在脏的工作目录中

```
git stash
```

# 18.删除所有隐藏的条目

```
git stash clear
```

> *分享&更新项目*

# 19.将一个分支推送到您的远程存储库

```
git push origin [branch name]
```

# 20.将更改推送到远程存储库

```
git push
```

# 21.将本地存储库更新为最新提交

```
git pull
```

# 22.从远程存储库中提取更改

```
git pull origin [branch name]
```

# 23.添加远程存储库

```
git remote add origin ssh://git@github.com/[username]/[repository-name].git
```

> *检查&比较*

# 24.查看更改

```
git log
```

# 25.合并前预览更改

```
git diff [source branch] [target branch]
```

## 结论

我希望你觉得这个指南有用。我们还遗漏了其他命令吗？如果有，请在评论中告诉我们！

# 进一步阅读

*更多内容请看*[***plain English . io***](http://plainenglish.io)