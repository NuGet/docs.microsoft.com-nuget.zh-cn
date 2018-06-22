---
title: 搜索，NuGet API
description: 搜索服务允许客户端到包按关键字的查询和某些包字段上的筛选结果。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 76600ee916305ee01ddfb675c83c184e980c5a42
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821078"
---
# <a name="search"></a>搜索

可搜索在包源使用 V3 API 上可用的包。 用于搜索的资源是`SearchQueryService`资源位于[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`将使用值：

@type 值                   | 说明
----------------------------- | -----
SearchQueryService            | 初始版本
SearchQueryService/3.0.0-beta | 别名 `SearchQueryService`
SearchQueryService/3.0.0-rc   | 别名 `SearchQueryService`

## <a name="base-url"></a>基 URL

以下 API 的基 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。 在以下文档中，将占位符基本 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。

## <a name="search-for-packages"></a>搜索包

搜索 API 允许包指定的搜索查询匹配的页的查询的客户端。 搜索查询 （例如搜索词的词汇切分） 的解释由服务器实现但的常规的假定条件下搜索查询用于匹配的包 Id、 标题、 说明和标记。 也可以考虑其他包元数据字段。

未列出的包应永远不会出现在搜索结果。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

名称        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | 字符串  | 否       | 为用于筛选器程序包搜索词
skip        | URL    | 整数 | 否       | 要分页的跳过的结果数
take        | URL    | 整数 | 否       | 要为分页返回的结果数
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字符串  | 否       | SemVer 1.0.0 版本字符串 

搜索查询`q`分析由服务器实现定义的方式。 nuget.org 支持基本筛选[各种字段](../consume-packages/finding-and-choosing-packages.md#search-syntax)。 如果没有`q`提供应返回所有包，skip 和 take 强加的边界内。 这使 NuGet Visual Studio 体验中的"浏览"选项卡。

`skip`参数默认值为 0。

`take`参数应大于零的整数。 服务器实现可能会对施加的最大值。

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用来选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 (与[标准的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，如使用 4 的整数部分的版本字符串)。
如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 兼容包将返回。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是包含最多的 JSON 文档`take`搜索结果。 搜索结果进行分组的包 id。

根 JSON 对象具有以下属性：

名称      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
totalHits | 整数          | 是      | 匹配项，而不考虑的总数目`skip`和 `take`
数据      | 对象的数组 | 是      | 由请求匹配的搜索结果

### <a name="search-result"></a>搜索结果

在每个项`data`数组是组成一组共享相同的包 id。 程序包版本的 JSON 对象
该对象具有以下属性：

名称           | 类型                       | 必需 | 说明
-------------- | -------------------------- | -------- | -----
id             | 字符串                     | 是      | 匹配的程序包的 ID
version        | 字符串                     | 是      | 完整的 SemVer 2.0.0 的版本字符串 （可能包含生成元数据） 的包
说明    | 字符串                     | 否       | 
版本       | 对象的数组           | 是      | 所有匹配的包版本`prerelease`参数
作者        | 字符串或字符串数组 | 否       | 
iconUrl        | 字符串                     | 否       | 
licenseUrl     | 字符串                     | 否       | 
所有者         | 字符串或字符串数组 | 否       | 
projectUrl     | 字符串                     | 否       | 
注册   | 字符串                     | 否       | 到关联的绝对 URL[注册索引](registration-base-url-resource.md#registration-index)
摘要        | 字符串                     | 否       | 
标记           | 字符串或字符串数组 | 否       | 
标题          | 字符串                     | 否       | 
totalDownloads | 整数                    | 否       | 此值可以推断出的总和中的下载`versions`数组
验证       | boolean                    | 否       | JSON 布尔值，该值指示包是否[验证](../reference/id-prefix-reservation.md)

在 nuget.org，验证的包是其中一个具有匹配保留的 ID 前缀的包 ID 和拥有的保留的命名空间的所有者之一。 有关详细信息，请参阅[文档 ID 前缀保留有关](../reference/id-prefix-reservation.md)。

搜索结果对象中包含的元数据中获取最新的包版本。 在每个项`versions`数组是具有以下属性的 JSON 对象：

名称      | 类型    | 必需 | 说明
--------- | ------- | -------- | -----
@id       | 字符串  | 是      | 到关联的绝对 URL[注册叶](registration-base-url-resource.md#registration-leaf)
version   | 字符串  | 是      | 完整的 SemVer 2.0.0 的版本字符串 （可能包含生成元数据） 的包
下载 | 整数 | 是      | 此特定包版本的下载的次数

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>示例响应

[!code-JSON [search-result.json](./_data/search-result.json)]
