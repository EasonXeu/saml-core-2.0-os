---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.4 元素\<AuthzDecisionStatement\>

> 注意：\<AuthzDecisionStatement\>特性在SAML 2.0版本中已经冻结了，未来没有进行功能增强的计划。需要额外功能的用户可能需要使用可扩展的访问控制标记语言[XACML]，它能提供增强的授权决策能力。

\<AuthzDecisionStatement\>元素描述了SAML机构的一条语句，该语句声称已经基于一些证据就断言主体能够访问指定的资源做出了授权决定。包含\<AuthzDecisionStatement\>元素的断言必须包含\<Subject\>元素。

资源是通过URI引用来进行标识的。为了能够正确且安全地解析断言，SAML机构和SAML依赖方必须以一致的方式解释每一个URI引用。如果不能实现一致的URI引用解释，那么，资源URI引用的编码的不同就可能会导致不同的授权决策。在[RFC 2396]第6节中可以找到规范化URI引用的规则：

> 一般来说，规范格式的等价规则和定义（如果有）依赖于schema。当schema使用通用语法的元素时，它也会使用通用语法的等价规则，即，协议头和主机名不区分大小写，且URL带有显式的":port"。其中，当端口是协议头对应的默认端口时，就相当于省略端口的情况。


为了避免由于URI编码的变化而导致的歧义，SAML系统实体应该尽可能地使用URI的规范化形式，如下所示：

+ SAML机构应该以规范化的格式编码所有的资源URI引用。

+ SAML依赖方应该在处理断言之前将资源URI引用转换为规范化的格式。

URI引用解释不一致也可能是由于URI引用语法和底层文件系统语义之间的差异造成的。如果使用URI引用来指定访问控制策略语言，则需要特别注意这个问题。使用SAML断言的系统应该满足下列的安全条件：

+ URI引用语法的部分要区分大小写。如果底层文件系统是大小写不敏感的，请求者不能通过更改资源URI引用的大小写来访问被拒绝的资源。

+ 许多文件系统都支持逻辑路径和符号链接等机制，这些机制允许用户在文件系统条目之间建立逻辑等价关系。请求者不能通过创建这样的等价关系来访问被拒绝的资源。


\<AuthzDecisionStatement\>元素是```AuthzDecisionStatementType```类型的，该类型继承自```StatementAbstractType```类型，并且具有下列额外的元素和属性：

+ Resource [必须]

一个URI引用，用于标识被授权去访问的资源。此属性的值可能为空URI引用（“”），根据[RFC 2396]第4.2节的规定，其含义为“当前文档的开始”。

+ Decision [必须]

SAML机构对指定资源做出的授权决定。其值是```DecisionType```简单类型。

+ \<Action\> [一个或更多]

授权可以在指定的资源上执行的动作集合。

+ \<Evidence\> [可选]

SAML机构在做出授权决定时所依赖的一组断言。

下列的schema片段定义了\<AuthzDecisionStatement\>元素以及它的```AuthzDecisionStatementType```复杂类型：

```xml
<element name="AuthzDecisionStatement" type="saml:AuthzDecisionStatementType"/>
<complexType name="AuthzDecisionStatementType">
    <complexContent>
        <extension base="saml:StatementAbstractType">
        <sequence>
            <element ref="saml:Action" maxOccurs="unbounded"/>
            <element ref="saml:Evidence" minOccurs="0"/>
        </sequence>
        <attribute name="Resource" type="anyURI" use="required"/>
        <attribute name="Decision" type="saml:DecisionType" use="required"/>
        </extension>
    </complexContent>
</complexType>
```

