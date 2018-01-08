---
title: "包元数据，NuGet API |Microsoft 文档"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 96b07019-c2e1-4f40-9290-f65ad71af3b1
description: "包注册基 URL 允许提取有关包的元数据。"
keywords: "NuGet API 包元数据、 NuGet API 注册，NuGet API 未列出的包"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1aabe6ae5c661e12b2639700813946e7a9a58b24
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/05/2018
---
# <a name="package-metadata"></a>包元数据

很可能，使用 NuGet V3 API 的包源提取有关可用的包的元数据。 可以使用提取此元数据`RegistrationsBaseUrl`资源位于[服务索引](service-index.md)。

下找到的文档集合`RegistrationsBaseUrl`通常称为"注册"或"注册 blob"。 下一个文档集`RegistrationsBaseUrl`简称为"注册配置单元"。 注册 hive 包含有关包源上的每个可用的包的所有元数据。

## <a name="versioning"></a>版本管理

以下`@type`将使用值：

@type 值                     | 说明
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-beta | 别名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 别名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 压缩过响应
RegistrationsBaseUrl/3.6.0      | 包含 SemVer 2.0.0 包

这表示三个不同的注册配置单元适用于各种客户端版本。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

这些注册不会被压缩 (这意味着它们使用默式`Content-Encoding: identity`)。 SemVer 2.0.0 包是**排除**从此配置单元。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

使用压缩这些注册`Content-Encoding: gzip`。 SemVer 2.0.0 包是**排除**从此配置单元。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

使用压缩这些注册`Content-Encoding: gzip`。 SemVer 2.0.0 包是**包含**此配置单元中。
有关 SemVer 2.0.0 的详细信息，请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是值`@id`与前面提到的资源关联的属性`@type`值。 在以下文档中，将占位符基本 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

HTTP 方法位于注册资源支持的所有 Url`GET`和`HEAD`。

## <a name="registration-index"></a>注册索引

注册资源组包元数据通过包 id。 不能一次获取多个包 ID 有关的数据。 此资源提供了无法发现包 Id。 而被假定客户端已经知道所需的包 id。 有关每个包版本可用的元数据因服务器实现。 包注册 blob 具有以下层次结构：

- **索引**： 包元数据，由相同的包 id。 与源上的所有包共享的入口点
- **页**： 包版本的分组。 由服务器实现定义的包版本在页中的数目。
- **叶**： 特定于单个包版本的文档。

注册索引的 URL 时可以预测和给定的包 ID 和注册资源的客户端可以确定`@id`从服务索引的值。 检查注册索引会发现的注册页和叶的 Url。

### <a name="registration-pages-and-leaves"></a>注册页并使

尽管它不是严格需要的服务器实现，用于存储注册叶片值在单独的注册页文档中，它是建议的做法，以节省客户端的内存。 而不是内联的所有注册将保留在索引或立即将使存储在页文档，则我们建议服务器实现定义某些启发式方法上的包版本数基于这两种方法之间进行选择或包的累计大小离开。

存储所有的包版本 （会保留） 中注册索引存储上的 HTTP 请求数所必需的提取包元数据，但意味着必须下载较大的文档和必须分配更多的客户端内存。 另一方面，如果服务器实现立即将注册使存储在单独页面文档中，客户端必须执行更多的 HTTP 请求获取所需的信息。

Nuget.org 使用如下所述的试探法： 如果有 128 个或以上版本的包，则会将叶分成大小 64 的页。 如果有不超过 128 个版本，所有内联都离开到注册索引。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>请求参数

name     | 内     | 类型    | 必需 | 说明
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | 字符串  | 是      | 包 ID 小写

`LOWER_ID`值是小写使用由实现的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>响应

响应是一个 JSON 文档具有一个根对象具有以下属性：

name  | 类型             | 必需 | 说明
----- | ---------------- | -------- | -----
count | 整数          | 是      | 在索引中的注册页面数
项 | 对象的数组 | 是      | 注册页的数组

在索引对象的每个项`items`数组是一个 JSON 对象，该对象代表的注册页。

#### <a name="registration-page-object"></a>注册 page 对象

在注册索引中发现的注册页对象具有以下属性：

name   | 类型             | 必需 | 说明
------ | ---------------- | -------- | -----
@id    | 字符串           | 是      | 到注册页 URL
count  | 整数          | 是      | 在页中离开注册的数
项  | 对象的数组 | 否       | 注册使和与其相关联的元数据的数组
较低  | 字符串           | 是      | 中的页 （含） 的最低 SemVer 2.0.0 版本
父 | 字符串           | 否       | 注册索引到 URL
上限  | 字符串           | 是      | （含） 页中的最高 SemVer 2.0.0 版本

`lower`和`upper`需要的特定页版本的元数据时，边界的 page 对象非常有用。
这些边界可用来提取所需的唯一注册页。 版本字符串遵守[NuGet 的版本规则](../reference/package-versioning.md)。 版本字符串被规范化，并且不包含生成元数据。 因为 NuGet 生态系统中的所有版本，与使用实现的版本字符串比较[SemVer 2.0.0's 版本优先规则](http://semver.org/spec/v2.0.0.html#spec-item-11)。

`parent`注册 page 对象才会显示属性`items`属性。

如果`items`属性不存在中注册 page 对象，在指定的 URL`@id`必须可用于提取有关单个包版本的元数据。 `items`数组有时排除从作为一种优化的页对象。 如果单个包 ID 版本数非常大，注册索引文档将大规模并浪费于仅关心特定的版本或较小的范围的版本的客户端过程。

请注意，如果`items`存在，属性，则`@id`属性不需要使用，因为所有的页面数据已经在内联`items`属性。

中的页对象的每一项`items`数组是表示注册叶的 JSON 对象，它具有关联的元数据。

#### <a name="registration-leaf-object-in-a-page"></a>注册在页中的叶对象

注册页中找到的注册叶对象具有以下属性：

name           | 类型   | 必需 | 说明
-------------- | ------ | -------- | -----
@id            | 字符串 | 是      | 注册叶到 URL
catalogEntry   | object | 是      | 包含包元数据的目录项
packageContent | 字符串 | 是      | 包内容 (.nupkg) 到 URL

每个注册叶对象表示单个包版本与关联的数据。

#### <a name="catalog-entry"></a>目录条目

`catalogEntry`注册叶对象中的属性具有以下属性：

name                     | 类型                       | 必需 | 说明
------------------------ | -------------------------- | -------- | -----
@id                      | 字符串                     | 是      | 指向用于生成此对象的文档的 URL
作者                  | 字符串或字符串数组 | 否       | 
dependencyGroups         | 对象的数组           | 否       | 包内容 (.nupkg) 到 URL
说明              | 字符串                     | 否       | 
iconUrl                  | 字符串                     | 否       | 
id                       | 字符串                     | 是      | 程序包的 ID
licenseUrl               | 字符串                     | 否       | 
列出                   | boolean                    | 否       | 应被视为列出如果不存在
MinClientVersion         | 字符串                     | 否       | 
projectUrl               | 字符串                     | 否       | 
发布                | 字符串                     | 否       | 包含 ISO 8601 时间戳的发布包的时间的字符串
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | 字符串                     | 否       | 
标记                     | 字符串或字符串数组  | 否       | 
标题                    | 字符串                     | 否       | 
version                  | 字符串                     | 是      | 包的版本

`dependencyGroups`属性是一个数组，这些对象表示的目标框架按分组的包的依赖关系。 如果包不具有任何依赖关系，`dependencyGroups`属性缺少，空数组，或`dependencies`的所有组的属性为空或缺失。

#### <a name="package-dependency-group"></a>包依赖关系组

每个依赖关系组对象具有以下属性：

name            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
targetFramework | 字符串           | 否       | 这些依赖关系是适用于目标框架
依赖项    | 对象的数组 | 否       |

`targetFramework`字符串使用格式由 NuGet 的.NET 库实现[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)。 如果没有`targetFramework`指定的依赖关系组适用于所有目标框架。

`dependencies`属性是对象的数组，每个元素表示的当前包的包依赖关系。

#### <a name="package-dependency"></a>包依赖关系

每个包依赖项具有以下属性：

name         | 类型   | 必需 | 说明
------------ | ------ | -------- | -----
id           | 字符串 | 是      | 包依赖项的 ID
range        | object | 否       | 允许[版本范围](../reference/package-versioning.md#version-ranges-and-wildcards)依赖关系
注册 | 字符串 | 否       | 此依赖关系的注册索引到 URL

如果`range`排除属性或空字符串，则客户端应默认为版本范围`(, )`。 即允许任何版本的依赖项。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>示例响应 

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在此特定情况下注册索引都有内联在注册页，因此任何额外请求所不需提取单个包版本有关的元数据。

## <a name="registration-page"></a>注册页

注册页包含注册使。 要提取的注册页的 URL 由`@id`中的属性[注册 page 对象](#registration-page-object)上文所述。

当`items`注册索引中未提供数组，HTTP GET 请求的`@id`值会返回 JSON 文档具有一个作为其根对象。 该对象具有以下属性：

name   | 类型             | 必需 | 说明
------ | ---------------- | -------- | -----
@id    | 字符串           | 是      | 到注册页 URL
count  | 整数          | 是      | 在页中离开注册的数
项  | 对象的数组 | 是      | 注册使和与其相关联的元数据的数组
较低  | 字符串           | 是      | 中的页 （含） 的最低 SemVer 2.0.0 版本
父 | 字符串           | 是      | 注册索引到 URL
上限  | 字符串           | 是      | （含） 页中的最高 SemVer 2.0.0 版本

注册叶对象的形状是与注册索引中的相同[上面](#registration-leaf-object-in-a-page)。

## <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>注册叶

注册叶包含有关特定包 ID 和版本信息。 有关特定版本的元数据可能不能在此文档中。 包元数据应从提取[注册索引](#registration-index)或[注册页](#registration-page)（这发现使用注册索引）。

从获取的 URL 来提取注册叶`@id`中的注册索引或注册页的注册叶对象的属性。

注册叶是具有以下属性的根对象的 JSON 文档：

name           | 类型    | 必需 | 说明
-------------- | ------- | -------- | -----
@id            | 字符串  | 是      | 注册叶到 URL
catalogEntry   | 字符串  | 否       | 生成这些叶的目录项 URL
列出         | boolean | 否       | 应被视为列出如果不存在
packageContent | 字符串  | 否       | 包内容 (.nupkg) 到 URL
发布      | 字符串  | 否       | 包含 ISO 8601 时间戳的发布包的时间的字符串
注册   | 字符串  | 否       | 注册索引到 URL

> [!Note]
> 在 nuget.org，`published`值设置为包时未列出的 1900 年。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
