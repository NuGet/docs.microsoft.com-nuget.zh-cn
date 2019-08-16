---
title: 自动完成, NuGet API
description: 搜索自动完成服务支持对包 Id 和版本进行交互式发现。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488295"
---
# <a name="autocomplete"></a>自动完成

可以使用 V3 API 构建包 ID 和版本自动完成体验。 用于使自动完成查询的资源是在`SearchAutocompleteService` [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本管理

使用以下`@type`值:

@type 值                          | 说明
------------------------------------ | -----
SearchAutocompleteService            | 初始版本
SearchAutocompleteService/3.0.0-beta | 别名`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | 别名`SearchAutocompleteService`

## <a name="base-url"></a>基 URL

以下 api 的基 URL 是与上述某个资源`@id` `@type`值关联的属性的值。 在下面的文档中, 将使用占位符`{@id}`基 URL。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。

## <a name="search-for-package-ids"></a>搜索包 Id

第一个自动完成 API 支持搜索包 ID 字符串的一部分。 如果要在与 NuGet 包源集成的用户界面中提供包 typeahead 功能, 这非常有用。

只有未列出的版本的包将不会出现在结果中。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

name        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | 否       | 要与包 Id 进行比较的字符串
skip        | URL    | integer | 否       | 要跳过的结果数, 用于分页
长        | URL    | integer | 否       | 要返回的结果数, 用于分页
早期  | URL    | boolean | 否       | `true`或`false`确定是否包括[预发布包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 否       | SemVer 1.0.0 版本字符串 

自动完成查询`q`按服务器实现所定义的方式进行分析。 nuget.org 支持查询包 ID 令牌的前缀, 该前缀是由拆分以大小写字符和符号字符为原始而生成的 ID 的组成部分。

`skip`参数默认为0。

`take`参数应为大于零的整数。 服务器实现可能会施加最大值。

如果`prerelease`未提供, 则将排除预发布包。

Query 参数用于选择[SemVer 2.0.0 包。](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages) `semVerLevel`
如果排除此查询参数, 则将仅返回带有 SemVer 1.0.0 兼容版本的包 Id (带有[标准的 NuGet 版本控制](../concepts/package-versioning.md)注意事项, 如具有4个整数部分的版本字符串)。
如果`semVerLevel=2.0.0`提供了, 则将返回 SemVer 1.0.0 和 SemVer 2.0.0 兼容包。 有关详细信息, 请参阅[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

### <a name="response"></a>响应

响应是最多`take`包含自动完成结果的 JSON 文档。

根 JSON 对象具有以下属性:

name      | 类型             | 必填 | 说明
--------- | ---------------- | -------- | -----
totalHits | integer          | 是      | 匹配项的总数, `skip`忽略和`take`
数据      | 字符串数组 | 是      | 请求匹配的包 Id

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>枚举包版本

使用以前的 API 发现包 ID 后, 客户端可以使用自动完成 API 来枚举提供的包 ID 的包版本。

未列出的包版本将不会出现在结果中。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>请求参数

name        | 内     | 类型    | 必需 | 说明
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | 是      | 要提取其版本的包 ID
早期  | URL    | boolean | 否       | `true`或`false`确定是否包括[预发布包](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | 否       | SemVer 2.0.0 版本字符串 

如果`prerelease`未提供, 则将排除预发布包。

`semVerLevel` Query 参数用于选择 SemVer 2.0.0 包。 如果排除此查询参数, 则仅返回 SemVer 1.0.0 版本。 如果`semVerLevel=2.0.0`提供了, 则将返回 SemVer 1.0.0 和 SemVer 2.0.0 版本。 有关详细信息, 请参阅[SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) 。

### <a name="response"></a>响应

响应是一个 JSON 文档, 其中包含所提供的包 ID 的所有包版本, 并按给定的查询参数进行筛选。

根 JSON 对象具有以下属性:

name      | 类型             | 必需 | 说明
--------- | ---------------- | -------- | -----
数据      | 字符串数组 | 是      | 与请求匹配的包版本

如果`1.0.0+metadata` `data` 查询字符串中提供了,则数组中的包版本可能包含SemVer2.0.0生成元数据(例如)。`semVerLevel=2.0.0`

### <a name="sample-request"></a>示例请求

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>示例响应

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
