---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.4.1 元素\<Subject>

元素\<Subject>是可选的，它用来指定受信实体，即SAML断言中所有声明（0个或者多个）的主体。它包含一个标识符，或一系列的一个或多个对主体身份的确认，或者两者都包含：

*   \<BaseID>、\<NameID>、或\<EncryptedID> \[可选]

    定义主体
*   \<SubjectConfirmation> \[零个或多个]

    认可主体身份所需要满足的信息。如果有超过一个的\<SubjectConfirmation>元素，那么满足其中的任何一个都足以确认该主体身份，以最终达到使用断言的目的。

> 译者（义臻）注：在IAM体系中，受信实体对应的英文单词通常为Principal，有时也用Trusted Entity表示。可以简单理解成被信任的一方。

\<Subject>元素可以包含一个标识符以及零个或多个\<SubjectConfirmation>元素，而依赖方在处理断言的过程中可以验证这些\<SubjectConfirmation>元素。如果其中任何一个\<SubjectConfirmation>元素验证通过，依赖方就可以将发布断言的实体视为断言方，且该断言方已经同标识符所代表的受信实体、以及断言中的声明关联起来了。断言中声明的实体和实际的主体可能是也可能不是同一个实体。

> 译者（义臻）注：在SAML 2.0中，SP通常也叫做依赖方（relaying party），指的是消费SAML断言的一方。IDP通常也叫断言方（asserting party），指的是发布SAML断言的一方。

如果\<Subject>元素中不包含\<SubjectConfirmation>元素，那么断言发布者和实际的主体之间的任何关系都是未指定的。

\<Subject>元素不应该定义超过一个受信实体。

下面的schema片段定义了\<Subject>元素、以及它的`SubjectType`复杂类型：

```xml
<element name="Subject" type="saml:SubjectType"/>
<complexType name="SubjectType">
    <choice>
        <sequence>
            <choice>
                <element ref="saml:BaseID"/>
                <element ref="saml:NameID"/>
                <element ref="saml:EncryptedID"/>
            </choice>
            <element ref="saml:SubjectConfirmation" minOccurs="0"
            maxOccurs="unbounded"/>
        </sequence>
        <element ref="saml:SubjectConfirmation" maxOccurs="unbounded"/>
    </choice>
</complexType>
```
