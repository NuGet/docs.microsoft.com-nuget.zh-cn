---
title: 目录资源，NuGet V3 API
description: 目录是所有程序包创建并删除在 nuget.org 上的索引。
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fd5188c92f8154391359b8da5c8a32f4d5d6f2c0
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453580"
---
# <a name="catalog"></a>Catalog

**目录**是记录之类的创建和删除的包源上的所有包操作的资源。 目录资源具有`Catalog`中键入[服务索引](service-index.md)。

> [!Note]
> 由于该目录不由官方 NuGet 客户端，并非所有包源都实现目录。

> [!Note]
> 目前，nuget.org 目录不是在中国推出的。 有关更多详细信息，请参阅[NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值   | 说明
------------- | -----
Catalog/3.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的入口点 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。 本主题使用占位符 URL `{@id}`。

## <a name="http-methods"></a>HTTP 方法

仅 HTTP 方法位于目录资源支持的所有 Url`GET`和`HEAD`。

## <a name="catalog-index"></a>目录索引

目录索引是具有一系列目录项，按时间顺序排列的已知位置中的文档。 它是目录资源的入口点。

索引组成目录页。 每个目录页包含目录项。 每个目录项表示有关时间点的单个包的事件。 目录项可以表示已创建，未列出、 重新列出或删除从包源的包。 通过处理中按时间顺序的目录项，客户端可以生成 V3 包源上存在的每个包的最新视图。

简单地说，目录的 blob 具有以下层次结构：

- **索引**： 目录的入口点。
- **页**： 目录项的分组。
- **叶**: 文档，表示一个目录项，它是单个包的状态的快照。

每个目录对象具有一个名为属性`commitTimeStamp`表示项添加到目录中时。 目录项添加到名为提交的批次中的目录页。 在同一提交中的所有目录项都具有相同提交时间戳 (`commitTimeStamp`) 和提交 ID (`commitId`)。 目录项放置在同一提交中表示时间上的包源围绕同一点发生的事件。 目录提交中没有排序。

因为每个包 ID 和版本是唯一的将永远不会有多个目录项的提交中。 这可确保，单个包的目录项可始终明确地排序方面提交时间戳。

没有永远不会为每个目录的多个提交`commitTimeStamp`。 换而言之，`commitId`是冗余的`commitTimeStamp`。

与此相反[包元数据资源](registration-base-url-resource.md)、 包 ID 索引、 目录是索引 （和可查询） 只能由时间。

目录项总是会添加到的目录中的单调递增的、 按时间顺序。 这意味着，如果在时间 X 添加目录提交则没有目录提交会不断添加时间小于或等于 X。

以下请求提取目录索引。

    GET {@id}

目录索引是包含具有以下属性的对象的 JSON 文档：

name            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 与最新提交关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 最新的提交时间戳
count           | 整数          | 是      | 在索引中的页面数
项           | 对象的数组 | 是      | 对象，表示页的每个对象的数组

在每个元素`items`数组是具有一些有关每个页面的最小的详细信息的对象。 这些页面对象不包含目录叶 （项）。 未定义此数组中元素的顺序。 可按内存使用中的客户端排序页及其`commitTimeStamp`属性。

由于新的页进行介绍，`count`递增和新对象将显示在`items`数组。

将项目添加到目录，该索引的`commitId`将更改和`commitTimeStamp`会增加。 这两个属性是通过所有页实质上是摘要`commitId`并`commitTimeStamp`中的值以`items`数组。

### <a name="catalog-page-object-in-the-index"></a>在索引中的目录页对象

目录索引中找到的目录页对象`items`属性具有以下属性：

name            | 类型    | 必需 | 说明
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 提取目录页面的 URL
commitId        | 字符串  | 是      | 使用此页中的最新提交关联的唯一 ID
commitTimeStamp | 字符串  | 是      | 在此页中的最新提交的时间戳
count           | 整数 | 是      | 在目录页中的项的数目

与此相反[包元数据资源](registration-base-url-resource.md)在某些情况下，内嵌元素离开到索引中，目录叶是永远不会内联到索引，始终必须通过使用页面的提取`@id`URL。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>目录页

目录页是目录项的集合。 这是使用其中一个提取的文档`@id`目录索引中找到的值。 目录页面的 URL 不应为可预测，并应使用仅目录索引发现。

新目录项添加到目录索引只能与最高的提交时间戳中的页或到新页面。 一旦具有更高版本的提交时间戳的页面添加到目录中，较早的页面永远不会添加或更改。

目录页文档是具有以下属性的 JSON 对象：

name            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 使用此页中的最新提交关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 在此页中的最新提交的时间戳
count           | 整数          | 是      | 在页中的项的数目
项           | 对象的数组 | 是      | 此页中的目录项
父级 (parent)          | 字符串           | 是      | 到目录索引 URL

在每个元素`items`数组是具有一些有关目录项的最小的详细信息的对象。 这些项对象不包含的所有目录项的数据。 在页面的项的顺序`items`数组未定义。 可按内存使用中的客户端排序项及其`commitTimeStamp`属性。

在页面中的目录项的数目由服务器实现定义。 对于 nuget.org，最多有 550 项在每个页中，尽管的实际数目的时间可能会更小，具体取决于在下一步提交批大小某些页面。

引入了新项，如`count`递增和新的目录项对象出现在`items`数组。

将项目添加到页上，`commitId`更改和`commitTimeStamp`会增加。 这两个属性对所有是实质上是摘要`commitId`并`commitTimeStamp`中的值以`items`数组。

### <a name="catalog-item-object-in-a-page"></a>目录项在页面中的对象

在目录页中找到的目录项对象`items`属性具有以下属性：

name            | 类型    | 必需 | 说明
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 要提取的目录项的 URL
@type           | 字符串  | 是      | 目录项的类型
commitId        | 字符串  | 是      | 与此目录项关联的提交 ID
commitTimeStamp | 字符串  | 是      | 此目录项的提交时间戳
nuget:id        | 字符串  | 是      | 该叶与包 ID
nuget:version   | 字符串  | 是      | 该叶与包版本

`@type`值将是以下两个值之一：

1. `nuget:PackageDetails`： 这对应于`PackageDetails`目录叶文档中的类型。
1. `nuget:PackageDelete`： 这对应于`PackageDelete`目录叶文档中的类型。

有关详细信息意味着每个类型，请参阅[相对应的项类型](#item-types)下面。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目录叶

目录叶包含有关特定包 ID 和版本在某个时间点的元数据的时间。 这是使用提取的文档`@id`目录页中找到的值。 为目录叶的 URL 不应为可预测，并且应使用目录页发现。

目录叶文档是具有以下属性的 JSON 对象：

name                    | 类型                       | 必需 | 说明
----------------------- | -------------------------- | -------- | -----
@type                   | 字符串或字符串数组 | 是      | 目录项的类型
catalog:commitId        | 字符串                     | 是      | 一个与此目录项关联的提交 ID
catalog:commitTimeStamp | 字符串                     | 是      | 此目录项的提交时间戳
id                      | 字符串                     | 是      | 目录项的包 ID
已发布               | 字符串                     | 是      | 包的目录项的发布的日期
version                 | 字符串                     | 是      | 目录项的包版本

### <a name="item-types"></a>项类型

`@type`属性为字符串数组。 为方便起见，如果`@type`值是一个字符串，它应视为一个大小的任何数组。 并非所有可能值`@type`记录。 但是，每个目录项有两个以下字符串类型值之一：

1. `PackageDetails`： 表示包元数据的快照
1. `PackageDelete`： 表示已删除的包

### <a name="package-details-catalog-items"></a>包的详细信息的目录项

目录项类型的`PackageDetails`包含特定包 （ID 和版本组合） 的包元数据的快照。 如果包源遇到的任何以下情况下，则会生成包目录项的详细信息：

1. 包是**推送**。
1. 包是**列出**。
1. 包是**未列出**。
1. 包是**重排**。

包重排是实质上是生成包本身的虚设推送，无需更改现有包的管理手势。 在 nuget.org 中，使用目录的后台作业之一修复 bug 后使用重排。

客户端使用的目录项不应尝试确定哪种方案生成的目录项目。 相反，客户端应只需更新任何维护的视图或索引使用的目录项目中包含的元数据。 此外，应妥善处理重复或冗余目录项 （幂等方式）。

包详细信息的目录项具有以下属性除了[包含在所有目录叶](#catalog-leaf)。

name                    | 类型                       | 必需 | 说明
----------------------- | -------------------------- | -------- | -----
作者                 | 字符串                     | 否       |
created                 | 字符串                     | 否       | 首次创建包的时间戳。 回退属性： `published`。
dependencyGroups        | 对象的数组           | 否       | 相同的格式设置为[包元数据资源](registration-base-url-resource.md#package-dependency-group)
说明             | 字符串                     | 否       |
iconUrl                 | 字符串                     | 否       |
isPrerelease            | boolean                    | 否       | 是否是预发行包版本。 可以从检测到`version`。
语言                | 字符串                     | 否       |
licenseUrl              | 字符串                     | 否       |
列出                  | boolean                    | 否       | 该程序包是否将列
minClientVersion        | 字符串                     | 否       |
packageHash             | 字符串                     | 是      | 使用编码的包的哈希[标准 base64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | 字符串                     | 是      |
packageSize             | 整数                    | 是      | 包.nupkg 以字节为单位的大小
projectUrl              | 字符串                     | 否       |
releaseNotes            | 字符串                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假定`false`如果排除
摘要                 | 字符串                     | 否       |
标记                    | 字符串数组           | 否       |
标题                   | 字符串                     | 否       |
verbatimVersion         | 字符串                     | 否       | 因为它的版本字符串最初位于.nuspec

包`version`属性是在执行规范化后的完整版本字符串。 这意味着，SemVer 2.0.0 生成数据可以包含此处。

`created`包已首次接收到包源，这通常是短时间之前目录项的提交时间戳时时间戳。

`packageHashAlgorithm`是由服务器实现表示哈希算法用于生成定义的字符串`packageHash`。 始终使用 nuget.org`packageHashAlgorithm`的值`SHA512`。

`published`时间戳是上次列出包的时间。

> [!Note]
> 在 nuget.org 中，`published`值设置为 1900 年时取消列出包。

#### <a name="sample-request"></a>示例请求

获取 https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>包删除目录项

目录项类型的`PackageDelete`包含少量的包从包源已被删除并且不再可用于任何包的操作 （如还原），指示向目录客户端的信息。

> [!Note]
> 很可能要删除的包和更高版本重新发布使用的相同包 ID 和版本。 在 nuget.org 中，这是极少数情况下，因为这会破坏的包 ID 和版本表示特定包内容的官方客户端的假设。 在 nuget.org 上包删除的详细信息，请参阅[我们的策略](../policies/deleting-packages.md)。

包删除目录项不包含其他属性除了[包含在所有目录叶](#catalog-leaf)。

`version`属性是在包.nuspec 中找到的原始版本字符串。

`published`属性是包被删除时，这通常是作为目录项的提交时间戳之前的短时间的时间。

#### <a name="sample-request"></a>示例请求

获取 https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>概述

本部分介绍的客户端概念，尽管不一定是托管协议，但应为任何实际目录客户端实现的一部分。

因为目录是时间索引的仅限追加的数据结构，应存储在客户端**游标**本地，最多的时间点在客户端表示已处理目录项。 请注意，应永远不会使用客户端的计算机时钟生成此游标值。 相反，值应来自于目录对象的`commitTimestamp`值。

每次客户端想要处理的包源上的新事件，它需要仅查询目录的提交时间戳的所有目录项大于其存储的游标。 客户端已成功处理所有新的目录项后，它会记录作为它的新游标值只是处理目录项的最新的提交时间戳。

使用此方法，而客户端可以确保永远不会错过包源发生的任何包事件。
此外，客户端绝不会重新处理在游标的记录的提交时间戳之前的旧事件。

这一功能强大的游标概念用于许多 nuget.org 后台作业，用于使 V3 API 本身保持最新。 

### <a name="initial-value"></a>初始值

当目录客户端第一次启动 （并因此具有任何游标值） 时，它应使用默认游标的值。NET 的`System.DateTimeOffset.MinValue`或最小可表示的时间戳的一些此类类似概念。

### <a name="iterating-over-catalog-items"></a>循环访问目录项

若要查询下一组要处理的目录项，客户端应：

1. 从本地存储区中提取记录的游标值。
1. 下载并反序列化目录索引。
1. 查找所有目录页提交时间戳*大于*光标。
1. 声明目录项，以便处理空的列表。
1. 为在步骤 3 中匹配每个目录页：
   1. 下载并反序列化目录页。
   1. 查找所有目录项提交时间戳*大于*光标。
   1. 将所有匹配的目录项添加到在步骤 4 中声明的列表。
1. 对目录项列表按提交时间戳进行排序。
1. 按顺序处理每个目录项：
   1. 下载并反序列化的目录项目。
   1. 相应地作出反应到目录项的类型。
   1. 处理目录项文档以特定于客户端的方式。
1. 记录为的新游标值的最后一个目录项的提交时间戳。

使用此基本算法，客户端实现可以构建包源上可用的所有包的完整视图。 客户端仅需要执行此算法会定期以始终要清楚的包源的最新更改。

> [!Note]
> 这是算法的 nuget.org 用来保持[包元数据](registration-base-url-resource.md)，[包内容](package-base-address-resource.md)，[搜索](search-query-service-resource.md)并[记忆式键入功能](search-autocomplete-service-resource.md)最新的资源。

### <a name="dependent-cursors"></a>依赖的游标

假设有两个目录客户端具有固有的依赖关系，其中一个客户端的输出取决于另一个客户端的输出。 

#### <a name="example"></a>示例

例如，在 nuget.org 上的新发布的包不应出现在搜索资源才会出现在包元数据资源。 这是因为"还原"操作执行的官方 NuGet 客户端使用的包元数据资源。 如果客户将发现使用搜索服务包，他们应能够成功还原该包使用的包元数据资源。 换而言之，搜索资源依赖于包元数据资源。 每个资源都有目录客户端后台作业，更新该资源。 每个客户端具有其自己的光标。

由于这两个资源是从目录更新搜索资源的目录客户端游标*必须不超过*包元数据目录客户端游标。

#### <a name="algorithm"></a>算法

若要实现这一限制，只需修改上面为算法：

1. 从本地存储区中提取记录的游标值。
1. 下载并反序列化目录索引。
1. 查找所有目录页提交时间戳*大于*光标**小于或等于依赖项的游标。**
1. 声明目录项，以便处理空的列表。
1. 为在步骤 3 中匹配每个目录页：
   1. 下载并反序列化目录页。
   1. 查找所有目录项提交时间戳*大于*光标**小于或等于依赖项的游标。**
   1. 将所有匹配的目录项添加到在步骤 4 中声明的列表。
1. 对目录项列表按提交时间戳进行排序。
1. 按顺序处理每个目录项：
   1. 下载并反序列化的目录项目。
   1. 相应地作出反应到目录项的类型。
   1. 处理目录项文档以特定于客户端的方式。
1. 记录为的新游标值的最后一个目录项的提交时间戳。

使用此修改后的算法，您可以构建系统的依赖目录客户端的所有生成其自己的特定索引、 项目等。
