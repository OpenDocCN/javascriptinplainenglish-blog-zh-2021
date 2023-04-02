# 什么是密码学？RSA 算法是什么？

> 原文：<https://javascript.plainenglish.io/what-is-cryptography-and-whats-the-rsa-algorithm-d1e790c279e6?source=collection_archive---------18----------------------->

## 数据如何通过加密传输。

![](img/c1a3e6fbe2a619a58be4cf9009bf77c1.png)

[Pexels](https://www.pexels.com/photo/black-screen-with-code-4164418/)

在直接进入 RSA 算法之前，让我们了解一下术语**密码术**是什么意思。基本上，密码学来源于希腊语**秘密写作**。它意味着以一种安全的格式隐藏信息，这样只有发送者和接收者可以阅读它。

它是对文本进行基本的加密和解密，以保证其安全性和隐私性。只有接收者可以用正确的知识解密信息。有两种类型的加密技术— **对称密钥加密技术**和**非对称密钥加密技术。**

关于对称密钥加密的一个简短信息是，它使用相同的密钥进行加密和解密。密钥基本上是可以用来解密信息的信息。

类似地，非对称密钥加密是一种技术，我们**使用不同的密钥进行加密和解密**，称为**公钥**和**私钥。**

## RSA 算法

RSA 是非对称密钥密码，RSA 的完整形式是 **Rivest，Shamir，**和 **Adleman。**他们是这种算法的发明者，因此以他们的名字命名。

正如我们已经看到的，非对称密钥加密需要两个密钥一个公钥和一个私钥，RSA 算法也是如此。因此，我们需要生成用于加密和解密的 `Public`和 `Private` 密钥。

**生成公钥—**

```
1) Select two prime numbers A and B 
   Let us Take 3 and 11
   Hence, A=3 and B=112) find n which is basically A*B
   n=A*B
   n=3*11
   n=333) We also need a T which is (A-1)*(B-1)
   T=(A-1)*(B-1)
   T=(3-1)*(11-1)
   T=2*10
   T=204) We also need a exponent called as e which should not be factor of     n and less than T
   lets say that e=7 which satisfies the conditionHence Our Public Key is made of e and n = (7, 33)
```

**生成私钥—**

```
Calculate a private key d such that 
(d*e)%T=1Hence we can get d=3Therefore our private key is made of d and n=(3,33)
```

## 加密数据—

```
To encrypt any data firstly convert it into numeric form as 1 for a, 2 for b etc... Let us assume the message m to encrypt is "b"In Numeric form of b is 2Encrypted Data **c= (m)^e mod n** 
c=(2)^7 mod 33
c=29
```

## 解密数据—

```
Decrypted data **m=(c)^d mod n** 
m=(29)^3 mod 33
m=2Converting into alphabetic form we get m="b"
```

因此，我们已经成功地实现了 RSA 算法，并且看到了为了用户的隐私而加密和解密数据是多么容易。因此，我们对数据进行加密，并通过互联网将其发送给用户，在那里进行数据加密。

我希望这篇文章对所有的读者都是有益的，有意义的。不断学习，不断成长。

[](https://aniketz.medium.com/membership) [## 通过我的推荐链接加入 Medium-Aniket

### 作为一个媒体会员，你的会员费的一部分会给你阅读的作家，你可以完全接触到每一个故事…

aniketz.medium.com](https://aniketz.medium.com/membership) 

*更多内容请看*[***plain English . io***](http://plainenglish.io/)***。*** *报名参加我们的* [***免费每周简讯这里***](http://newsletter.plainenglish.io/) ***。***