---
title: 推送符号包，NuGet API |Microsoft Docs
author: cristinamanum
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
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235104"
---
# <a name="push-symbol-packages"></a>推送符号包

可以使用 NuGet V3 API 推送符号包（[snupkg](../create-packages/Symbol-Packages-snupkg.md)）。
这些操作基于`SymbolPackagePublish`在[服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本管理

使用以下`@type`值：

@type 值                 | 说明
--------------------        | -----
SymbolPackagePublish/4.9。0  | 初始版本

## <a name="base-url"></a>基 URL

以下 api 的基 URL 是包源的[服务索引](service-index.md)中`@id` `SymbolPackagePublish/4.9.0`资源的属性的值。 对于以下文档，使用 nuget 的 URL。 请`https://www.nuget.org/api/v2/symbolpackage`考虑在服务索引中`@id`找到的值的占位符。

## <a name="http-methods"></a>HTTP 方法

此资源支持 HTTP 方法。 `PUT` 

## <a name="push-a-symbol-package"></a>推送符号包

nuget.org 支持使用以下 API 推送新的符号包格式（[snupkg](../create-packages/Symbol-Packages-snupkg.md)）。 

    PUT https://www.nuget.org/api/v2/symbolpackage

可以多次提交具有相同 ID 和版本的符号包。 在以下情况下，将拒绝符号包。
- ID 和版本相同的包不存在。
- 已推送具有相同 ID 和版本的符号包，但尚未发布。
- 符号包（[snupkg](../create-packages/Symbol-Packages-snupkg.md)）无效（请参阅[符号包约束](../create-packages/Symbol-Packages-snupkg.md)）。

### <a name="request-parameters"></a>请求参数

name           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

API 密钥是用户从包源中获得的不透明字符串，配置到客户端。 不会强制执行任何特定的字符串格式，但 API 密钥的长度不应超过 HTTP 标头值的合理大小。

### <a name="request-body"></a>请求正文

符号推送的请求正文与包推送请求的请求正文相同（请参阅[包推送和删除](package-publish-resource.md)）。 

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
201         | 已成功推送符号包。
400         | 提供的符号包无效。
401         | 用户无权执行此操作。
404         | 具有提供的 ID 和版本的对应包不存在。
409         | 已推送具有提供的 ID 和版本的符号包，但它尚不可用。
413         | 包太大。

