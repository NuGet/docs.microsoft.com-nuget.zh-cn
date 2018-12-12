---
title: 存储库签名，NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: 存储库签名资源允许客户端包源地宣布其签名功能的存储库。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248437"
---
# <a name="repository-signatures"></a>存储库签名

如果包源支持添加存储库发布的包签名，就可以确定所用的包源的签名证书的客户端。 此资源允许客户端以检测包是否已签名的存储库已被篡改或包含意外的签名证书。

此存储库签名信息中提取的使用的资源是`RepositorySignatures`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                | 说明
-------------------------- | -----
RepositorySignatures/4.7.0 | 初始版本
RepositorySignatures/4.9.0 | 允许启用 `allRepositorySigned`

## <a name="base-url"></a>基 URL

以下 Api 的入口点 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。 本主题使用占位符 URL `{@id}`。

请注意，与其他资源不同`{@id}`URL，才能通过 HTTPS 提供服务。

## <a name="http-methods"></a>HTTP 方法

在存储库签名资源支持的 HTTP 方法中找到的所有 Url`GET`和`HEAD`。

## <a name="repository-signatures-index"></a>存储库签名索引

存储库签名索引包含两条信息：

1. 所有包源上可以都找到的是受此包的来源签署的存储库。
1. 包源来进行包所用证书的列表。

在大多数情况下，证书的列表将只会追加到。 以前的签名证书已过期，但包源需要开始使用新的签名证书时，会将新证书添加到列表。 如果从列表中删除证书，这意味着，使用已删除的签名证书创建的所有包签名应不再被都视为有效客户端。 在这种情况下，包的签名 （但不是一定是包） 是无效的。 客户端策略可能会允许安装未签名包。

在证书吊销 （例如密钥泄漏） 的情况下应将包的源文件重新签名由受影响的证书签名的所有包。 此外，包源应从签名的证书列表中删除受影响的证书。

以下请求获取存储库签名索引。

    GET {@id}

存储库签名索引是包含具有以下属性的对象的 JSON 文档：

name                | 类型             | 必需 | 说明
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 是      | 必须为`false`上 4.7.0 资源
signingCertificates | 对象的数组 | 是      | 

`allRepositorySigned`布尔值设置为 false，如果包源具有一些具有任何存储库的签名的包。 如果布尔值设置为 true，可在上找到的所有包源必须由其中一个签名证书中所述的存储库签名`signingCertificates`。

> [!Warning]
> `allRepositorySigned`布尔值必须为假上 4.7.0 资源。 NuGet v4.7 和 v4.8 客户端不能从具有的源安装包`allRepositorySigned`设置为 true。

应在一个或多个签名证书`signingCertificates`数组如果`allRepositorySigned`布尔值设置为 true。 如果数组为空并`allRepositorySigned`设置为 true，来自源的所有包应都视为无效，尽管客户端策略可能仍允许使用包。 此数组中的每个元素均具有以下属性的 JSON 对象。

name         | 类型   | 必需 | 说明
------------ | ------ | -------- | -----
contentUrl   | 字符串 | 是      | 绝对 URL 的 DER 编码的公用证书
指纹 | object | 是      |
主题      | 字符串 | 是      | 从证书使用者可分辨的名称
issuer       | 字符串 | 是      | 证书的颁发者的可分辨的名称
notBefore    | 字符串 | 是      | 证书的有效期的起始时间戳
notAfter     | 字符串 | 是      | 证书的有效期的结束时间戳

请注意，`contentUrl`需要通过 HTTPS 提供服务。 此 URL 具有任何特定的 URL 模式，并且必须使用此存储库签名索引文档动态地发现。 

此对象中的所有属性 (除了`contentUrl`) 必须是从证书，请参阅派生`contentUrl`。
为方便起见，尽量减少往返过程提供了这些派生的属性。

`fingerprints`对象具有以下属性：

name                   | 类型   | 必需 | 说明
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | 字符串 | 是      | SHA-256 指纹

密钥名称`2.16.840.1.101.3.4.2.1`是 SHA-256 哈希算法的 OID。

所有哈希值必须为小写字符、 十六进制编码的字符串表示形式的哈希摘要。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
