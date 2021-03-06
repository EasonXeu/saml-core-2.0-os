---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.2 名称标识符

以下部分定义了SAML结构，其中包含主体以及断言和协议消息的发布者的描述性标识符。

在SAML中有很多场景，在这些场景中需要让两个系统能够关于第三方进行沟通。例如，SAML认证请求协议触发对一个主体的三方认证。因此，建立一种把相关方和对相关方都有价值的标识符关联起来的方法是很有价值的。在一些案例中，把标识符限制在只能被一小部分系统使用是很有必要的（例如，可能为了保护认证主体的私密性）。相似的名字标识符可能也会被用来指代SAML协议消息或者SAML断言的发布者（Issuer）。

两个甚至更多的系统可能使用相同的标识符来代表不同的身份，这就导致每个系统可能对相同的名字有着不同的理解。SAML提供了名字限定符（name qualifier），通过把名字标识符放到一个与名字限定符相关联的联盟命名空间来消除类似的名字标识符带来的歧义。SAML 2.0版本允许名字标识符既可以按照断言方被限定，也可以按照特定的依赖方被限定，或者，在需要时显示双方的语义。

名字标识符也可以被加密来进一步提升对私密性的保护，尤其是在一些名字标识符可能被中间方传输的情况下。

> 注意，为了避免使用相对高级的XML schema结构，不同类型的标识符元素的不会共享通用的类型层级结构。
