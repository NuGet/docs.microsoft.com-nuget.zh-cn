---
title: 搜索，NuGet API
description: 搜索服务允许客户端按关键字查询包，并筛选某些包字段的结果。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235126"
---
# <a name="search"></a>搜索

可以使用 V3 API 搜索包源上可用的包。 用于搜索的资源是在`SearchQueryService` [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本管理

使用以下`@type`值：

@type 值                   | 说明
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-beta | 别名`SearchQueryService`
SearchQueryService/3.0.0-rc   | 别名`SearchQueryService`

## <a name="base-url"></a>基 URL

以下 API 的基 URL 是与上述某个资源`@id` `@type`值关联的属性的值。 在下面的文档中，将使用占位符`{@id}`基 URL。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。

## <a name="search-for-packages"></a>搜索包

搜索 API 允许客户端查询与指定的搜索查询匹配的包页面。 搜索查询（如搜索词的词汇切分）的解释由服务器实现确定，但一般的期望是搜索查询用于匹配包 Id、标题、说明和标记。 还可以考虑其他包元数据字段。

未列出的包决不会出现在搜索结果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

name        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 否       | 用于筛选包的搜索词
skip        | URL    | integer | 否       | 要跳过的结果数，用于分页
长        | URL    | integer | 否       | 要返回的结果数，用于分页
早期  | URL    | boolean | 否       | `true`或`false`确定是否包括[预发布包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 否       | SemVer 1.0.0 版本字符串 

搜索查询`q`按服务器实现所定义的方式进行分析。 nuget.org 支持针对[各种字段](../consume-packages/finding-and-choosing-packages.md#search-syntax)的基本筛选。 如果未`q`提供，则应在 skip 和 take 施加的边界内返回所有包。 这会启用 NuGet Visual Studio 体验中的 "浏览" 选项卡。

`skip`参数默认为0。

`take`参数应为大于零的整数。 服务器实现可能会施加最大值。

如果`prerelease`未提供，则将排除预发布包。

Query 参数用于选择[SemVer 2.0.0 包。](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
如果此查询参数被排除，则将仅返回 SemVer 1.0.0 兼容版本的包（其中包含[标准 NuGet 版本控制](../concepts/package-versioning.md)注意事项，如具有4个整数部分的版本字符串）。
如果`semVerLevel=2.0.0`提供了，则将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。 有关详细信息，请参阅[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

### <a name="response"></a>响应

响应是最多`take`包含搜索结果的 JSON 文档。 搜索结果按包 ID 分组。

根 JSON 对象具有以下属性：

name      | 类型             | 必填 | 说明
--------- | ---------------- | -------- | -----
totalHits | integer          | 是      | 匹配项的总数， `skip`忽略和`take`
数据      | 对象数组 | 是      | 请求匹配的搜索结果

### <a name="search-result"></a>搜索结果

`data`数组中的每一项都是一个 JSON 对象，其中包含一组共享同一包 ID 的包版本。
对象具有以下属性：

name           | 类型                       | 必填 | 说明
-------------- | -------------------------- | -------- | -----
id             | string                     | 是      | 匹配包的 ID
version        | string                     | 是      | 包的完整 SemVer 2.0.0 版本字符串（可能包含生成元数据）
description    | string                     | 否       | 
版本       | 对象数组           | 是      | 与`prerelease`参数匹配的包的所有版本
作者        | 字符串或字符串数组 | 否       | 
iconUrl        | string                     | 否       | 
licenseUrl     | string                     | 否       | 
所有者         | 字符串或字符串数组 | 否       | 
projectUrl     | string                     | 否       | 
注册   | string                     | 否       | 关联[注册索引](registration-base-url-resource.md#registration-index)的绝对 URL
摘要        | string                     | 否       | 
标记           | 字符串或字符串数组 | 否       | 
标题          | string                     | 否       | 
totalDownloads | integer                    | 否       | 此值可由`versions`数组中的下载内容和
得到       | boolean                    | 否       | 一个 JSON 布尔值，指示是否[验证](../nuget-org/id-prefix-reservation.md)了包

在 nuget.org 上，已验证的包是指其包 ID 与保留的 ID 前缀匹配并由保留前缀的一个所有者拥有的包 ID。 有关详细信息，请参阅[有关 ID 前缀保留的文档](../reference/id-prefix-reservation.md)。

搜索结果对象中包含的元数据取自最新的包版本。 `versions`数组中的每一项都是具有以下属性的 JSON 对象：

name      | 类型    | 必需 | 说明
--------- | ------- | -------- | -----
@id       | string  | 是      | 关联[注册叶](registration-base-url-resource.md#registration-leaf)的绝对 URL
version   | string  | 是      | 包的完整 SemVer 2.0.0 版本字符串（可能包含生成元数据）
下载 | integer | 是      | 此特定包版本的下载数

### <a name="sample-request"></a>示例请求

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>示例响应

[!code-JSON [search-result.json](./_data/search-result.json)]
