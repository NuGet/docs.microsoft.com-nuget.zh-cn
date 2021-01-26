---
title: nuget.org 协议
description: 用于与 NuGet 客户端进行交互的演变 nuget.org 协议。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773975"
---
# <a name="nugetorg-protocols"></a>nuget.org 协议

若要与 nuget.org 交互，客户端需要遵循某些协议。 由于这些协议不断发展，因此客户端必须在调用特定的 nuget.org Api 时标识它们使用的协议版本。 这允许 nuget.org 为旧客户端引入非重大的更改。

> [!Note]
> 本页面上所述的 Api 特定于 nuget.org，并且不希望其他 NuGet 服务器实现引入这些 Api。 

有关在 NuGet 生态系统中广泛实现的 NuGet API 的信息，请参阅 [API 概述](overview.md)。

本主题列出了各种协议，无论它们何时存在都是如此。

## <a name="nuget-protocol-version-410"></a>NuGet 协议版本4.1。0

4.1.0 协议指定使用验证作用域密钥与 nuget.org 以外的服务进行交互，以针对 nuget.org 帐户验证包。 请注意， `4.1.0` 版本号是不透明的字符串，但会与支持此协议的第一个正式 NuGet 客户端版本一致。

验证可确保用户创建的 API 密钥仅与 nuget.org 一起使用，并且第三方服务的其他验证或验证是通过一次性使用验证-作用域密钥来处理的。 可以使用这些验证作用域密钥来验证包是否属于特定用户 (帐户) nuget.org 上。

### <a name="client-requirement"></a>客户端要求

当客户端进行 API 调用以将包 **推送** 到 nuget.org 时，需要客户端传递以下标头：

```
X-NuGet-Protocol-Version: 4.1.0
```

请注意， `X-NuGet-Client-Version` 标头具有相似的语义，但保留为仅供官方 NuGet 客户端使用。 第三方客户端应使用 `X-NuGet-Protocol-Version` 标头和值。

[ `PackagePublish` 资源](package-publish-resource.md)的文档中描述了 **推送** 协议本身。

如果客户端与外部服务进行交互，并且需要验证包是否属于特定用户 (帐户) ，则它应使用以下协议，并使用 nuget.org 中的验证作用域密钥而不是 API 密钥。

### <a name="api-to-request-a-verify-scope-key"></a>用于请求验证作用域密钥的 API

此 API 用于获取 nuget.org 作者验证范围的密钥，以便验证其拥有的包。

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>请求参数

名称           | In     | 类型   | 必须 | 注释
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 是      | 为其请求验证作用域密钥的包 identidier
VERSION        | URL    | string | 否       | 包版本
X-NuGet-ApiKey | 标头 | string | 是      | 例如： `X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>响应

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>用于验证验证作用域密钥的 API

此 API 用于验证 nuget.org 作者拥有的包的验证范围键。

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>请求参数

名称           | In     | 类型   | 必须 | 注释
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | 是      | 为其请求验证作用域密钥的包标识符
VERSION        | URL    | string | 否       | 包版本
X-NuGet-ApiKey | 标头 | string | 是      | 例如： `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此验证作用域 API 密钥会在一天的时间或第一次使用时过期，以先发生的情况为准。

#### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
200         | API 密钥有效
403         | API 密钥无效或无权推送包
404         | 由引用的包 `ID` 和 `VERSION` (可选) 不存在
