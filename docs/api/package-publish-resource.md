---
title: 推送和删除，NuGet API
description: 发布服务允许客户端发布新包，并取消列出或删除现有包。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773920"
---
# <a name="push-and-delete"></a>推送和删除

使用 NuGet V3 API，可以推送、删除 (或取消列出，具体取决于服务器实现) 和重新列出包。 这些操作基于 `PackagePublish` 在 [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值          | 说明
-------------------- | -----
PackagePublish/2.0。0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是 `@id` `PackagePublish/2.0.0` 包源的 [服务索引](service-index.md)中资源的属性的值。 对于以下文档，使用 nuget 的 URL。 请考虑 `https://www.nuget.org/api/v2/package` `@id` 在服务索引中找到的值的占位符。

请注意，此 URL 指向与旧版 V2 推送终结点相同的位置，因为协议是相同的。

## <a name="http-methods"></a>HTTP 方法

`PUT` `POST` `DELETE` 此资源支持、和 HTTP 方法。 对于每个终结点支持的方法，请参阅下面的。

## <a name="push-a-package"></a>推送包

> [!Note]
> nuget.org 具有与推送终结点交互的 [其他要求](NuGet-Protocols.md) 。

nuget.org 支持使用以下 API 推送新包。 如果已存在具有提供的 ID 和版本的包，则 nuget.org 将拒绝推送。 其他包源可能支持替换现有包。

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>请求参数

名称           | In     | 类型   | 必须 | 注释
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | 标头 | string | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}`

API 密钥是用户从包源中获得的不透明字符串，配置到客户端。 不会强制执行任何特定的字符串格式，但 API 密钥的长度不应超过 HTTP 标头值的合理大小。

### <a name="request-body"></a>请求正文

请求正文必须采用以下形式：

#### <a name="multipart-form-data"></a>多部分表单数据

请求标头 `Content-Type` 为 `multipart/form-data` ，而请求正文中的第一项是所推送的 nupkg 的原始字节。 多部分正文中的后续项将被忽略。 将忽略多部分项目的文件名或任何其他标头。

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
201、202    | 已成功推送包
400         | 提供的包无效
409         | 具有提供的 ID 和版本的包已存在

服务器实现不同于成功推送包时返回的成功状态代码。

## <a name="delete-a-package"></a>删除包

nuget.org 将包删除请求解释为 "取消列出"。 这意味着包对于包的现有使用者仍可用，但包不再显示在搜索结果或 web 界面中。 有关此操作的详细信息，请参阅 [已删除的包](../nuget-org/policies/deleting-packages.md) 策略。 其他服务器实现可随意将此信号解释为硬删除、软删除或取消列出。 例如， [NuGet. server](https://www.nuget.org/packages/NuGet.Server) (服务器实现仅支持旧版 V2 API) 支持将此请求作为基于配置选项的取消列出或硬删除进行处理。

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>请求参数

名称           | In     | 类型   | 必须 | 注释
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 是      | 要删除的包的 ID
VERSION        | URL    | string | 是      | 要删除的包的版本
X-NuGet-ApiKey | 标头 | string | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
204         | 已删除包
404         | 未提供 `ID` 和存在具有的 `VERSION` 包

## <a name="relist-a-package"></a>重新列出包

如果未列出某个包，则可以使用 "重新列出" 终结点将该包再次显示在搜索结果中。 此终结点与 [delete (取消列出) 终结点](#delete-a-package) 具有相同的形状，但使用 `POST` HTTP 方法而不是 `DELETE` 方法。

如果包已列出，请求仍会成功。

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>请求参数

名称           | In     | 类型   | 必须 | 注释
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 是      | 要重新列出的包的 ID
VERSION        | URL    | string | 是      | 要重新列出的包的版本
X-NuGet-ApiKey | 标头 | string | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
200         | 现在会列出此包
404         | 未提供 `ID` 和存在具有的 `VERSION` 包
