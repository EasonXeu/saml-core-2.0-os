---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 3.6 名称标识符管理协议

为身份主体建立名称标识符之后，如果身份提供商希望更改其在引用主体时将使用的标识符的值或格式，或者希望提示某名称标识符将不再用于某身份主体，那么可以通过向服务提供商发送\<ManageNameIDRequest\>消息来通知该更改。

服务提供商还使用此消息注册或更改在使用基础名称标识符与其进行通信时要包含的SPProviderId值，或者是终止在其与身份提供商之间使用该名称标识符。

注意，此协议通常不与```transient```类型的名称标识符一起使用，因为这种类型的名称标识符本来就不打算长期管理。

