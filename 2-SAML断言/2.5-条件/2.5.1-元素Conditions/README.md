---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 2.5.1 元素\<Conditions\>


元素\<Conditions\>可能包含下列元素和属性：

+ NotBefore [可选]

指定了SAML断言生效的最早的时间。时间是UTC格式，正如1.3.3章节中所描述的那样。

+ NotOnOrAfter [可选]

指定了SAML断言的过期时间，等于或者超过这个时间，则断言失效。时间是UTC格式，正如1.3.3章节中所描述的那样。

+ \<Condition\> [任意数量]

在扩展schema中定义的类型的条件。```xsi:type```属性必须用来指定实际的条件类型。

+ \<AudienceRestriction\> [任意数量]

声明断言是颁发给指定的受众的。

+ \<OneTimeUse\> [可选]

指定断言应该立刻被使用，而不能留着等待将来使用。虽然schema允许出现多次，但实际此元素最多只能有一个实例。

+ \<ProxyRestriction\> [可选]

指定断言方对“希望随后自己充当断言方并根据原始断言中包含的信息发布自己的断言的”依赖方施加的限制。虽然schema允许出现多次，但实际此元素最多只能有一个实例。

> 译者（义臻）注：即，如果一个依赖方希望根据断言方发过来的断言信息封装并发布自己的断言，此参数用户对其施加限制。此时依赖方有点像“中间商”。

因为使用```xsi:type```属性将允许断言包含多个SAML定义的ConditionType子类型的实例（例如OneTimeUseType），因此schema并不会显式的限制可以包含特定条件的次数。如上所示，特定类型的条件可以定义对此类型使用的限制。

下面的schema片段定义了\<Conditions\>元素和他的复杂类型ConditionsType。

```xml
<element name="Conditions" type="saml:ConditionsType"/>
<complexType name="ConditionsType">
    <choice minOccurs="0" maxOccurs="unbounded">
        <element ref="saml:Condition"/>
        <element ref="saml:AudienceRestriction"/>
        <element ref="saml:OneTimeUse"/>
        <element ref="saml:ProxyRestriction"/>
    </choice>
    <attribute name="NotBefore" type="dateTime" use="optional"/>
    <attribute name="NotOnOrAfter" type="dateTime" use="optional"/>
</complexType>
```


