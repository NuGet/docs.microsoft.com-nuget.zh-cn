---
title: 推送符号包，NuGet API |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 发布服务允许客户端发布新的符号包。
keywords: NuGet API 推送符号包
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580410"
---
# <a name="push-symbol-packages"></a>推送符号包

可以将包推送符号 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用 NuGet V3 API。
这些操作所基于的中断`SymbolPackagePublish`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                 | 说明
--------------------        | -----
SymbolPackagePublish/4.9.0  | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是的值`@id`的属性`SymbolPackagePublish/4.9.0`包源中的资源[服务索引](service-index.md)。 以下文档中，使用 nuget.org 的 URL。 请考虑`https://www.nuget.org/api/v2/symbolpackage`作为占位符`@id`服务索引中找到的值。

## <a name="http-methods"></a>HTTP 方法

`PUT`此资源是否支持 HTTP 方法。 

## <a name="push-a-symbol-package"></a>推送符号包

nuget.org 支持推送新的符号包格式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 使用以下 API。 

    PUT https://www.nuget.org/api/v2/symbolpackage

可以多次提交具有同一 ID 和版本的符号包。 在以下情况下，符号包将被拒绝。
- 具有相同的 ID 和版本的包不存在。
- 具有相同的 ID 和版本的符号包已推送，但尚未发布。
- 符号包 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) 是无效的 (请参阅[符号包约束](../create-packages/Symbol-Packages-snupkg.md))。

### <a name="request-parameters"></a>请求参数

name           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | 字符串 | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

API 密钥是从包源获得由用户和配置到客户端不透明的字符串。 强制要求任何特定字符串格式，但 API 密钥的长度不应超过合理的大小，为 HTTP 标头值。

### <a name="request-body"></a>请求正文

符号推送的请求正文是与包推送请求的请求正文 (请参阅[打包推送和删除](package-publish-resource.md))。 

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
201         | 已成功推送符号包。
400         | 提供的符号包无效。
401         | 用户无权执行此操作。
404         | 具有提供的 ID 和版本的相应包不存在。
409         | 已推送符号包具有提供的 ID 和版本，但尚不可用。
413         | 包是太大。

