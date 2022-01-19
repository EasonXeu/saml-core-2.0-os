---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 3.2.2 复杂类型StatusResponseType

所有SAML响应都是派生自```StatusResponseType```复杂类型的类型。此类型定义与所有SAML响应关联的公共属性和元素：

+ ID [必须]

SAML响应的标识符。它是```xs:ID```类型，并且必须遵循第1.3.4节中规定的标识符唯一性要求。

+ InResponseTo [可选]

如果响应不是为响应请求而生成的，或者如果无法确定请求的ID属性值（例如，请求格式不正确），则该属性一定不能存在。否则，它必须存在，并且和相应SAML请求的ID属性值相匹配。

+ Version [必须]

响应的版本号。本规范中定义的SAML版本的标识符为“2.0”。SAML版本控制在第4节中讨论。

+ IssueInstant [必须]

生成SAML响应的时间。该时间是UTC格式，符合1.3.3部分中的描述。

+ Destination [可选]

一个URI引用，指示当前响应要发送到哪个地址。这有助于防止恶意的将响应转发给非预期收件人，这是被某些协议绑定所要求的保护机制。如果该属性存在，那么实际的接受者必须验证URI引用所指代的地址就是实际接收消息的地址。如果该属性不存在，那么响应必须被丢弃。一些协议绑定可能要求使用这个属性（参考[SAMLBind]）。

+ Consent [可选]

说明在发送此响应时是否（以及在何种条件下）获得委托人的同意。可以在8.4节找到一些可能被用作```Consent```属性值的URI引用及其相关描述。如果```Consent```属性值不存在，那么默认使用```urn:oasis:names:tc:SAML:2.0:consent:unspecified```标识符（参考8.4.1部分）。

+ \<saml:Issuer\> [可选]

指示生成SAML响应的实体（可以参考2.2.5节查看更多该元素的信息）。

+ \<ds:Signature\> [可选]

验证请求者并提供消息完整性的XML签名，如后面第5节所述。


+ \<Extensions\> [可选]

此扩展点包含通信双方商定的可选的协议消息扩展元素。使用此扩展点不需要任何扩展schema，即便提供了扩展schema，宽松的验证设置也不要求扩展一定是有效的。SAML扩展元素必须在非SAML定义的命名空间中进行命名空间限定。

+ \<Status\> [必须]

表示相应请求状态的编码。

根据特定协议或概要文件的要求，SAML响应者通常需要验证自身，通常可能需要消息完整性。认证性和消息完整性可以由协议绑定提供的机制提供（请参见[SAMLBind]）。SAML响应可能会被签名，签名可以提供认证性和消息完整性。

如果使用了这样的签名，那么\<ds:Signature\>元素就必须存在，并且收到该响应的SAML请求者就必须根据[XMLSig]规范验证签名是合法的（即信息没有被篡改）。如果签名无效，那么请求者不能依赖于响应的内容，并且应该将其视为一个错误。如果签名合法，那么请求者应该评估签名，以决定签名者的身份与适当性，并可继续处理其认为适当的响应。

如果包含```Consent```属性，并且其值指示已经获得了依赖方的某种同意，那么响应就应该被签名。

下列的schema片段定义了```StatusResponseType```复杂类型：

```
<complexType name="StatusResponseType">
    <sequence>
        <element ref="saml:Issuer" minOccurs="0"/>
        <element ref="ds:Signature" minOccurs="0"/>
        <element ref="samlp:Extensions" minOccurs="0"/>
        <element ref="samlp:Status"/>
    </sequence>
    <attribute name="ID" type="ID" use="required"/>
    <attribute name="InResponseTo" type="NCName" use="optional"/>
    <attribute name="Version" type="string" use="required"/>
    <attribute name="IssueInstant" type="dateTime" use="required"/>
    <attribute name="Destination" type="anyURI" use="optional"/>
    <attribute name="Consent" type="anyURI" use="optional"/>
</complexType>
```


