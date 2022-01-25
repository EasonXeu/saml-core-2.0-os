---
description: 本博客采用知识共享署名 4.0 国际许可协议进行许可
---

# 4 SAML版本管理

SAML规范集有两种独立的版本控制方式。本章会就每一种方式进行讨论，也会讨论检测和处理版本差异的处理规则。此外，还将讨论何时以及为何具体的版本信息要在本规范的未来版本中更改。

当使用主要版本（Major）和次要版本（Minor）来表达版本信息时，我们采用```Major.Minor```的格式。版本号```MajorB.MinorB```高于版本号```MajorA.MinorA```，需要满足下列条件：

> (MajorB > MajorA) OR ((MajorB = MajorA) AND (MinorB > MinorA))
