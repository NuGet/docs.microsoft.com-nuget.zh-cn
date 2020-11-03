---
title: NuGet 服务器 API 概述
description: NuGet 服务器 API 是一组 HTTP 终结点，可用于下载包、提取元数据、发布新包等。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: aacf56a5dc5af9abf6f60d42bc7fd530a128d0d8
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237804"
---
# <a name="nuget-server-api"></a>NuGet 服务器 API

NuGet 服务器 API 是一组 HTTP 终结点，可用于下载包、提取元数据、发布新包以及执行官方 NuGet 客户端中提供的大多数其他操作。

此 API 由 NuGet 客户端在 Visual Studio 中使用，nuget.exe 和 .NET CLI 来执行 NuGet 操作 [`dotnet restore`](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) ，例如，在 Visual STUDIO UI 中搜索和 [`nuget.exe push`](../reference/cli-reference/cli-ref-push.md) 。

请注意，在某些情况下，nuget.org 具有其他包源未强制执行的其他要求。 [Nuget.org 协议](nuget-protocols.md)记录了这些差异。

有关可用 nuget.exe 版本的简单枚举和下载，请参阅终结点 [ 上的tools.js](tools-json.md) 。

## <a name="service-index"></a>服务索引

该 API 的入口点是众所周知的位置中的 JSON 文档。 此文档称为 **服务索引** 。 Nuget.org 的服务索引的位置为 `https://api.nuget.org/v3/index.json` 。

此 JSON 文档包含资源列表，这些 *资源* 提供不同的功能并实现不同的用例。

支持 API 的客户端应接受一个或多个服务索引 URL 作为连接到相应包源的方法。

有关服务索引的详细信息，请参阅 [它的 API 参考](service-index.md)。

## <a name="versioning"></a>版本控制

API 是 NuGet 的 HTTP 协议的版本3。 此协议有时称为 "V3 API"。 这些参考文档将此版本的协议称为 "API"。

服务索引架构版本由 `version` 服务索引中的属性表示。 API 规定版本字符串具有的主要版本号 `3` 。 由于对服务索引架构进行了非重大更改，将增加版本字符串的次要版本。

旧客户端 (如 nuget.exe 2.x) 不支持 V3 API，并且仅支持旧版 V2 API，此处未介绍。

NuGet V3 API 命名为，因为它是 V2 API 的后续版本，后者是基于 OData 的协议，该协议是由8.x 版的官方 NuGet 客户端实现的。 第一版的官方 NuGet 客户端3.0 支持 V3 API，但它仍然是 NuGet 客户端、4.0 和上支持的最新主要协议版本。 

自首次发布以来，已对 API 进行了非重大协议更改。

## <a name="resources-and-schema"></a>资源和架构

**服务索引** 描述了各种资源。 当前支持的资源集如下所示：

资源名称                                                        | 必须 | 说明
-------------------------------------------------------------------- | -------- | -----------
[目录](catalog-resource.md)                                       | 否       | 所有包事件的完整记录。
[PackageBaseAddress](package-base-address-resource.md)               | 是      | )  ( 获取包内容。
[PackageDetailsUriTemplate](package-details-template-resource.md)    | 否       | 构造用于访问包详细信息网页的 URL。
[PackagePublish](package-publish-resource.md)                        | 是      | 推送和删除 (或取消列出) 包。
[RegistrationsBaseUrl](registration-base-url-resource.md)            | 是      | 获取包元数据。
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | 否       | 构造用于访问报表滥用网页的 URL。
[RepositorySignatures](repository-signatures-resource.md)            | 否       | 获取用于存储库签名的证书。
[SearchAutocompleteService](search-autocomplete-service-resource.md) | 否       | 按子字符串发现包 Id 和版本。
[SearchQueryService](search-query-service-resource.md)               | 是      | 按关键字筛选和搜索包。
[SymbolPackagePublish](symbol-package-publish-resource.md)           | 否       | 推送符号包。

通常，API 资源返回的所有非二进制数据都使用 JSON 进行序列化。 服务索引中每个资源返回的响应架构分别为该资源定义。 有关每个资源的详细信息，请参阅上面列出的主题。

将来，随着协议的发展，可能会向 JSON 响应中添加新的属性。 为了使客户端能够进行进一步的验证，实现不应假定响应架构是最终的，不能包含额外的数据。 应忽略实现不理解的所有属性。

> [!Note]
> 当源未实现时， `SearchAutocompleteService` 应妥善禁用自动完成行为。 当 `ReportAbuseUriTemplate` 未实现时，官方 nuget 客户端将回退到 nuget。通过 [Nuget/Home # 4924](https://github.com/NuGet/Home/issues/4924)) 进行跟踪，组织的报表滥用 URL (。 其他客户端可能选择只是不向用户显示报表滥用 URL。

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org 上未记录的资源

Nuget.org 上的 V3 服务索引有一些未在上面列出的资源。 不记录资源的原因有很多。

首先，我们不会将使用的资源记录为 nuget.org 的实现细节。 `SearchGalleryQueryService` 属于此类别。 [NuGetGallery](https://github.com/NuGet/NuGetGallery) 使用此资源将某些 V2 (OData) 查询委托给搜索索引，而不是使用数据库。 之所以引入此资源是为了实现可伸缩性的原因，不能供外部使用。

其次，我们不会记录从未在官方客户端 RTM 版本中提供的资源。
`PackageDisplayMetadataUriTemplate` 并 `PackageVersionDisplayMetadataUriTemplate` 属于此类别。

脾气，我们不会记录与 V2 协议紧密耦合的资源，这本身就是有意未记录的。 `LegacyGallery`资源属于此类别。 此资源允许 V3 服务索引指向相应的 V2 源 URL。 此资源支持 `nuget.exe list` 。

如果此处未记录资源， *强烈* 建议您不要对其进行依赖。 我们可能会删除或更改这些未记录资源的行为，这些资源可能会以意外的方式中断您的实现。

## <a name="timestamps"></a>时间戳

API 返回的所有时间戳均为 UTC，或者使用 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 表示形式指定。 

## <a name="http-methods"></a>HTTP 方法

谓词   | 用途
------ | -----------
GET    | 执行只读操作，通常检索数据。
HEAD   | 获取相应请求的响应标头 `GET` 。
PUT    | 创建不存在的资源，如果该资源存在，则将其更新。 某些资源可能不支持更新。
DELETE | 删除或取消列出资源。

## <a name="http-status-codes"></a>HTTP 状态代码

代码 | 说明
---- | -----
200  | 成功，并且存在响应正文。
201  | 成功，并创建了资源。
202  | 成功，请求已被接受，但一些工作可能仍未完成并以异步方式完成。
204  | 成功，但没有响应正文。
301  | 永久性重定向。
302  | 临时重定向。
400  | URL 或请求正文中的参数无效。
401  | 提供的凭据无效。
403  | 给定提供的凭据不允许执行该操作。
404  | 请求的资源不存在。
409  | 请求与现有资源冲突。
500  | 服务遇到意外错误。
503  | 该服务暂时不可用。

对 `GET` API 终结点发出的任何请求可能会返回 HTTP 重定向 (301 或 302) 。 客户端应通过观察 `Location` 标头并发出后续的来正常处理此类重定向 `GET` 。 与特定终结点相关的文档将不会显式调用可以使用重定向的位置。

对于500级别的状态代码，客户端可以实现合理的重试机制。 如果遇到任何500级状态代码或 TCP/IP 错误，官方 NuGet 客户端将重试三次。

## <a name="http-request-headers"></a>HTTP 请求标头

名称                     | 说明
------------------------ | -----------
X-NuGet-ApiKey           | 需要进行推送和删除，请参阅[ `PackagePublish` 资源](package-publish-resource.md)
X-NuGet-客户端版本   | **弃用** 并替换 `X-NuGet-Protocol-Version`
X-NuGet-协议版本 | 仅在某些情况下在 nuget.org 上是必需的，请参阅 [nuget.org 协议](NuGet-Protocols.md)
X-NuGet-会话 Id       | 可选。 NuGet 客户端 4.7 + 识别属于同一 NuGet 客户端会话的 HTTP 请求。

`X-NuGet-Session-Id`对于与中的单个还原相关的所有操作，都有一个值 `PackageReference` 。 对于其他方案，如 "自动完成" 和 "还原"， `packages.config` 可能有几个不同的会话 ID，原因是代码的分解方式。

## <a name="authentication"></a>身份验证

身份验证留给包源实现定义。 对于 nuget.org，只有 `PackagePublish` 资源需要通过一个特殊 API 密钥标头进行身份验证。 有关详细信息，请参阅[ `PackagePublish` 资源](package-publish-resource.md)。
