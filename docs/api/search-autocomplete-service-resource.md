---
title: 记忆式键入功能，NuGet API
description: 搜索记忆式键入功能服务支持交互式发现的包 Id 和版本。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822131"
---
# <a name="autocomplete"></a>自动完成

它是可以生成使用 V3 API 的包 ID 和版本记忆式键入功能体验。 用于进行自动完成查询的资源是`SearchAutocompleteService`资源位于[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`将使用值：

@type 值                          | 说明
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-beta | 别名 `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 别名 `SearchAutocompleteService`

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。 在以下文档中，将占位符基本 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。

## <a name="search-for-package-ids"></a>搜索包 Id

第一个自动完成 API 支持搜索包 ID 字符串的一部分。 当你想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。

仅未列出的版本的包将不会出现在结果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

名称        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | 字符串  | 否       | 要针对包 Id 进行比较的字符串
skip        | URL    | 整数 | 否       | 要分页的跳过的结果数
take        | URL    | 整数 | 否       | 要为分页返回的结果数
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字符串  | 否       | SemVer 1.0.0 版本字符串 

自动完成查询`q`分析由服务器实现定义的方式。 nuget.org 支持查询个前缀的包 ID 令牌，它们是由拆分生成的 ID 的段原始由 camel 大小写和符号字符。

`skip`参数默认值为 0。

`take`参数应大于零的整数。 服务器实现可能会对施加的最大值。

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用来选择[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一包 Id (与[标准的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，如使用 4 的整数部分的版本字符串)。
如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 兼容包将返回。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是包含最多的 JSON 文档`take`记忆式键入功能结果。

根 JSON 对象具有以下属性：

名称      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
totalHits | 整数          | 是      | 匹配项，而不考虑的总数目`skip`和 `take`
数据      | 字符串数组 | 是      | 由请求的包 Id 匹配

### <a name="sample-request"></a>示例请求

获取 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>枚举包版本

客户端后，发现了包 ID 使用以前的 API，可以使用记忆式键入 API 提供的包 id 枚举包版本

未列出的包版本将不会出现在结果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

名称        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
id          | URL    | 字符串  | 是      | 要提取的版本的包 ID
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字符串  | 否       | SemVer 2.0.0 的版本字符串 

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用于选择加入到 SemVer 2.0.0 包。 如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。 如果`semVerLevel=2.0.0`提供 SemVer 1.0.0 和 SemVer 2.0.0 版本将返回。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是包含所有包版本的提供的包 ID，筛选由给定的查询参数的 JSON 文档。

根 JSON 对象具有以下属性：

名称      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
数据      | 字符串数组 | 是      | 由请求匹配的程序包版本

中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
