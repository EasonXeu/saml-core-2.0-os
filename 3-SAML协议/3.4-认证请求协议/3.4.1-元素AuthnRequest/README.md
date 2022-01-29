---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 3.4.1 元素\<AuthnRequest\>

为了请求身份提供商发布一个包含认证声明的断言，请求提出方（```presenter```）向身份提供商认证其自身（或依赖于现有的安全上下文）并向其发送一个\<AuthnRequest\>消息以描述生成的断言满足其目的所需要的属性。这些属性中，可能是与断言的内容有关的信息，也可能是生成的\<Response\>消息应以何种方式转发给请求方（```request```）的信息。请求提出方（```presenter```）的身份认证过程可以在\<AuthnRequest\>消息的初始传递之前、期间或之后进行。

请求方（```request```）可能和请求的提出方（```presenter```）是不同的，例如，如果请求方是一个想要使用结果断言来对被请求主体进行身份验证或授权的依赖方，以便依赖方可以决定是否提供服务。

\<AuthnRequest\>消息应该被签名，或者被转发这个消息的协议绑定进行身份认证和完整性保护。

\<AuthnRequest\>消息是```AuthnRequestType```复杂类型，它继承自```RequestAbstractType```类型，并添加了以下元素和属性，这些元素和属性通常都是可选的，但可能被特定的配置文件所必需：

+ \<saml:Subject\> [可选]

指定结果断言中的被请求主体。可以包含一个或多个\<saml:SubjectConfirmation\>元素以说明生成的断言是被谁以及通过何种方式确认的。可以在2.4节中查看更多的信息。

如果此元素被完全省略或者没有包含标识符，那么就假定消息的提出方是被请求的主体。如果不包含\<saml:SubjectConfirmation\>元素，那么就假定消息的提出方是需要的唯一进行证明的实体，且证明的方法是由身份提供商的使用配置和策略来说明。

+ \<NameIDPolicy\> [可选]

指定对用来代表被请求主体的名称标识符的约束限制。如果省略，那么就可以使用身份提供商支持被请求主体使用的、又或者受任何相关部署特定策略约束的任何标识符类型，比如，涉及隐私的标识符类型。

+ \<saml:Conditions\> [可选]

指定请求者希望限制结果断言的有效性或使用场景的SAML条件。响应者可在其认为必要时修改或补充该集合。该元素中的信息被用作构建断言过程的输入，而不是作为使用请求本身的条件。（关于此元素的更多信息，可以参考2.5章节）

+ \<RequestedAuthnContext\> [可选]

指定请求者对认证上下文的要求（如果有），该认证上下文用于响应提供者对请求提出者的认证过程中。可在3.3.2.2.1章节中找到有关该元素的处理规则。

+ \<Scoping\> [可选]

指定一系列被请求者信任的身份提供商以对请求提出者进行身份认证，以及与响应者如何将\<AuthnRequest\>消息代理给后续身份提供商有关的限制和上下文。

+ ForceAuthn [可选]

一个布尔值。如果是```true```，身份提供商必须直接对请求提出方进行身份认证，而不是依赖之前的安全上下文。如果没有指定该值的话，默认值是```false```。然而，如果```ForceAuthn```和```IsPassive```同时为```true```的话，那么身份提供商不得对请求提出者进行身份认证，除非满足```iPassive```的限制。

+ IsPassive [可选]

一个布尔值。如果是```true```，身份提供者和用户代理UA本身不得明显地从控制请求者的用户界面，并以明显的方式与请求提出方进行交互。如果没有指定该值的话，默认值是```false```。

+ AssertionConsumerServiceIndex [可选]

间接地说明\<Response\>消息应返回给请求者的地址。它仅适用于请求者与提出者不同的场景，例如[SAMLProf]中的Web浏览器SSO场景。身份提供商必须有可靠的方法将属性中的索引值映射到与请求者关联的地址上。[SAMLMeta]提供了一种可能的机制。如果省略的话，那么身份提供者必须将\<Response\>消息返回到与请求者相关联的默认地址。如果指定的索引不合法，那么身份提供商可以返回一个错误的\<Response\>消息，或者使用默认的地址。 此属性与```AssertionConsumerServiceURL```属性和```ProtocolBinding```属性互斥。

+ AssertionConsumerServiceURL [可选]

通过值来指定\<Response\>消息必须返回给请求者的地址。响应者必须通过某种方式确保指定的值实际上是与请求者关联在一起的。[SAMLMeta]提供了一种可能的机制。将对应的\<AuthnRequest\>消息进行签名是另一种机制。此属性与```AssertionConsumerServiceIndex```属性互斥，并且通常和```ProtocolBinding```属性一起出现。

+ ProtocolBinding [可选]

一个URI引用，用于标识返回\<Response\>消息时要使用的SAML协议绑定。有关协议绑定和为其定义的URI引用的更多信息，可以参见[SAMLBind]。此属性与```AssertionConsumerServiceIndex```属性互斥，并且通常和```AssertionConsumerServiceURL```属性一起出现。

+ AttributeConsumingServiceIndex [可选]

间接地标识了与请求者相关的消息（描述请求者希望或要求身份提供者在\<Response\>消息中提供的SAML属性）。身份提供商必须有可靠的方法将属性中的索引值映射到与请求者关联的信息上。[SAMLMeta]提供了一种可能的机制。身份提供商可以使用此信息在其返回的断言中填充一个或多个\<saml:AttributeStatement\>元素。

+ ProviderName [可选]

指定请求者的可读名称，以供提出者的用户代理（UA）或身份提供商使用。

有关此消息的一般处理规则，请参见第3.4.1.4节。

下列的schema片段定义了\<AuthnRequest\>元素和它的```AuthnRequestType```复杂类型：

```xml
<element name="AuthnRequest" type="samlp:AuthnRequestType"/>
<complexType name="AuthnRequestType">
    <complexContent>
        <extension base="samlp:RequestAbstractType">
            <sequence>
                <element ref="saml:Subject" minOccurs="0"/>
                <element ref="samlp:NameIDPolicy" minOccurs="0"/>
                <element ref="saml:Conditions" minOccurs="0"/>
                <element ref="samlp:RequestedAuthnContext" minOccurs="0"/>
                <element ref="samlp:Scoping" minOccurs="0"/>
            </sequence>
            <attribute name="ForceAuthn" type="boolean" use="optional"/>
            <attribute name="IsPassive" type="boolean" use="optional"/>
            <attribute name="ProtocolBinding" type="anyURI" use="optional"/>
            <attribute name="AssertionConsumerServiceIndex" type="unsignedShort" use="optional"/>
            <attribute name="AssertionConsumerServiceURL" type="anyURI" use="optional"/>
            <attribute name="AttributeConsumingServiceIndex" type="unsignedShort" use="optional"/>
            <attribute name="ProviderName" type="string" use="optional"/>
        </extension>
    </complexContent>
</complexType>
```