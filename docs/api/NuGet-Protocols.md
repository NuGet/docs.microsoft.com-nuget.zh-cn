---
title: nuget.org 协议
description: 要与 NuGet 客户端交互的不断发展 nuget.org 协议。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547268"
---
# <a name="nugetorg-protocols"></a>nuget.org 协议

若要与 nuget.org 进行交互，客户端需要遵守某些协议。 由于这些协议，让不断演变，客户端必须标识调用特定 nuget.org Api 时，它们使用的协议版本。 这样，nuget.org 的旧客户端不间断的方式引入的更改。

> [!Note]
> 此页上所述的 Api 是特定于 nuget.org 并且没有任何其他 NuGet 服务器上实现来引入这些 Api 的假定条件。 

有关在 NuGet 生态系统中实施广泛 NuGet API 的信息，请参阅[API 概述](overview.md)。

本主题列出了作为各种协议和时它们可以直接对存在。

## <a name="nuget-protocol-version-410"></a>NuGet 协议版本 4.1.0

4.1.0 协议指定验证范围密钥与 nuget.org 中，若要验证包对 nuget.org 帐户以外的服务进行交互的用法。 请注意，`4.1.0`数目是不透明的字符串，但恰好官方 NuGet 客户端支持此协议的第一个版本的版本。

验证可确保用户创建 API 密钥仅用于 nuget.org 中，并通过使用一次验证作用域键处理该验证或通过第三方服务的验证。 这些验证范围密钥可以用于验证包属于 nuget.org 上的特定用户 （帐户）。

### <a name="client-requirement"></a>客户端要求

要求客户端时它们向发出 API 调用传递以下标头**推送**到 nuget.org 的包：

    X-NuGet-Protocol-Version: 4.1.0

请注意，`X-NuGet-Client-Version`标头具有类似语义，但将其保留仅供官方 NuGet 客户端。 第三方客户端应使用`X-NuGet-Protocol-Version`标头和值。

**推送**协议本身中的文档所述[`PackagePublish`资源](package-publish-resource.md)。

如果客户端与外部服务，需要验证是否属于特定用户 （帐户） 的包进行交互，它应使用以下协议，并使用作用域的验证密钥和不从 nuget.org 的 API 密钥。

### <a name="api-to-request-a-verify-scope-key"></a>API 请求作用域的验证密钥

此 API 用于获取 nuget.org 作者可以验证拥有的他/她的包的作用域的验证密钥。

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>请求参数

name           | 内     | 类型   | 必需 | 说明
-------------- | ------ | ------ | -------- | -----
Id             | URL    | 字符串 | 是      | 为其请求验证作用域键包 identidier
VERSION        | URL    | 字符串 | 否       | 包版本
X-NuGet-ApiKey | Header | 字符串 | 是      | 例如，`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>响应

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>若要验证验证作用域键的 API

此 API 用于验证归 nuget.org 作者的包的作用域的验证密钥。

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>请求参数

name           | 内     | 类型   | 必需 | 说明
-------------  | ------ | ------ | -------- | -----
Id             | URL    | 字符串 | 是      | 为其请求验证作用域键包标识符
VERSION        | URL    | 字符串 | 否       | 包版本
X-NuGet-ApiKey | Header | 字符串 | 是      | 例如，`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此验证作用域 API 密钥将在某一天的时间后过期，或在首次使用准。

#### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
200         | API 密钥无效
403         | API 密钥是无效或未授权，以对包推送
404         | 由包引用`ID`和`VERSION`（可选） 不存在
