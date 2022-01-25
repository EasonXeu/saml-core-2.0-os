---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 1 介绍

> 翻译自[saml-core-2.0-os文档](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)

SAML配置文件要求系统实体之间就标识符、绑定支持、访问端点、证书和密钥等达成一致。元数据规范有助于以一个标准的方式描述这些信息。这个规范为SAML系统实体定义了一个可扩展的元数据格式，并且由能够反映SAML配置文件的角色组织起来。这些角色包括SSO身份提供商（IDP）、SSO服务提供商（SP）、从属关系、属性权限、属性请求者和策略决策点。

这个规范进一步定义了系统实体之间进行元数据动态交换的配置文件，这在进行部署的场景中会很有用。

SAML一致性文档[【SAMLConform】](https://docs.oasis-open.org/security/saml/v2.0/saml-conformance-2.0-os.pdf)列出了构成SAML2.0的所有规范。

