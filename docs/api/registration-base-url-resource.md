---
title: 包元数据，NuGet API
description: 包注册基 URL 允许提取有关包的元数据。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: ba47d6fdeeaa4ee9de83ef4dd990707bd4928063
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453554"
---
# <a name="package-metadata"></a>包元数据

就可以使用 NuGet V3 API 对包源获取可用的包有关的元数据。 可以使用提取此元数据`RegistrationsBaseUrl`资源中找到[服务索引](service-index.md)。

文档下找到的集合`RegistrationsBaseUrl`通常称为"注册"或"注册 blob"。 下一个文档集`RegistrationsBaseUrl`被称为"注册配置单元"。 注册配置单元包含有关包源上可用的每个包的所有元数据。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                     | 说明
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-beta | 别名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 别名 `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | 使用 gzip 压缩响应
RegistrationsBaseUrl/3.6.0      | 包含 SemVer 2.0.0 包

这表示三个不同的注册配置单元可用于各种客户端版本。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

这些注册不会被压缩 (这意味着它们使用隐式`Content-Encoding: identity`)。 SemVer 2.0.0 程序包**排除**此 hive 中。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

使用压缩这些注册`Content-Encoding: gzip`。 SemVer 2.0.0 程序包**排除**此 hive 中。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

使用压缩这些注册`Content-Encoding: gzip`。 SemVer 2.0.0 程序包**包含**此配置单元中。
有关 SemVer 2.0.0 的详细信息，请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。 在以下文档中，占位符基 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。

## <a name="registration-index"></a>注册索引

注册资源组包元数据的包 id。 不能一次获取多个包 ID 有关的数据。 此资源提供了无法发现的包 Id。 而被假定客户端已经知道所需的包 id。 有关每个包版本的可用元数据因服务器实现。 包注册 blob 具有以下层次结构：

- **索引**： 共享相同的包 id。 源上的所有包的包元数据的入口点
- **页**： 包版本的分组。 在页面中的包版本数量由服务器实现定义。
- **叶**： 特定于单个包版本的文档。

注册索引的 URL 是可预测，也可由客户端指定包 ID 和注册资源`@id`从服务索引的值。 检查注册索引会发现的注册页面和叶的 Url。

### <a name="registration-pages-and-leaves"></a>注册页并使

尽管它并未严格要求服务器实现，用于存储注册叶中单独的注册页文档，但它是建议的做法，以节省客户端的内存。 而不是初始化所有注册将留在索引或立即将使存储在页文档，建议服务器实现定义某些启发式算法以基于包的版本数的两种方法之间进行选择或使包的累积大小。

存储所有的包版本 （叶） 中注册索引存储上的 HTTP 请求数所需提取包元数据，但意味着，必须下载较大的文档，并且必须分配更多的客户端内存。 但是，如果服务器实现立即将注册使存储在单独的页的文档中，客户端必须执行更多的 HTTP 请求以获取所需的信息。

Nuget.org 使用如下所示的试探法： 如果有 128 个或以上版本的包，则会将叶分成大小 64 的页面。 如果有不超过 128 个版本，所有内联都离开到注册的索引。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>请求参数

name     | 内     | 类型    | 必需 | 说明
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字符串  | 是      | 包 ID 小写

`LOWER_ID`值是小写使用通过实施的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>响应

响应是一个 JSON 文档具有一个根对象具有以下属性：

name  | 类型             | 必需 | 说明
----- | ---------------- | -------- | -----
count | 整数          | 是      | 在索引中的注册页面数
项 | 对象的数组 | 是      | 注册页的数组

在该索引对象的每个项`items`数组是 JSON 对象，表示注册页。

#### <a name="registration-page-object"></a>注册页对象

注册页对象注册索引中找到具有以下属性：

name   | 类型             | 必需 | 说明
------ | ---------------- | -------- | -----
@id    | 字符串           | 是      | 注册页面的 URL
count  | 整数          | 是      | 在页面中离开注册数
项  | 对象的数组 | 否       | 注册叶和其关联的元数据的数组
较低  | 字符串           | 是      | （含） 的页中最低的 SemVer 2.0.0 版本
父级 (parent) | 字符串           | 否       | 为注册索引 URL
上限  | 字符串           | 是      | （含） 的页中最高的 SemVer 2.0.0 版本

`lower`和`upper`时所需的元数据的特定页版本页面对象的边界很有用。
这些边界可用来提取所需的唯一注册页。 版本字符串遵守[的 NuGet 版本规则](../reference/package-versioning.md)。 版本字符串进行规范化，并且不包括生成元数据。 NuGet 生态系统中的所有版本的版本字符串比较是实现使用[SemVer 2.0.0's 版本优先顺序规则](http://semver.org/spec/v2.0.0.html#spec-item-11)。

`parent`注册页对象具有才会出现属性`items`属性。

如果`items`属性不存在于注册页对象中，在指定的 URL`@id`必须可用于获取有关各个包版本的元数据。 `items`数组有时不作为一种优化的 page 对象。 如果单个包 ID 的版本数非常大，注册索引文档将大规模和浪费只关心特定的版本或小范围的版本的客户端的过程。

请注意，如果`items`存在，属性，则`@id`属性不需要使用，因为所有的页面数据已在内联`items`属性。

Page 对象中的每一项`items`数组，表示注册叶的 JSON 对象以及与其关联的元数据。

#### <a name="registration-leaf-object-in-a-page"></a>注册页中的叶对象

在注册页中找到的注册叶对象具有以下属性：

name           | 类型   | 必需 | 说明
-------------- | ------ | -------- | -----
@id            | 字符串 | 是      | 为注册叶 URL
catalogEntry   | object | 是      | 包含包元数据的目录条目
packageContent | 字符串 | 是      | 指向包内容 (.nupkg) 的 URL

每个注册叶对象表示单个包版本与关联的数据。

#### <a name="catalog-entry"></a>目录条目

`catalogEntry`注册叶对象中的属性具有以下属性：

name                     | 类型                       | 必需 | 说明
------------------------ | -------------------------- | -------- | -----
@id                      | 字符串                     | 是      | 指向用于生成此对象的文档的 URL
作者                  | 字符串或字符串数组 | 否       | 
dependencyGroups         | 对象的数组           | 否       | 按目标框架的包依赖项
说明              | 字符串                     | 否       | 
iconUrl                  | 字符串                     | 否       | 
id                       | 字符串                     | 是      | 包的 ID
licenseUrl               | 字符串                     | 否       | 
列出                   | boolean                    | 否       | 应被视为列出如果不存在
minClientVersion         | 字符串                     | 否       | 
projectUrl               | 字符串                     | 否       | 
已发布                | 字符串                     | 否       | 一个包含已发布包时的 ISO 8601 时间戳的字符串
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | 字符串                     | 否       | 
标记                     | 字符串或字符串数组  | 否       | 
标题                    | 字符串                     | 否       | 
version                  | 字符串                     | 是      | 规范化后的完整版本字符串

包`version`属性是在执行规范化后的完整版本字符串。 这意味着，SemVer 2.0.0 生成数据可以包含此处。

`dependencyGroups`属性是一个表示按目标框架的包的依赖项的对象的数组。 如果包有没有依赖关系`dependencyGroups`缺少属性，一个空数组或`dependencies`所有组的属性为空或缺失。

#### <a name="package-dependency-group"></a>包依赖关系组

每个依赖关系组对象具有以下属性：

name            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
targetFramework | 字符串           | 否       | 这些依赖关系都适用于目标框架
依赖项    | 对象的数组 | 否       |

`targetFramework`字符串使用格式由 NuGet 的.NET 库实现[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)。 如果没有`targetFramework`指定，则依赖关系组适用于所有目标框架。

`dependencies`属性是对象的数组，每个元素表示的当前包的包依赖项。

#### <a name="package-dependency"></a>包依赖项

每个包依赖项具有以下属性：

name         | 类型   | 必需 | 说明
------------ | ------ | -------- | -----
id           | 字符串 | 是      | 包依赖项的 ID
range        | object | 否       | 允许[版本范围](../reference/package-versioning.md#version-ranges-and-wildcards)依赖关系
注册 | 字符串 | 否       | 为此依赖项的注册索引到 URL

如果`range`属性被排除或者为空字符串，客户端应默认为版本范围`(, )`。 也就是说，允许任何版本的依赖项。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特定情况下注册索引都有内联的注册页，因此没有额外的请求所需提取单个包版本有关的元数据。

## <a name="registration-page"></a>注册页

注册页包含注册叶。 要提取的注册页的 URL 由`@id`中的属性[注册页对象](#registration-page-object)上面所述。

当`items`数组未提供注册索引中，HTTP GET 请求的`@id`值将返回一个 JSON 文档具有作为其根对象。 该对象具有以下属性：

name   | 类型             | 必需 | 说明
------ | ---------------- | -------- | -----
@id    | 字符串           | 是      | 注册页面的 URL
count  | 整数          | 是      | 在页面中离开注册数
项  | 对象的数组 | 是      | 注册叶和其关联的元数据的数组
较低  | 字符串           | 是      | （含） 的页中最低的 SemVer 2.0.0 版本
父级 (parent) | 字符串           | 是      | 为注册索引 URL
上限  | 字符串           | 是      | （含） 的页中最高的 SemVer 2.0.0 版本

注册叶对象的形状是与注册索引中的相同[上面](#registration-leaf-object-in-a-page)。

## <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>注册叶

注册叶包含有关特定包 ID 和版本信息。 有关特定版本的元数据可能不可用本文档中。 包元数据应从中提取[注册索引](#registration-index)或[注册页](#registration-page)（这发现使用注册索引）。

从获取的 URL 来提取注册叶`@id`注册索引或注册页中的注册叶对象的属性。

注册叶是与具有以下属性的根对象的 JSON 文档：

name           | 类型    | 必需 | 说明
-------------- | ------- | -------- | -----
@id            | 字符串  | 是      | 为注册叶 URL
catalogEntry   | 字符串  | 否       | 生成这些叶的目录项 URL
列出         | boolean | 否       | 应被视为列出如果不存在
packageContent | 字符串  | 否       | 指向包内容 (.nupkg) 的 URL
已发布      | 字符串  | 否       | 一个包含已发布包时的 ISO 8601 时间戳的字符串
注册   | 字符串  | 否       | 为注册索引 URL

> [!Note]
> 在 nuget.org 中，`published`值设置为当包很未列出的 1900 年。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
