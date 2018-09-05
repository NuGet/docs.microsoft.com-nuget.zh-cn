---
title: 记忆式键入功能，NuGet API
description: 该搜索自动完成服务支持交互式搜索的包 Id 和版本。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549078"
---
# <a name="autocomplete"></a>自动完成

它是可以构建使用 V3 API 的包 ID 和版本自动完成体验。 在进行自动完成查询使用的资源是`SearchAutocompleteService`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                          | 说明
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-beta | 别名 `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 别名 `SearchAutocompleteService`

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。 在以下文档中，占位符基 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。

## <a name="search-for-package-ids"></a>搜索包 Id

第一个自动完成 API 支持搜索包 ID 字符串的一部分。 当您想要提供用户界面集成在一起的 NuGet 包源中的包 typeahead 功能时，这非常有利。

仅未列出的版本的包不会出现在结果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

name        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | 字符串  | 否       | 要与包 Id 进行比较的字符串
skip        | URL    | 整数 | 否       | 要分页的跳过的结果数
Take        | URL    | 整数 | 否       | 要为分页返回的结果数
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字符串  | 否       | SemVer 1.0.0 版本字符串 

记忆式键入功能查询`q`分析由服务器实现定义的方式。 nuget.org 支持查询是由拆分生成的 ID 的片段的包 ID 令牌的前缀为原始由驼峰式大小写和符号字符。

`skip`参数默认值为 0。

`take`参数应为大于零的整数。 服务器实现可能会施加最大值。

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用来选择中加入[SemVer 2.0.0 包](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)。
如果排除此查询参数，将返回与 SemVer 1.0.0 兼容版本的唯一程序包 Id (与[standard 的 NuGet 版本控制](../reference/package-versioning.md)需要注意的问题，例如使用 4 个整数部分的版本字符串)。
如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是 JSON 文档，其中最多包含`take`记忆式键入功能结果。

根 JSON 对象具有以下属性：

name      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
totalHits | 整数          | 是      | 匹配项，而不考虑总数`skip`和 `take`
数据      | 字符串数组 | 是      | 包 Id 匹配的请求

### <a name="sample-request"></a>示例请求

获取 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>枚举的包版本

客户端的包 ID 发现后使用以前的 API，可以使用记忆式键入功能 API 枚举的包版本的提供的包 id。

未列出的包版本不会出现在结果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

name        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
id          | URL    | 字符串  | 是      | 要提取的版本的程序包 ID
预发行版  | URL    | boolean | 否       | `true` 或`false`确定是否包括[预发行包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | 字符串  | 否       | SemVer 2.0.0 版本字符串 

如果`prerelease`未提供排除预发行包。

`semVerLevel`查询参数用来参加 SemVer 2.0.0 包。 如果排除此查询参数，将返回仅 SemVer 1.0.0 版本。 如果`semVerLevel=2.0.0`提供，将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)有关详细信息。

### <a name="response"></a>响应

响应是 JSON 文档，其中包含按给定的查询参数进行筛选提供的包 ID 的所有包版本。

根 JSON 对象具有以下属性：

name      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
数据      | 字符串数组 | 是      | 由请求匹配的包版本

中的包版本`data`数组可能包含 SemVer 2.0.0 生成元数据 (例如`1.0.0+metadata`) 如果`semVerLevel=2.0.0`查询字符串中提供。

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
