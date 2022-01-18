---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.4 元素\<AuthzDecisionStatement\>

> 注意：\<AuthzDecisionStatement\>特性在SAML 2.0版本中已经冻结了，未来没有改进计划。需要额外功能的用户可能需要可扩展的访问控制标记语言[XACML]，它能提供增强的授权决策功能。

\<AuthzDecisionStatement\>元素描述了SAML机构的一条语句，该语句声称已经基于一些证据就断言主体能够访问指定的资源做出了授权决定。包含\<AuthzDecisionStatement\>元素的断言必须包含\<Subject\>元素。

资源是通过URI引用来进行标识的。为了能够正确且安全地解析断言，SAML机构和SAML依赖方必须以一致的方式解释每一个URI引用。如果不能实现一致的URI引用解释，那么，资源URI引用的编码的不同就可能会导致不同的授权决策。在[RFC 2396]第6节中可以找到规范化URI引用的规则：

> 一般来说，规范格式的等价规则和定义（如果有）依赖于schema。当schema使用通用语法的元素时，它也会使用通用语法的等价规则，即，协议头和主机名不区分大小写，且URL带有显式的":port"。其中，当端口是协议头对应的默认端口时，就相当于省略端口的情况。


为了避免由于URI编码的变化而导致的歧义，SAML系统实体应该尽可能地使用URI的规范化形式，如下所示：

+ SAML机构应该以规范化的格式编码所有的资源URI引用。

+ SAML依赖方应该在处理断言之前将资源URI引用转换为规范化的格式。

//TODO
Inconsistent URI reference interpretation can also result from differences between the URI reference
syntax and the semantics of an underlying file system. Particular care is required if URI references are
employed to specify an access control policy language. The following security conditions SHOULD be
satisfied by the system which employs SAML assertions:
