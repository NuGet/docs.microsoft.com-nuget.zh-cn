---
title: NuGet API 的概述
description: NuGet API 是一组 HTTP 终结点，可用于下载包，提取元数据，将发布新的包，等等。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 770173d6b84048cf42a5da46cbc474d8cf604a08
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547498"
---
# <a name="nuget-api"></a>NuGet API

NuGet API 是一组可用于下载包、 提取元数据、 将发布新的包，并执行大多数官方 NuGet 客户端中提供其他操作的 HTTP 终结点。

在 Visual Studio、 nuget.exe 和.NET CLI 中的 NuGet 客户端使用此 API 来执行 NuGet 操作，如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜索并[ `nuget.exe push` ](../tools/cli-ref-push.md)。

请注意，在某些情况下，nuget.org 具有由其他包源中不强制执行的附加要求。 这些差异记录通过[nuget.org 协议](nuget-protocols.md)。

简单枚举和可用 nuget.exe 版本的下载，请参阅[tools.json](tools-json.md)终结点。

## <a name="service-index"></a>服务索引

适用于 API 的入口点是一个已知位置中的 JSON 文档。 本文档名为**服务索引**。 Nuget.org 的服务索引的位置是`https://api.nuget.org/v3/index.json`。

此 JSON 文档包含一系列*资源*它提供不同的功能并满足不同的用例。

支持 API 的客户端应接受一个或多个这些服务索引 URL 作为连接到相应的程序包源的方式。

有关服务索引的详细信息，请参阅[其 API 参考](service-index.md)。

## <a name="versioning"></a>版本管理

该 API 是 NuGet 的 HTTP 协议版本 3。 此协议有时称为"V3 API。" 这些引用文档将引用到此版本的协议，简称为"API。"

指示服务索引的架构版本`version`服务索引中的属性。 API 要求的版本字符串有主版本号的`3`。 服务索引架构做出非重大更改后，会增加版本字符串的次要版本。

较旧的客户端 (如 nuget.exe 2.x) 不支持 V3 API，并仅支持较旧的 V2 API，本文未提供。

因为它是后一 V2 API，这是由 2.x 版的官方 NuGet 客户端实现的基于 OData 的协议，这种情况下命名 NuGet V3 API。 V3 API 首先受官方 NuGet 客户端的 3.0 版本和仍的主要协议最新版本支持通过 NuGet 客户端，4.0 和上。 

第一次发布以来，对 API 进行了非重大协议更改。

## <a name="resources-and-schema"></a>资源和架构

**服务索引**介绍了各种资源。 当前的受支持的资源集如下所示：

资源名称                                                          | 必需 | 描述
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 是      | 推送和删除 （或取消列出） 包。
[`SearchQueryService`](search-query-service-resource.md)               | 是      | 筛选器和搜索的关键字的包。
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 是      | 获取包元数据。
[`PackageBaseAddress`](package-base-address-resource.md)               | 是      | 获取包的内容 (.nupkg)。
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 否       | 发现的子字符串的包 Id 和版本。
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 否       | 构造一个 URL 以访问"报告滥用行为"网页。
[`RepositorySignatures`](repository-signatures-resource.md)            | 否       | 获取用于存储库签名的证书。
[`Catalog`](catalog-resource.md)                                       | 否       | 包的所有事件的完整记录。

一般情况下，使用 JSON API 资源返回的所有非二进制数据进行序列化。 该资源的单独定义的服务索引的每个资源返回的响应架构。 有关每个资源的详细信息，请参阅上面列出的主题。

> [!Note]
> 当源不实现`SearchAutocompleteService`应适当地禁用任何自动完成行为。 当`ReportAbuseUriTemplate`未实现，正式的 NuGet 客户端回退到 nuget.org 的报告滥用 URL (通过跟踪[NuGet/Home #4924](https://github.com/NuGet/Home/issues/4924))。 其他客户端可以选择只是不向用户显示报告滥用 URL。

## <a name="timestamps"></a>时间戳

API 返回的所有时间戳采用 UTC，或使用否则指定[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示形式。 

## <a name="http-methods"></a>HTTP 方法

谓词   | 使用
------ | -----------
GET    | 执行只读操作，通常检索数据。
HEAD   | 提取相应的响应标头`GET`请求。
PUT    | 创建一个资源不存在，或如果文件确实存在，对其进行更新。 某些资源可能不支持更新。
DELETE | 删除或取消列出资源。

## <a name="http-status-codes"></a>HTTP 状态代码

代码 | 描述
---- | -----
200  | 如果成功，并且没有响应正文。
201  | 已创建成功后和资源。
202  | 如果成功，该请求已被接受，但一些工作仍可能是不完整且已完成以异步方式。
204  | 如果成功，但没有任何响应正文。
301  | 永久重定向。
302  | 临时重定向。
400  | 在 URL 中或在请求正文中的参数不是有效的。
401  | 所提供的凭据均无效。
403  | 给定所提供的凭据不允许操作。
404  | 请求的资源不存在。
409  | 请求与现有资源冲突。
500  | 服务遇到意外的错误。
503  | 此服务暂时不可用。

任何`GET`对 API 终结点发出的请求可能返回的 HTTP 重定向 （301 或 302）。 客户端应适当地处理这种重定向通过观察`Location`标头和发出的后续`GET`。 有关特定终结点的文档将不显式调用重定向可能会派上用场。

对于一个 500 级状态代码和客户端可以实现合理的重试机制。 官方 NuGet 客户端时，重试三次遇到任何 500 级状态代码或 TCP/DNS 错误。

## <a name="http-request-headers"></a>HTTP 请求标头

name                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 所需的推送和删除，请参阅[`PackagePublish`资源](package-publish-resource.md)
X-NuGet-Client-Version   | **不推荐使用**并替换为 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 在某些情况下，仅在 nuget.org 上必需的请参阅[nuget.org 协议](NuGet-Protocols.md)
X-NuGet-Session-Id       | *可选*。 NuGet 客户端 v4.7 + 标识属于同一个 NuGet 客户端会话的 HTTP 请求。 有关`PackageReference`存在还原操作是单个会话 id，对于其他方案，如自动完成，和`packages.config`还原可能有几个不同的会话 id 的由于代码构造的方式。

## <a name="authentication"></a>身份验证

身份验证应由要定义的包源实现。 对于 nuget.org，仅`PackagePublish`资源需要通过特殊的 API 密钥标头的身份验证。 请参阅[`PackagePublish`资源](package-publish-resource.md)有关详细信息。
