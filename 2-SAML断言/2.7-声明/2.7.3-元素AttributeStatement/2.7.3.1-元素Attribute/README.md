---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.7.3.1 元素\<Attribute\>

\<Attribute\>元素通过名称标识属性，并可在其中包含它的值。它是```AttributeType```复杂类型。它用于在一个属性声明中表达与断言主体相关的特定属性及其值，如上一节所述。该元素还被用在属性查询中以请求返回特定SAML属性的值（可以在3.3.2.3中看到更多信息）。\<Attribute\>元素包含下列的XML属性：

+ Name [必须]

属性的名字。

+ NameFormat [可选]

表示属性名称分类的URI引用，用于解释名称。可以参阅第8.2 节去了解一些可用作```NameFormat```属性值的URI引用及其相关的描述和处理规则。如果没有提供```NameFormat```的值，则默认使用标识符```urn:oasis:names:tc:SAML:2.0:attrname-format:unspecified```（参见第 8.2.1 节）。

+ FriendlyName [可选]

一个字符串，它提供了更易于阅读的属性名称形式，这在实际属性名称很复杂或不透明的情况下会很有用，例如属性名称是OID或UUID的情况。该属性的值不得用作正式标识SAML属性的基准。

+ Arbitrary attributes

该复杂类型使用\<xs:anyAttribute\>扩展点以允许将任意的的XML属性添加到\<Attribute\>结构中，而无需进行显式的schema扩展。这使得可以按需的添加其他字段，以提供要使用的其他参数，例如，在属性查询中。SAML扩展不得向```AttributeType```复杂类型及其派生类型中添加本地（非命名空间限定的）的XML属性或由SAML定义的命名空间限定的XML属性。SAML自身保留这样的属性以用作将来的维护或者扩展。

+ \<AttributeValue\> [任意数量]

包含属性的值。如果一个属性包含多个离散值，则推荐把每个值都放到单独的\<AttributeValue\>元素中。如果一个属性中包含了不止一个\<AttributeValue\>元素，并且每个\<AttributeValue\>元素都通过```xsi:type```分配了数据类型，那么这些\<AttributeValue\>元素都必须是相同的数据类型。

不包含\<AttributeValue\>元素的\<Attribute\>元素的含义取决于其上下文。在\<AttributeStatement\>中，如果SAML属性存在但是没有值的话，那么需要省略\<AttributeValue\>元素。在\<samlp:AttributeQuery\>元素中，缺少值表示请求者对任何或所有命名属性的值感兴趣（另请参见第3.3.2.3节）。

由配置文件或其他规范对\<Attribute\>元素指定的任何其他引用，都必须定义指定或省略\<AttributeValue\>元素的语义。

下列的schema片段定义了\<Attribute\>元素以及它的```AttributeType```复杂类型：

```xml
<element name="Attribute" type="saml:AttributeType"/>
<complexType name="AttributeType">
    <sequence>
        <element ref="saml:AttributeValue" minOccurs="0" maxOccurs="unbounded"/>
    </sequence>
    <attribute name="Name" type="string" use="required"/>
    <attribute name="NameFormat" type="anyURI" use="optional"/>
    <attribute name="FriendlyName" type="string" use="optional"/>
    <anyAttribute namespace="##other" processContents="lax"/>
</complexType>
```