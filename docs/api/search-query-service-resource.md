---
title: 搜索，NuGet API
description: 搜索服务允许客户端按关键字查询包，并筛选某些包字段的结果。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7047dfd48b7f93756bbb1491de1b7e65da2c12b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775410"
---
# <a name="search"></a>搜索

可以使用 V3 API 搜索包源上可用的包。 用于搜索的资源是 `SearchQueryService` 在 [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值                   | 说明
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-beta | 别名 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 别名 `SearchQueryService`
SearchQueryService/3.5。0      | 支持 `packageType` 查询参数

### <a name="searchqueryservice350"></a>SearchQueryService/3.5。0
此版本引入了对 `packageType` 查询参数和 `packageTypes` response 属性的支持，允许按作者定义的包类型进行筛选。 它完全向后兼容的查询 `SearchQueryService` 。

## <a name="base-url"></a>基 URL

以下 API 的基 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。 在下面的文档中，将使用占位符基 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 Url 都支持 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="search-for-packages"></a>搜索包

搜索 API 允许客户端查询与指定的搜索查询匹配的包页面。 搜索查询的解释 (例如，搜索词的标记) 由服务器实现确定，但一般情况下，搜索查询用于匹配包 Id、标题、说明和标记。 还可以考虑其他包元数据字段。

未列出的包决不会出现在搜索结果中。

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>请求参数

名称        | In     | 类型    | 必须 | 注释
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 否       | 用于筛选包的搜索词
skip        | URL    | integer | 否       | 要跳过的结果数，用于分页
take        | URL    | integer | 否       | 要返回的结果数，用于分页
prerelease  | URL    | boolean | 否       | `true` 或 `false` 确定是否包括 [预发布包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 否       | SemVer 1.0.0 版本字符串 
packageType | URL    | string  | 否       | 用于筛选包的包类型 (添加到 `SearchQueryService/3.5.0`) 

搜索查询按 `q` 服务器实现所定义的方式进行分析。 nuget.org 支持针对 [各种字段](../consume-packages/finding-and-choosing-packages.md#search-syntax)的基本筛选。 如果未 `q` 提供，则应在 skip 和 take 施加的边界内返回所有包。 这会启用 NuGet Visual Studio 体验中的 "浏览" 选项卡。

`skip`参数默认为0。

`take`参数应为大于零的整数。 服务器实现可能会施加最大值。

如果 `prerelease` 未提供，则将排除预发布包。

`semVerLevel`Query 参数用于选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查询参数，则将仅返回 SemVer 1.0.0 兼容版本的包， (带有 [标准 NuGet 版本控制](../concepts/package-versioning.md) 注意事项，如) 的4个整数部分的版本字符串。
如果 `semVerLevel=2.0.0` 提供了，则将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。 有关详细信息，请参阅 [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

`packageType`参数用于进一步筛选搜索结果，使其仅包含至少一个与包类型名称匹配的包类型的包。
如果所提供的包类型不是 [包类型文档](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)定义的有效包类型，将返回一个空结果。
如果提供的包类型为空，则不会应用任何筛选器。 换言之，不将值传递给 packageType 参数的行为就像未传递参数一样。

### <a name="response"></a>响应

响应是最多包含搜索结果的 JSON 文档 `take` 。 搜索结果按包 ID 分组。

根 JSON 对象具有以下属性：

名称      | 类型             | 必须 | 注释
--------- | ---------------- | -------- | -----
totalHits | integer          | 是      | 匹配项的总数，忽略 `skip` 和 `take`
data      | 对象数组 | 是      | 请求匹配的搜索结果

### <a name="search-result"></a>搜索结果

数组中的每一项 `data` 都是一个 JSON 对象，其中包含一组共享同一包 ID 的包版本。
该对象包含以下属性：

名称           | 类型                       | 必须 | 注释
-------------- | -------------------------- | -------- | -----
id             | string                     | 是      | 匹配包的 ID
版本        | string                     | 是      | 包 (的完整 SemVer 2.0.0 版本字符串可以包含生成元数据) 
description    | string                     | 否       | 
versions       | 对象数组           | 是      | 与参数匹配的包的所有版本 `prerelease`
作者        | 字符串或字符串数组 | 否       | 
iconUrl        | string                     | 否       | 
licenseUrl     | string                     | 否       | 
所有者         | 字符串或字符串数组 | 否       | 
projectUrl     | string                     | 否       | 
注册   | string                     | 否       | 关联[注册索引](registration-base-url-resource.md#registration-index)的绝对 URL
摘要        | string                     | 否       | 
标记           | 字符串或字符串数组 | 否       | 
title          | string                     | 否       | 
totalDownloads | integer                    | 否       | 此值可由数组中的下载内容和 `versions`
得到       | boolean                    | 否       | 一个 JSON 布尔值，指示是否[验证](../nuget-org/id-prefix-reservation.md)了包
packageTypes   | 对象数组           | 是      | 包作者定义的包类型 (添加到 `SearchQueryService/3.5.0`) 

在 nuget.org 上，已验证的包是指其包 ID 与保留的 ID 前缀匹配并由保留前缀的一个所有者拥有的包 ID。 有关详细信息，请参阅 [有关 ID 前缀保留的文档](../nuget-org/id-prefix-reservation.md)。

搜索结果对象中包含的元数据取自最新的包版本。 数组中的每一项 `versions` 都是具有以下属性的 JSON 对象：

名称      | 类型    | 必须 | 注释
--------- | ------- | -------- | -----
@id       | string  | 是      | 关联[注册叶](registration-base-url-resource.md#registration-leaf)的绝对 URL
版本   | string  | 是      | 包 (的完整 SemVer 2.0.0 版本字符串可以包含生成元数据) 
downloads | integer | 是      | 此特定包版本的下载数

`packageTypes`数组始终包含至少一个 (1) 项。 给定包 ID 的包类型被认为是由最新版本的包（与其他搜索参数有关）定义的包类型。 数组中的每一项 `packageTypes` 都是具有以下属性的 JSON 对象：

名称      | 类型    | 必须 | 说明
--------- | ------- | -------- | -----
name      | string  | 是      | 包类型的名称。

### <a name="sample-request"></a>示例请求

```
GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0
```

### <a name="sample-response"></a>示例响应

[!code-JSON [search-result.json](./_data/search-result.json)]