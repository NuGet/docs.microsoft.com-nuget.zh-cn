---
title: nuget.org 协议
description: 不断发展与 NuGet 客户端交互 nuget.org 协议。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: cc6d52617ea8b69d5b18b831ddf8a1a85dd6798f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822573"
---
# <a name="nugetorg-protocols"></a>nuget.org 协议

若要与 nuget.org 进行交互，客户端需要遵循某些协议。 由于这些协议保留在发展，客户端必须标识调用特定 nuget.org Api 时，他们使用的协议版本。 这允许 nuget.org 的旧客户端的非换行方式引入的更改。

> [!Note]
> 此页上介绍的 Api 是特定于 nuget.org 并且没有其他的 NuGet 服务器实现引入这些 Api 不期望。 

有关 NuGet API 实现广泛整个 NuGet 生态系统的信息，请参阅[API 概述](overview.md)。

本主题列出为各种协议和当到达存在。

## <a name="nuget-protocol-version-410"></a>所需的 NuGet 协议版本 4.1.0

4.1.0 协议指定的作用域验证密钥与除 nuget.org，若要验证针对 nuget.org 帐户之外的服务进行交互的用法。 请注意，`4.1.0`版本数是不透明的字符串，但不会支持此协议的官方 NuGet 客户端的第一个版本保持一致。

验证确保用户创建 API 密钥仅用于 nuget.org，并通过一次使用验证范围密钥处理该验证或从第三方服务的验证。 这些验证范围密钥可以用于验证包属于 nuget.org 上的特定用户 （帐户）。

### <a name="client-requirement"></a>客户端要求

要求客户端传递以下标头，当他们开展 API 调用发布到**推送**nuget.org 的包：

    X-NuGet-Protocol-Version: 4.1.0

请注意，`X-NuGet-Client-Version`标头具有相似的语义，但已保留以仅供官方 NuGet 客户端。 第三方客户端应使用`X-NuGet-Protocol-Version`标头和值。

**推送**协议本身中的文档所述[`PackagePublish`资源](package-publish-resource.md)。

如果客户端与外部服务，需要验证是否属于特定用户 （帐户） 的包交互时，它应使用以下协议，并使用作用域的验证密钥和不从 nuget.org 的 API 密钥。

### <a name="api-to-request-a-verify-scope-key"></a>API 来请求作用域的验证密钥

此 API 用于获取 nuget.org 作者，以验证归他/她的包的作用域的验证密钥。

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
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

此 API 用于验证包归 nuget.org 作者作用域的验证密钥。

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>请求参数

名称           | 内     | 类型   | 必需 | 说明
-------------  | ------ | ------ | -------- | -----
Id             | URL    | 字符串 | 是      | 为其请求验证作用域键包标识符
VERSION        | URL    | 字符串 | 否       | 包版本
X-NuGet-ApiKey | Header | 字符串 | 是      | 例如，`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> 此验证作用域 API 密钥将在一天的时间之后过期或首次使用，无论哪个操作发生第一次。

#### <a name="response"></a>响应

状态代码 | 含义
----------- | -------
200         | API 密钥是有效
403         | API 密钥是无效或未授权推送对包
404         | 引用包`ID`和`VERSION`（可选） 不存在
