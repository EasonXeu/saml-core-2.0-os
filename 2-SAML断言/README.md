---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2 SAML断言

断言是一个信息的集合，这个集合中包含了由SAML机构(SAML authority) 颁发的零个或多个声明。在讨论SAML断言的生成和交换的过程中，SAML机构有时候也被称为断言方（asserting parties），而收到并使用SAML断言的一方系统被称为依赖方（relying parties）。（注意，这些术语是保留词汇，专门用来讨论SAML协议的信息交换过程，和HTTP中的请求方和响应方是不同的）。

通常情况下，SAML断言是用来描述一个主体（Subject），这个主体用 \<Subject>元素来表示。然而，这个\<Subject>元素是可选择的。在一些其他的规范和定义中，它们使用了SAML断言的框架结构来做类似的声明但却没有指定一个主体，或者是以其他方式来指定主体。通常，会有很多的服务提供方（Service Provider）使用关于一个主体的断言来进行自身系统的访问控制进而提供一些定制的服务。相应的，这些服务提供方就变成了断言方的依赖方。断言方（asserting party）也被称为身份提供方（Identity Party）。

> 译者注（义臻）：原文中上面的话很绕，简言之，SAML断言的交换过程中会涉及两方。断言方和依赖方，对应的也可以叫做身份提供方（Identity Provider）和服务提供方（Service Provider），对应的英文缩写是IDP和SP。

SAML规范中定义了SAML机构可以颁发的三种不同类型的断言声明。所有SAML定义的声明都是关于一个Subject主体的。这三种不同类型的断言声明分别是：

* Authentication：断言的主体在特定的时间被以一种特定的认证手段进行了认证。
* Attribute：断言的主体所关联的一些属性。
* Authorization Decision：断言的主体访问特定的资源的请求被允许了还是被禁止了。

断言声明的外部结构是很通用的，它提供了关于断言声明的一些常用信息。在断言中，一系列的内部元素描述了Authentication、Attribute、Authorization Decision或者一些包含了指定信息的用户自定义的声明。

正如第7章所描述的，SAML断言的schema是允许被扩展的，允许用户自定义的对断言和声明的扩展，同时也允许定义新类型的断言和声明。

SAML技术概览[【SAML TechOvw】](https://www.oasis-open.org/committees/download.php/27819/sstc-saml-tech-overview-2.0-cd-02.pdf)和术语表[【SAML Gloss】](https://docs.oasis-open.org/security/saml/v2.0/saml-glossary-2.0-os.pdf)提供了更多的关于SAML术语和概念的解释。
