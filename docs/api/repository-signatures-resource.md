---
title: 存储库签名，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存储库签名资源允许客户端包源公布其存储库签名功能。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775328"
---
# <a name="repository-signatures"></a>存储库签名

如果包源支持将存储库签名添加到已发布的包，客户端可能会确定包源使用的签名证书。 此资源可让客户端检测存储库签名包是否已被篡改或是否有意外的签名证书。

用于获取此存储库签名信息的资源是 `RepositorySignatures` 在 [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值                | 说明
-------------------------- | -----
RepositorySignatures/4.7.0 | 初始版本
RepositorySignatures/4.9。0 | NuGet v 4.9 + 客户端支持
RepositorySignatures/5.0。0 | 允许启用 `allRepositorySigned` 。 由 NuGet 版本 5.0 + 客户端支持

## <a name="base-url"></a>基 URL

以下 Api 的入口点 URL 是 `@id` 与上述资源值关联的属性的值 `@type` 。 本主题使用占位符 URL `{@id}` 。

请注意，与其他资源不同， `{@id}` 需要通过 HTTPS 提供 URL。

## <a name="http-methods"></a>HTTP 方法

存储库签名资源中的所有 Url 仅支持 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="repository-signatures-index"></a>存储库签名索引

存储库签名索引包含两条信息：

1. 源中找到的所有包是否均为此包源签名的存储库。
1. 包源用于对包进行签名的证书列表。

在大多数情况下，证书列表仅会附加到。 当以前的签名证书已过期，并且包源需要使用新的签名证书开始时，将向列表中添加新证书。 如果从列表中删除了证书，则表示使用已删除签名证书创建的所有包签名都不应再被客户端视为有效。 在这种情况下，包签名 (，但不一定包) 无效。 客户端策略可能允许将包安装为无符号。

如果证书吊销 (例如密钥泄漏) ，则包源应对受影响证书签名的所有包进行重新签名。 此外，包源还应从签名证书列表中删除受影响的证书。

以下请求将获取存储库签名索引。

```
GET {@id}
```

存储库签名索引是一个 JSON 文档，其中包含具有以下属性的对象：

名称                | 类型             | 必须 | 注释
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 是      | 必须 `false` 在4.7.0 和4.9.0 资源上
signingCertificates | 对象数组 | 是      | 

`allRepositorySigned`如果包源包含某些没有存储库签名的包，则将该布尔值设置为 false。 如果布尔值设置为 true，则源上可用的所有包都必须具有存储库签名，该签名由中提到的一个签名证书生成 `signingCertificates` 。

> [!Warning]
> 对于 `allRepositorySigned` 4.7.0 和4.9.0 资源，布尔值必须为 false。 NuGet 4.7 4.7、med-v 和 v 4.9 客户端无法从设置为 true 的源安装包 `allRepositorySigned` 。

`signingCertificates`如果 `allRepositorySigned` 布尔值设置为 true，则在数组中应该有一个或多个签名证书。 如果数组为空且 `allRepositorySigned` 设置为 true，则源中的所有包都应视为无效，不过，客户端策略可能仍允许使用包。 此数组中的每个元素都是具有以下属性的 JSON 对象。

名称         | 类型   | 必须 | 注释
------------ | ------ | -------- | -----
contentUrl   | string | 是      | DER 编码的公共证书的绝对 URL
指纹 | object | 是      |
subject      | string | 是      | 证书中的使用者可分辨名称
颁发者       | string | 是      | 证书颁发者的可分辨名称
notBefore    | string | 是      | 证书有效期的开始时间戳
notAfter     | string | 是      | 证书有效期的结束时间戳

请注意， `contentUrl` 需要通过 HTTPS 进行服务。 此 URL 没有特定的 URL 模式，必须使用此存储库签名索引文档动态发现它。 

此对象中 (除了) 之外的所有属性都 `contentUrl` 必须从找到的证书中名称可以 `contentUrl` 。
提供这些名称可以属性是为了最大程度地减少往返行程。

`fingerprints` 对象具有以下属性：

名称                   | 类型   | 必须 | 注释
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | 是      | SHA-256 指纹

密钥名称 `2.16.840.1.101.3.4.2.1` 是 SHA-256 哈希算法的 OID。

所有哈希值必须为哈希摘要的十六进制编码字符串表示形式。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
