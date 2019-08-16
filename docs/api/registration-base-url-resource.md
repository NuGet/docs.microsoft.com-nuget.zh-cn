---
title: 包元数据, NuGet API
description: 包注册基 URL 允许获取有关包的元数据。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488318"
---
# <a name="package-metadata"></a>包元数据

可以使用 NuGet V3 API 提取有关包源上可用包的元数据。 可以使用在[服务索引](service-index.md)中找到`RegistrationsBaseUrl`的资源提取此元数据。

在下`RegistrationsBaseUrl`找到的文档的集合通常称为 "注册" 或 "注册 blob"。 一个单一`RegistrationsBaseUrl`的文档集称为 "注册配置单元"。 注册配置单元包含有关包源上可用的每个包的所有元数据。

## <a name="versioning"></a>版本管理

使用以下`@type`值:

@type 值                     | 说明
------------------------------- | -----
RegistrationsBaseUrl            | 初始版本
RegistrationsBaseUrl/3.0.0-beta | 别名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | 别名`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 压缩过响应
RegistrationsBaseUrl/3.6.0      | 包括 SemVer 2.0.0 包

这表示可用于各种客户端版本的三个不同的注册配置单元。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

这些注册不会压缩 (也就是说, 它们使用隐含`Content-Encoding: identity`的)。 此配置单元中**排除**了 SemVer 2.0.0 包。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

这些注册使用`Content-Encoding: gzip`进行压缩。 此配置单元中**排除**了 SemVer 2.0.0 包。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

这些注册使用`Content-Encoding: gzip`进行压缩。 此配置单元中**包含**SemVer 2.0.0 包。
有关 SemVer 2.0.0 的详细信息, 请参阅[nuget.org 的 SemVer 2.0.0 支持](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)。

## <a name="base-url"></a>基 URL

以下 api 的基 URL 是与上述资源`@id` `@type`值关联的属性的值。 在下面的文档中, 将使用占位符`{@id}`基 URL。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 url 都支持 HTTP 方法`GET`和`HEAD`。

## <a name="registration-index"></a>注册索引

注册资源组按包 ID 包元数据。 一次不能获取有关多个包 ID 的数据。 此资源不提供任何方式来发现包 Id。 相反, 假设客户端已经知道所需的包 ID。 每个包版本的可用元数据因服务器实现而异。 包注册 blob 具有以下层次结构:

- **索引**: 包元数据的入口点, 由具有相同包 ID 的源中的所有包共享。
- **页面**: 包版本的分组。 页面中的包版本数由服务器实现定义。
- **叶**: 特定于单个包版本的文档。

注册索引的 URL 可预测, 并且可以由客户端从服务索引中给定包 ID 和注册资源的`@id`值来确定。 通过检查注册索引发现注册页和叶的 Url。

### <a name="registration-pages-and-leaves"></a>注册页面和叶

尽管服务器实现将注册 leafs 存储在单独的注册页文档中并不是绝对必需的, 但建议使用这种方法来节省客户端内存。 建议服务器实现定义一些试探法, 以根据包版本的数量在这两种方法之间进行选择, 而不是将所有注册留在索引中, 也不会立即存储在页面文档中。包叶的累计大小。

将所有包版本 (叶) 存储在注册索引中可节省提取包元数据所需的 HTTP 请求数, 但这意味着必须下载更大的文档, 并且必须分配更多的客户端内存。 另一方面, 如果服务器实现立即将注册留在单独的页面文档中, 则客户端必须执行更多 HTTP 请求以获取所需的信息。

Nuget.org 使用的试探法如下: 如果包有128或更多版本, 请将叶分成大小为64的页。 如果版本低于 128, 则将所有行都置于注册索引中。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>请求参数

name     | 内     | 类型    | 必填 | 说明
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 是      | 包 ID lowercased

`LOWER_ID`值是所需的包 ID lowercased, 它使用由实现的规则。NET 的[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>响应

响应是一个 JSON 文档, 其中包含具有以下属性的根对象:

name  | 类型             | 必需 | 说明
----- | ---------------- | -------- | -----
count | integer          | 是      | 索引中注册页的数目
项 | 对象数组 | 是      | 注册页的数组

Index 对象的`items`数组中的每一项都是一个表示注册页的 JSON 对象。

#### <a name="registration-page-object"></a>注册页对象

在注册索引中找到的注册页对象具有以下属性:

name   | 类型             | 必填 | 说明
------ | ---------------- | -------- | -----
@id    | string           | 是      | 注册页的 URL
count  | integer          | 是      | 页面中的注册离开次数
项  | 对象数组 | 否       | 注册叶数组及其关联元数据
下移  | string           | 是      | 页面中的最低 SemVer 2.0.0 版本 (包含)
父级 (parent) | string           | 否       | 注册索引的 URL
左上  | string           | 是      | 页面中的 SemVer 2.0.0 的最高版本 (包含)

当`lower`需要`upper`特定页面版本的元数据时, page 对象的和界限非常有用。
这些界限可用于提取所需的唯一注册页面。 版本字符串遵循[NuGet 的版本规则](../concepts/package-versioning.md)。 版本字符串已规范化, 不包括生成元数据。 与 NuGet 生态系统中的所有版本一样, 版本字符串的比较是使用[SemVer 2.0.0 的版本优先规则](http://semver.org/spec/v2.0.0.html#spec-item-11)实现的。

只有`parent`当注册页对象`items`具有属性时, 才会显示属性。

如果注册页对象中不存在该`@id` 属性,则中指定的URL必须用于获取有关各个包版本的元数据。`items` 该`items`数组有时从页对象中排除为优化。 如果单个包 ID 的版本数非常大, 则对于只关心特定版本或少量版本的客户端, 注册索引文档将会很大, 并且会浪费大量的信息。

请注意, 如果`items`该属性存在, 则`@id`不需要使用属性, 因为所有页面数据`items`都已在属性中内联。

Page 对象的`items`数组中的每一项都是一个表示注册叶及其关联元数据的 JSON 对象。

#### <a name="registration-leaf-object-in-a-page"></a>页中的注册叶对象

在注册页中找到的注册叶对象具有以下属性:

name           | 类型   | 必填 | 说明
-------------- | ------ | -------- | -----
@id            | string | 是      | 注册叶的 URL
catalogEntry   | 对象 (object) | 是      | 包含包元数据的目录条目
packageContent | string | 是      | 包内容的 URL (. nupkg)

每个注册叶对象均表示与单个包版本关联的数据。

#### <a name="catalog-entry"></a>目录条目

注册`catalogEntry`叶对象中的属性具有以下属性:

name                     | 类型                       | 必填 | 说明
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 是      | 用于生成此对象的文档的 URL
作者                  | 字符串或字符串数组 | 否       | 
dependencyGroups         | 对象数组           | 否       | 包的依赖项, 按目标框架分组
弃用              | 对象 (object)                     | 否       | 与包关联的弃用
description              | string                     | 否       | 
iconUrl                  | string                     | 否       | 
id                       | string                     | 是      | 包的 ID
licenseUrl               | string                     | 否       |
licenseExpression        | string                     | 否       | 
列出                   | boolean                    | 否       | 如果不存在, 则应将其视为列出
minClientVersion         | string                     | 否       | 
projectUrl               | string                     | 否       | 
发布                | string                     | 否       | 一个字符串, 其中包含发布包时的 ISO 8601 时间戳
requireLicenseAcceptance | boolean                    | 否       | 
摘要                  | string                     | 否       | 
标记                     | 字符串或字符串数组  | 否       | 
标题                    | string                     | 否       | 
version                  | string                     | 是      | 规范化后的完整版本字符串

Package `version`属性是规范化后的完整版本字符串。 这意味着, 可以在此处包括 SemVer 2.0.0 生成数据。

`dependencyGroups`属性是对象的数组, 这些对象表示包的依赖项, 按目标框架分组。 如果包没有依赖项, 则`dependencyGroups`属性缺失, 空数组, 或者所有组的`dependencies`属性为空或缺失。

`licenseExpression`属性的值符合[NuGet 许可证表达式语法](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)。

#### <a name="package-dependency-group"></a>包依赖关系组

每个依赖项组对象具有以下属性:

name            | 类型             | 必填 | 说明
--------------- | ---------------- | -------- | -----
targetFramework | string           | 否       | 这些依赖关系适用的目标框架
依赖项    | 对象数组 | 否       |

此`targetFramework`字符串使用 NuGet 的 .net 库[nuget](https://www.nuget.org/packages/NuGet.Frameworks/)所实现的格式。 如果未`targetFramework`指定, 则依赖项组适用于所有目标框架。

`dependencies`属性是对象的数组, 每个对象表示当前包的包依赖项。

#### <a name="package-dependency"></a>包依赖关系

每个包依赖项都具有以下属性:

name         | 类型   | 必填 | 说明
------------ | ------ | -------- | -----
id           | string | 是      | 包依赖项的 ID
range        | 对象 (object) | 否       | 依赖项的允许[版本范围](../concepts/package-versioning.md#version-ranges-and-wildcards)
注册 | string | 否       | 此依赖项的注册索引的 URL

如果排除`(, )`属性或空字符串, 客户端应默认为版本范围。 `range` 也就是说, 允许使用任何版本的依赖项。

#### <a name="package-deprecation"></a>包弃用

每个包弃用都具有以下属性:

name             | 类型             | 必需 | 说明
---------------- | ---------------- | -------- | -----
原因          | 字符串数组 | 是      | 弃用包的原因
消息          | string           | 否       | 有关此弃用的其他详细信息
alternatePackage | 对象 (object)           | 否       | 应改为使用的包依赖项

该`reasons`属性必须包含至少一个字符串, 并且应仅包含下表中的字符串:

原因       | 描述             
------------ | -----------
遗留       | 不再维护包
CriticalBugs | 包中的 bug 使其不适用于使用
其他        | 由于未在此列表中的原因, 包已弃用

`reasons`如果属性包含不是来自已知集的字符串, 则应将其忽略。 字符串不区分大小写, 因此`legacy`应将其视为与`Legacy`相同。 数组没有排序限制, 因此字符串可以任意顺序排列。 此外, 如果属性仅包含不来自已知集的字符串, 则应将其视为只包含 "其他" 字符串。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

在这种特定情况下, 注册索引会内嵌注册页面, 因此, 提取有关各个包版本的元数据不需要额外的请求。

## <a name="registration-page"></a>注册页

注册页面包含注册离开。 用于提取注册页的 URL 由前面提到的`@id` [注册页对象](#registration-page-object)中的属性确定。

当注册索引中未提供`@id` 数组时,值的HTTPGET请求将返回一个JSON文档,该文档将对象作为其根。`items` 对象具有以下属性:

name   | 类型             | 必填 | 说明
------ | ---------------- | -------- | -----
@id    | string           | 是      | 注册页的 URL
count  | integer          | 是      | 页面中的注册离开次数
项  | 对象数组 | 是      | 注册叶数组及其关联元数据
下移  | string           | 是      | 页面中的最低 SemVer 2.0.0 版本 (包含)
父级 (parent) | string           | 是      | 注册索引的 URL
左上  | string           | 是      | 页面中的 SemVer 2.0.0 的最高版本 (包含)

注册叶对象的形状与[上面](#registration-leaf-object-in-a-page)的注册索引相同。

## <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>注册叶

注册叶包含有关特定包 ID 和版本的信息。 有关特定版本的元数据在本文档中可能不可用。 应该从[注册索引](#registration-index)或[注册页](#registration-page)(使用注册索引发现) 提取包元数据。

提取注册叶的 URL 是从注册索引或注册`@id`页中注册叶对象的属性获取的。

注册叶是包含具有以下属性的根对象的 JSON 文档:

name           | 类型    | 必填 | 说明
-------------- | ------- | -------- | -----
@id            | string  | 是      | 注册叶的 URL
catalogEntry   | string  | 否       | 生成这些叶的目录条目的 URL
列出         | boolean | 否       | 如果不存在, 则应将其视为列出
packageContent | string  | 否       | 包内容的 URL (. nupkg)
发布      | string  | 否       | 一个字符串, 其中包含发布包时的 ISO 8601 时间戳
注册   | string  | 否       | 注册索引的 URL

> [!Note]
> 在 nuget.org 上, `published`如果未列出包, 该值将设置为1900年。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
