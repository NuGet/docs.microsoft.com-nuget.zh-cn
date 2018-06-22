---
title: NuGet API 的概述
description: NuGet API 是一组可用于下载包，提取元数据，发布新的包等的 HTTP 终结点。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a638dba005c14bff4b2e668e2d6ca527a67b94a9
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819996"
---
# <a name="nuget-api"></a>NuGet API

NuGet API 是一套用于下载包、 提取元数据、 发布新的程序包和执行大多数官方 NuGet 客户端中提供其他操作的 HTTP 终结点。

在 Visual Studio、 nuget.exe 和.NET CLI NuGet 客户端使用此 API 执行 NuGet 操作如[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)，在 Visual Studio UI 中，搜索和[ `nuget.exe push` ](../tools/cli-ref-push.md)。

请注意，在某些情况下，nuget.org 具有由其他包源中不强制执行的附加要求。 这些差异记录通过[nuget.org 协议](nuget-protocols.md)。

## <a name="service-index"></a>服务索引

API 的入口点是一个已知位置中的 JSON 文档。 此文档被称为**服务索引**。 Nuget.org 的服务索引的位置是`https://api.nuget.org/v3/index.json`。

此 JSON 文档包含的列表*资源*其提供不同的功能和满足不同用例。

支持 API 的客户端应接受一个或多个这些服务索引 URL 作为连接到相应的程序包源的方法。

服务索引有关的详细信息，请参阅[其 API 参考](service-index.md)。

## <a name="versioning"></a>版本管理

API 是 NuGet 的 HTTP 协议版本 3。 此协议有时称为"V3 API。" 这些引用文档将引用到此版本的协议，只需作为"API。"

服务索引架构版本将由`version`服务索引中的属性。 API 规定的版本字符串有的一个主要版本号`3`。 对服务索引架构进行非重大更改时，将增加的版本字符串的次要版本。

旧版客户端 (如 nuget.exe 2.x) 不支持 V3 API，并仅支持较旧的 V2 API 未在此处介绍。

因为它是 V2 API 的后继版本这是由官方 NuGet 客户端 2.x 版本实现的基于 OData 的协议，因此命名 NuGet V3 API。 V3 API 首先受正式 NuGet 客户端的 3.0 版本和仍的最新主要协议版本支持通过 NuGet 客户端，4.0，在。 

第一次发布以来，对 API 进行了非重大协议更改。

## <a name="resources-and-schema"></a>资源和架构

**服务索引**介绍各种资源。 当前的受支持的资源集如下所示：

资源名称                                                          | 必需 | 描述
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 是      | 推送和删除 （或不列出） 包。
[`SearchQueryService`](search-query-service-resource.md)               | 是      | 筛选器和搜索的关键字的包。
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 是      | 获取包元数据。
[`PackageBaseAddress`](package-base-address-resource.md)               | 是      | 获取包的内容 (.nupkg)。
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | 否       | 按子字符串中发现的包 Id 和版本。
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | 否       | 构造访问"报告滥用行为"网页的 URL。
[`Catalog`](catalog-resource.md)                                       | 否       | 所有包事件的完整记录。

一般情况下，使用 JSON API 资源返回的所有非二进制数据进行序列化。 为该资源，分别定义了返回服务索引中每个资源的响应架构。 有关每个资源的详细信息，请参阅上面列出的主题。

> [!Note]
> 当源不实现`SearchAutocompleteService`应正常禁用任何自动完成行为。 当`ReportAbuseUriTemplate`未实现，则正式的 NuGet 客户端回退到 nuget.org 的报告滥用行为 URL (通过跟踪[NuGet/主页 #4924](https://github.com/NuGet/Home/issues/4924))。 其他客户端可以选择只是不向用户显示报表滥用行为 URL。

## <a name="timestamps"></a>时间戳

API 返回的所有时间戳是 UTC，或使用否则指定[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表示形式。 

## <a name="http-methods"></a>HTTP 方法

谓词   | 使用
------ | -----------
GET    | 执行只读操作，通常检索数据。
HEAD   | 提取相应的响应标头`GET`请求。
PUT    | 创建的资源不存在，或如果文件确实存在，更新它。 某些资源可能不支持更新。
DELETE | 删除或 unlists 资源。

## <a name="http-status-codes"></a>HTTP 状态代码

代码 | 描述
---- | -----
200  | 如果成功，并且没有响应正文。
201  | 已创建成功后和资源。
202  | 成功后，请求已被接受，但某些工作仍可能不完整和已完成以异步方式。
204  | 如果成功，但没有任何响应正文。
301  | 永久重定向。
302  | 临时重定向。
400  | 在 URL 中或在请求正文中的参数不是有效的。
401  | 提供的凭据均无效。
403  | 给定提供的凭据不允许操作。
404  | 请求的资源不存在。
409  | 与现有资源的请求冲突。
500  | 服务遇到意外的错误。
503  | 该服务是暂时不可用。

任何`GET`向 API 终结点发出的请求可能返回的 HTTP 重定向 （301 或 302）。 客户端应通过观察正常处理此类重定向`Location`标头和正在发送后续`GET`。 有关特定终结点的文档将不显式调出可能使用重定向的位置。

对于 500 级别状态代码，客户端可以实现合理的重试机制。 官方 NuGet 客户端重试三次时遇到任何 500 级别状态代码或 TCP/DNS 错误。

## <a name="http-request-headers"></a>HTTP 请求标头

名称                     | 描述
------------------------ | -----------
X-NuGet-ApiKey           | 所需的推送和删除，请参阅[`PackagePublish`资源](package-publish-resource.md)
X-NuGet-Client-Version   | **弃用**和替换为 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 在某些情况下，仅在 nuget.org 上的需要，请参阅[nuget.org 协议](NuGet-Protocols.md)
X-NuGet-Session-Id       | *可选*。 NuGet 客户端 v4.7 + 标识属于同一 NuGet 客户端会话的 HTTP 请求。 有关`PackageReference`存在还原操作是否为单个会话 id，其他情况下自动完成，如和`packages.config`还原可能有几个不同的会话 id 的由于代码被分解的因子。

## <a name="authentication"></a>身份验证

身份验证都留给要定义的包源实现。 Nuget.org，仅为`PackagePublish`资源需要身份验证通过特殊的 API 密钥标头。 请参阅[`PackagePublish`资源](package-publish-resource.md)有关详细信息。
