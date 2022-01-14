---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.2 元素\<AuthnStatement\>

\<AuthnStatement\>元素用于描述SAML权威机构的声明，该声明断言了当前断言主体是在特定的时间以特定的方式被认证的。包含\<AuthnStatement\>元素的断言必须包含一个\<Subject\>元素。

它是```AuthnStatementType```类型的，该类型继承自```StatementAbstractType```类型，并且增加了以下的元素和属性：

> 注意：\<AuthorityBinding\>元素及其相关类型已经从 SAML2.0版本的\<AuthnStatement\>元素中移除。

+ AuthnInstant [必须]

指定了认证发生的时间。该值是UTC格式，符合1.3.3章节中的描述。

+ SessionIndex [可选]

指定主体标识的身份与认证机构之间的特定会话的索引。

+ SessionNotOnOrAfter [可选]

标识一个时间点，到达改时间点之后，主体标识的身份与发布声明的认证机构之间的会话被视为结束。该值是UTC格式，符合1.3.3章节中的描述。此属性和可能在断言中存在的```NotOnOrAfter```条件属性之间没有必然联系。

> 译者（义臻）注：通常来讲，一个用户在登录之后，登陆中心会为此用户维护一个登录态Session，该Session是有过期时间的。在生成SAML断言时，登录中心通过```SessionNotOnOrAfter```属性来声明这个过期时间。

+ \<SubjectLocality\> [可选]

指定断言主体发生认证时所在的系统的DNS域名和IP地址。

+ \<AuthnContext\> [必须]

身份验证机构使用的上下文，包括产生此声明的身份验证事件。包含一个认证上下文类型引用，一个认证上下文声明或者声明引用，或两者兼备。有关身份验证上下文信息的完整描述，请参见身份验证上下文规范 [SAMLAuthnCxt]。

一般来说，任何字符串值都可以用作```SessionIndex```的值。但是，当涉及隐私的时候，必须考虑到```SessionIndex```的值不能使其他隐私机制无效。相应的，该值不能用于关联身份实体在不同会话参与者中的活动。推荐使用下面提供的两种解决方案来实现此目标：
 
+ 使用小的正整数（或列表中重复出现的常量）来标识```SessionIndex```。SAML认证机构应该选择值的范围，使得任何一个整数的基数都足够高，以防止特定身份实体的行为在多个会话参与者之间相互关联。SAML认证机构应该从这个范围内随机选择值来标识```SessionIndex```（除非需要确保给同一会话参与者但作为不同会话的一部分的后续语句的唯一值）。

+ 在```SessionIndex```中使用封闭断言的ID值。

> 译者（义臻）注：在生成断言时，通常使用方法二，即使用AuthnStatement元素所在的断言的ID值作为```SessionIndex```的值。

下列的schema片段定义了\<AuthnStatement\>元素以及它的```AuthnStatementType```复杂类型：

```xml
<element name="AuthnStatement" type="saml:AuthnStatementType"/>
<complexType name="AuthnStatementType">
    <complexContent>
        <extension base="saml:StatementAbstractType">
            <sequence>
                <element ref="saml:SubjectLocality" minOccurs="0"/>
                <element ref="saml:AuthnContext"/>
            </sequence>
            <attribute name="AuthnInstant" type="dateTime" use="required"/>
            <attribute name="SessionIndex" type="string" use="optional"/>
            <attribute name="SessionNotOnOrAfter" type="dateTime" use="optional"/>
        </extension>
    </complexContent>
</complexType>
```