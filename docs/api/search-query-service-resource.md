---
title: 搜索，NuGet API
description: 搜索服务允许客户端查询按关键字的包和包的某些字段上的筛选器结果。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d462b289c39c2dd1418304dabcad47d0d4217f82
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426736"
---
# <a name="search"></a>搜索

就可以搜索使用 V3 API 的包源上可用的包。 用于搜索的资源是`SearchQueryService`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                   | 说明
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-beta | 别名 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 别名 `SearchQueryService`

## <a name="base-url"></a>基 URL

以下 API 的基 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。 在以下文档中，占位符基 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。

## <a name="search-for-packages"></a>搜索包

搜索 API 允许查询到的客户端的包指定的搜索查询匹配的一个页面。 搜索查询 （例如搜索词的词汇切分） 解释由服务器实现，但一般预期结果是，使用搜索查询匹配的包 Id、 标题、 说明和标记。 也可以考虑使用其他包元数据字段。

取消列出的包应永远不会出现在搜索结果。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

名称        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 否       | 搜索条款，用于筛选器包
skip        | URL    | 整数 | 否       | 要分页的跳过的结果数
Take        | URL    | 整数 | 否       | 要为分页返回的结果数
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 否       | SemVer 1.0.0 版本字符串 

搜索查询`q`分析由服务器实现定义的方式。 nuget.org 支持在基本筛选[各种字段](../consume-packages/finding-and-choosing-packages.md#search-syntax)。 如果没有`q`提供应返回所有包，施加的 skip 和 take 的边界内。 这样，NuGet Visual Studio 体验中的"浏览"选项卡。

`skip`参数默认值为 0。

`take`参数应为大于零的整数。 服务器实现可能会施加最大值。

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用来选择中加入[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 (与[standard 的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，例如使用 4 个整数部分的版本字符串)。
如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是 JSON 文档，其中最多包含`take`搜索结果。 搜索结果进行分组的包 id。

根 JSON 对象具有以下属性：

名称      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
totalHits | 整数          | 是      | 匹配项，而不考虑总数`skip`和 `take`
数据      | 对象的数组 | 是      | 由请求匹配的搜索结果

### <a name="search-result"></a>搜索结果

中的每项`data`数组是组成一组共享相同的包 id。 包版本的 JSON 对象
该对象具有以下属性：

名称           | 类型                       | 必需 | 说明
-------------- | -------------------------- | -------- | -----
id             | string                     | 是      | 匹配的包的 ID
version        | string                     | 是      | （可能包含生成元数据） 的包的完整的 SemVer 2.0.0 版本字符串
说明    | string                     | 否       | 
版本       | 对象的数组           | 是      | 所有匹配的包版本`prerelease`参数
作者        | 字符串或字符串数组 | 否       | 
iconUrl        | string                     | 否       | 
licenseUrl     | string                     | 否       | 
所有者         | 字符串或字符串数组 | 否       | 
projectUrl     | string                     | 否       | 
注册   | string                     | 否       | 到关联的绝对 URL[注册索引](registration-base-url-resource.md#registration-index)
摘要        | string                     | 否       | 
标记           | 字符串或字符串数组 | 否       | 
标题          | string                     | 否       | 
totalDownloads | 整数                    | 否       | 此值可以推断出的下载内容的总和`versions`数组
验证       | boolean                    | 否       | JSON 布尔值，该值指示包是否[验证](../nuget-org/id-prefix-reservation.md)

在 nuget.org 中，已验证的包是一个具有与保留的 ID 前缀匹配的包 ID 和拥有的保留的前缀的所有者之一。 有关详细信息，请参阅[ID 前缀保留有关文档](../reference/id-prefix-reservation.md)。

在搜索结果对象中包含的元数据中获取最新的包版本。 中的每项`versions`数组是具有以下属性的 JSON 对象：

名称      | 类型    | 必需 | 说明
--------- | ------- | -------- | -----
@id       | string  | 是      | 到关联的绝对 URL[注册叶](registration-base-url-resource.md#registration-leaf)
version   | string  | 是      | （可能包含生成元数据） 的包的完整的 SemVer 2.0.0 版本字符串
下载 | 整数 | 是      | 为此特定包版本的下载次数

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>示例响应

[!code-JSON [search-result.json](./_data/search-result.json)]
