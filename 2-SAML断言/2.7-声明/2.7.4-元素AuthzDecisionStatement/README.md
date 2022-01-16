---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.4 元素\<AuthzDecisionStatement\>

> 注意：\<AuthzDecisionStatement\>特性在SAML 2.0版本中已经冻结了，未来没有改进计划。需要额外功能的用户可能需要可扩展的访问控制标记语言[XACML]，它能提供增强的授权决策功能。

The <AuthzDecisionStatement> element describes a statement by the SAML authority asserting that a request for access by the assertion subject to the specified resource has resulted in the specified authorization decision on the basis of some optionally specified evidence. Assertions containing <AuthzDecisionStatement> elements MUST contain a <Subject> element.


