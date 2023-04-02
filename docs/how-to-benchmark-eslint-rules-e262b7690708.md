# 如何评测 ESLint 规则

> 原文：<https://javascript.plainenglish.io/how-to-benchmark-eslint-rules-e262b7690708?source=collection_archive---------21----------------------->

![](img/1b7cb9df9fcfbe00b22410535e172487.png)

[ESLint](https://b.remarkabl.org/306x1A3)

有时 [ESLint](https://eslint.org/) 可能需要一段时间运行，尤其是当你有很多规则和文件的时候。那么，如何衡量每条规则需要多长时间呢？

通过环境变量`[TIMING](https://eslint.org/docs/1.0.0/developer-guide/working-with-rules#per-rule-performance)`，ESLint 跟踪单个规则的性能。

所以不要像这样运行 ESLint:

```
$ npx eslint ./lib/
```

在命令前加上`TIMING=1`:

```
$ TIMING=1 npx eslint ./lib/
Rule                    | Time (ms) | Relative
:-----------------------|----------:|--------:
prettier/prettier       |   136.659 |    92.4%
no-unused-vars          |     2.139 |     1.4%
no-redeclare            |     1.780 |     1.2%
no-unexpected-multiline |     0.789 |     0.5%
no-global-assign        |     0.630 |     0.4%
constructor-super       |     0.369 |     0.2%
no-unsafe-finally       |     0.323 |     0.2%
no-unreachable          |     0.319 |     0.2%
no-self-assign          |     0.311 |     0.2%
no-dupe-else-if         |     0.291 |     0.2%
```

用[纱](https://yarnpkg.com/)，可以得到总经过时间:

```
$ TIMING=1 yarn eslint ./lib/
yarn run v1.22.10
$ /Users/mark/html-react-parser/node_modules/.bin/eslint ./lib/
Rule                    | Time (ms) | Relative
:-----------------------|----------:|--------:
prettier/prettier       |   140.710 |    92.2%
no-unused-vars          |     2.573 |     1.7%
no-redeclare            |     1.748 |     1.1%
no-unexpected-multiline |     0.845 |     0.6%
no-global-assign        |     0.769 |     0.5%
constructor-super       |     0.377 |     0.2%
no-unreachable          |     0.333 |     0.2%
no-unsafe-finally       |     0.329 |     0.2%
no-dupe-else-if         |     0.287 |     0.2%
no-this-before-super    |     0.283 |     0.2%
✨  Done in 0.81s.
```

[*本文原载于 2021 年 3 月 2 日《remarkablemark.org》。*](https://b.remarkabl.org/304qFBl)