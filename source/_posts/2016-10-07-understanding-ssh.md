---
categories: tech
layout: post
title: 理解ssh加密和连接流程(译)
date: 2016-10-07
tags:
- 工具
---

#### 简介

SSH全称secure shell，是管理远程服务器最常用的方法。通过使用一系列的
加密技术，SSH 提供了这样一个机制：建立安全加密连接，互相授权，发送命令和返回输出结果。 
在其他文章中，我们讨论过了如何配置ssh访问，如何使用ssh连接，和一些ssh建议和技巧。 
在本文，我们将介绍SSH的底层加密技术和建立加密连接的方法。这对于理解多个加密层以及建立连接，相互授权的步骤是非常有用的。


#### 对称加密，非对称加密和哈希

为了安全的传输信息，SSH在传输过程中的不同阶段，采用不同类型的控制技术。这些技术包括对称加密，非对称加密和哈希。  


1. 对称加密

加密和解密组件的关系决定了一个加密技术是对称的还是非对称的。


对称加密指的是一个密钥既可以用来加密消息，也可以用来解密消息。这意味着通信双方都持有相同的密钥，既可以加密又可以解密。这种加密方式又叫做“共享加密”或“密钥加密”。典型的是只有一个密钥或者一对关系紧密的密钥（获得另一个密钥并不重要）。


在SSH中，对称加密用于加密整个连接。与一些用户猜想的不同，公／私非对称密钥只用来授权。对称加密也用于密码授权。


客户端和服务器一起生成密钥，生成的密钥不会被第三方知道。密钥是通过一个叫做密钥交换算法生成的。交换的结果是服务器和客户端双方获得相同的密钥。这个流程将在后面详细介绍。


对称加密密钥的生成是基于session的，并建立了实际传输数据的加密。一旦密钥建立所有数据必须通过共享密钥加密。这是在授权客户端之前完成的。


SSH可配置使用多种不同的对称加密系统，包括AES，Blowfish，3DES，CAST128，和Arcfour。客户端和服务器都有一个算法列表，根据优先级来决定使用哪种加密算法。客户端列表中的第一选择，如果服务器也支持，这个算法将被采用。

在Ubuntu 14.04，客户端和服务器的默认算法列表均为:aes128-ctr, aes192-ctr, aes256-ctr, arcfour256, arcfour128, aes128-gcm@openssh.com, aes256-gcm@openssh.com, chacha20-poly1305@openssh.com, aes128-cbc, blowfish-cbc, cast128-cbc, aes192-cbc, aes256-cbc, arcfour。 这就是说，如果两个Ubuntu14.04机器建立连接，（如果没有通过修改配置文件，修改默认算法列表），它们将采用aes128-ctr算法来加密连接。

2. 非对称加密

非对称加密中，需要两个密钥：一个叫公钥，另一个叫私钥。公钥可以被放到任何地方。私钥应该保密，不能与其他方共享。私钥不能靠公钥计算获得。公钥和私钥的关系是：公钥加密的数据只能靠私钥解密。这个操作是单向的，也就是说，公钥没有办法解密自己加密的数据。

SSH在很多地方使用了非对称加密。比如，在建立对称加密时,交换密钥的过程中，双方产生临时密钥对，用来交换共享密钥（对称加密，用于加密整个session）。

非对称加密在SSH中最被人熟知的用途是基于密钥的授权。客户端生成密钥对，然后将公钥上传到访问服务器，放到~/.ssh/authorized_keys 文件中。

在服务器与客户端的对称加密建立以后，客户端需要被授权访问。服务器使用公钥加密一条消息并发送给客户端。如果客户端能解密这条消息，说明拥有私钥，于是授权成功。

3. 哈希

SSH还用了一种数据处理叫做哈希加密。哈希加密用来生成数字签名。哈希加密的主要特点是不能反向解密。生成的数字签名不可预测，而且是唯一的。

使用相同的哈希算法加密消息产生的hash值是不变的。修改消息的任何部分将产生完全不同的哈希值。用户不能通过hash值获得原始的消息，但是可以根据能判断一个消息是否对应给定的hash值。

基于以上特性，哈希值一般用于数据完整性验证和消息可靠性检查。
SSH中哈希主要用于HMAC（hash-based message authentication code基于hash的消息授权检查）,用来保证收到的消息是完整的，未修改的。

#### SSH是如何工作的

<未完待续...>




