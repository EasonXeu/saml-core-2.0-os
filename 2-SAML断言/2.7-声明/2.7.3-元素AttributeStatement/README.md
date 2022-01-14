---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.3 元素\<AttributeStatement\>

\<AttributeStatement\>元素用于描述SAML权威机构的声明，该声明断言了当前断言主体是和指定的属性相关联的。包含\<AttributeStatement\>元素的断言必须包含\<Subject\>元素。

该元素是```AttributeStatementType```类型的，这个类型继承自```StatementAbstractType```，并且添加了以下元素：

+ \<Attribute\>或者\<EncryptedAttribute\> [一个或多个]

\<Attribute\>元素指定了断言主体的一个属性。\<EncryptedAttribute\>元素指定了一个加密了的SAML属性。

下列的schema片段定义了\<AttributeStatement\>元素以及它的```AttributeStatementType```复杂类型：

```xml
<element name="AttributeStatement" type="saml:AttributeStatementType"/>
<complexType name="AttributeStatementType">
    <complexContent>
        <extension base="saml:StatementAbstractType">
            <choice maxOccurs="unbounded">
                <element ref="saml:Attribute"/>
                <element ref="saml:EncryptedAttribute"/>
            </choice>
        </extension>
    </complexContent>
</complexType>
```



