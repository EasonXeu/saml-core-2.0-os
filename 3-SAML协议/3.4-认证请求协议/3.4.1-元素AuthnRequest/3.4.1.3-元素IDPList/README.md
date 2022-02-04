---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 3.4.1.3 元素\<IDPList\>

\<IDPList\>元素指定了受请求者信任的身份提供商，以认证请求提出者的身份。它是```IDPListType```复杂类型，该类型定义了下列元素：

+ \<IDPEntry\> [一个或更多]

关于单个的身份提供商的信息。

+ \<GetComplete\> [可选]

如果\<IDPList\>不完整，则可以使用此元素来指定一个URI引用，以检索完整的列表。检索与URI关联的资源必须产生一个XML实例，其根元素是本身不包含\<GetComplete\>元素的\<IDPList\>。

下列的schema片段定义了\<IDPList\>元素和它的```IDPListType```复杂类型：

```xml
<element name="IDPList" type="samlp:IDPListType"/>
<complexType name="IDPListType">
    <sequence>
        <element ref="samlp:IDPEntry" maxOccurs="unbounded"/>
        <element ref="samlp:GetComplete" minOccurs="0"/>
    </sequence>
</complexType>
<element name="GetComplete" type="anyURI"/>
```