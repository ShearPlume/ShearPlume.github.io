---
title: week 5 Public Key Cryptography
date: 2023-05-03 04:00:52
tags:
- CSD
---

# Public Key Cryptography

## 引言

### 公钥加密：动机和需求

传统加密：

![image-20230503040530690](week-5-Public-Key-Cryptography/image-20230503040530690.png)

灵魂三问：如何保证m的保密？如何保证m的认证？如何保证m的完整？

问题 

要求发送方、接收方知道共享秘钥： 问：如何首先就密钥达成一致（尤其是在从未 "见面 "的情况下）？

加密能力与解密能力捆绑：解决机密性 

密钥管理问题：量、方法 

其他安全需求：网络

不相识、不信任 的人之间通信的安全要求

Diffe和Hellman提出：

其加密算法和解密算法分别使用 不同的密钥，从而，可将加密密钥公开(称为公开密钥P)、解 密密钥保密(称为保密密钥S)。要求：

![image-20230503041001578](week-5-Public-Key-Cryptography/image-20230503041001578.png)

解决方法：

- 发送方和接收方不共享秘密密钥
- 所有人都知道的公开加密密钥 
- 只有接收方知道的私人解密密钥 

示意图：

![image-20230503040911292](week-5-Public-Key-Cryptography/image-20230503040911292.png)



![image-20230503043537948](week-5-Public-Key-Cryptography/image-20230503043537948.png)

所有用户的密钥保存在目录服务里

##### 三点需求：

## ![image-20230503043844476](week-5-Public-Key-Cryptography/image-20230503043844476.png) 

## Diffe Hellman Key Exchange Protocol

### idea:

困难的单向操作：容易做，但很难反着做

见老师的混合色例子

### 概述：

➢ Diffie-Hellman 密钥交换使用一个指数加密系统来生成一个由两个人共享的单一密钥。
➢ 双方通过不安全的通信渠道共享信息，对密钥作出贡献。
➢ 每一方都对一些信息进行保密。这种秘密信息对于构建密钥至关重要。
➢ 密钥不能从公共信息中产生。
➢ 这种算法是许多互联网应用中构建会话密钥的基础。

### 交换步骤：

1.选择全局参数：通信双方（通常称为Alice和Bob）选择两个全局参数g和p，其中p是一个大素数，g是p的一个原根。这些参数可以公开，并且可以在多个密钥交换过程中重复使用。

2.生成私钥：Alice和Bob各自生成一个私有随机数，分别称为a和b。这些私钥必须保密，不要在通信过程中公开。

3.计算公钥：Alice和Bob分别使用全局参数和私钥计算公钥。Alice的公钥为A = g^a mod p，Bob的公钥为B = g^b mod p。公钥可以在公共通道上安全地交换。

4.交换公钥：Alice将公钥A发送给Bob，Bob将公钥B发送给Alice。

5.计算共享密钥：现在，Alice和Bob可以使用对方的公钥和自己的私钥计算共享密钥。Alice计算K_Alice = B^a mod p，Bob计算K_Bob = A^b mod p。由于离散对数的性质，K_Alice和K_Bob相等，因此双方得到相同的共享密钥K。

6.加密通信：Alice和Bob现在可以使用共享密钥K作为对称加密算法的密钥（如AES）来加密和解密数据。

### 单向函数：







## ==RSA== Public key Cryptography
