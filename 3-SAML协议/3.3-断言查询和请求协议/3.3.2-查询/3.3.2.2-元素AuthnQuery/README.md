---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 3.3.2.2 元素\<AuthnQuery\>

\<AuthnQuery\>信息元素被用于进行如下查询：“你有哪些关于这个主体的包含身份认证声明的断言？”成功的\<Response\>将包含一个或多个包含身份验证语句的断言。

\<AuthnQuery\>信息不得用来使用请求中提供的凭据进行新的身份验证的请求。\<AuthnQuery\>用来请求身份认证相关的声明，而相应的身份认证之前已经发生在指定主体和认证机构的交互中了。

该元素是```AuthnQueryType```类型的，该类型继承自```SubjectQueryAbstractType```类型，并新增如下元素和属性：

+ SessionIndex [可选]

如果存在，则用于指定可能返回的响应的过滤器。这样的查询问了一个问题是“在所提供的会话信息的上下文中，你有哪些关于这个主体的包含身份认证声明的断言”

+ \<RequestedAuthnContext\> [可选]

如果存在，则用于指定可能返回的响应的过滤器。这样的查询问了一个问题是“你有哪些关于这个主体的包含身份认证声明的断言，且这些断言能够满足\<RequestedAuthnContext\>元素中指定的认证上下文需求”

作为对认证查询的响应，SAML机构需要返回具有如下认证声明的断言：

+ 在3.3.4章节中为了匹配SAML查询中的\<Subject\>元素而给出的规则定义了可能被返回的断言

+ 如果在SAML查询中存在```SessionIndex```属性，那么在返回的一系列断言中，必须至少有一个\<AuthnStatement\>元素包含与之匹配的```SessionIndex```属性。可以选择在响应中返回所有此类匹配断言的完整集。

+ 如果在SAML查询中存在\<RequestedAuthnContext\>元素，那么在返回的一系列断言中，必须至少有一个\<AuthnStatement\>元素包含\<AuthnContext\>元素，且该元素满足查询中\<AuthnContext\>元素（参考3.3.2.2.1章节）。可以选择在响应中返回所有此类匹配断言的完整集。

下列的schema片段定义了\<AuthnQuery\>元素以及它的```AuthnQueryType```复杂类型：

```xml
<element name="AuthnQuery" type="samlp:AuthnQueryType"/>
<complexType name="AuthnQueryType">
    <complexContent>
        <extension base="samlp:SubjectQueryAbstractType">
            <sequence>
                <element ref="samlp:RequestedAuthnContext" minOccurs="0"/>
            </sequence>
            <attribute name="SessionIndex" type="string" use="optional"/>
        </extension>
    </complexContent>
</complexType>
```