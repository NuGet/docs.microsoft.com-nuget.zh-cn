---
title: 目录资源，NuGet V3 API
description: 目录是在 nuget.org 上创建和删除的所有包的索引。
author: joelverhagen
ms.author: jver
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6c04453fec9beb7b0998953384ec60694e1213c1
ms.sourcegitcommit: af059dc776cfdcbad20baab2919b5d6dc1e9022d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "99990160"
---
# <a name="catalog"></a>目录

**目录** 是记录包源上所有包操作（如创建和删除）的资源。 目录资源的 `Catalog` [服务索引](service-index.md)中包含类型。 您可以使用此资源 [查询所有已发布的包](../guides/api/query-for-all-published-packages.md)。

> [!Note]
> 由于官方 NuGet 客户端不使用目录，因此并非所有包源都实现目录。

> [!Note]
> 目前，nuget.org 目录在中国不可用。 有关更多详细信息，请参阅 [NuGet/NuGetGallery # 4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值   | 注释
------------- | -----
Catalog/3.0。0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的入口点 URL 是 `@id` 与上述资源值关联的属性的值 `@type` 。 本主题使用占位符 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

在目录资源中找到的所有 Url 仅支持 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="catalog-index"></a>目录索引

目录索引是众所周知位置的文档，其中包含目录项列表，按时间顺序排列。 它是目录资源的入口点。

此索引由目录页组成。 每个目录页面都包含目录项。 每个目录项都表示一个事件，该事件涉及到某个时间点的单个包。 目录项可以表示从包源创建、未列出、重新列出或删除的包。 通过按时间顺序处理目录项，客户端可以生成在 V3 包源上存在的每个包的最新视图。

简而言之，目录 blob 具有以下层次结构：

- **Index**：目录的入口点。
- **页面**：目录项的分组。
- **叶**：表示目录项的文档，该目录项是单个包状态的快照。

每个目录对象都有一个名为的属性，该属性 `commitTimeStamp` 表示将项添加到目录的时间。 目录项将添加到名为 "提交" 的批次的目录页中。 同一提交中的所有目录项都具有相同的提交时间戳 (`commitTimeStamp`) 并提交 ID (`commitId`) 。 放置在同一提交中的目录项表示在包源上的同一时间点附近发生的事件。 目录提交中没有排序。

由于每个包 ID 和版本都是唯一的，因此在一个提交中将永远不会有多个目录项。 这可确保单个包的目录项始终可以明确地按提交时间戳进行排序。

每个目录的提交永远不会超过一个 `commitTimeStamp` 。 换言之， `commitId` 是的冗余 `commitTimeStamp` 。

与按包 ID 编制索引的 [包元数据资源](registration-base-url-resource.md)不同，目录 (，只按时间) 查询。

目录项始终按单调递增的时间顺序添加到目录中。 这意味着，如果在时间 X 添加目录提交，则不会使用小于或等于 X 的时间来添加目录提交。

以下请求将获取目录索引。

```
GET {@id}
```

目录索引是一个 JSON 文档，其中包含具有以下属性的对象：

名称            | 类型             | 必须 | 注释
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 与最新提交关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 最近提交的时间戳
count           | integer          | 是      | 索引中的页数
items           | 对象数组 | 是      | 对象的数组，每个对象表示一个页

数组中的每个元素 `items` 都是一个对象，其中包含有关每个页面的一些最少的详细信息。 这些页面对象不包含目录 (项) 。 未定义此数组中元素的顺序。 客户端可以使用其属性在内存中对页面进行排序 `commitTimeStamp` 。

随着新页的引入， `count` 将递增，新的对象将出现在数组中 `items` 。

在将项添加到目录中时，索引的 `commitId` 将会更改，并且 `commitTimeStamp` 将增加。 这两个属性本质上是对 `commitId` 数组中所有页面和值的汇总 `commitTimeStamp` `items` 。

### <a name="catalog-page-object-in-the-index"></a>索引中的目录页对象

在目录索引的属性中找到的目录页对象 `items` 具有以下属性：

名称            | 类型    | 必须 | 注释
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 要提取目录页的 URL
commitId        | 字符串  | 是      | 与此页中的最新提交关联的唯一 ID
commitTimeStamp | 字符串  | 是      | 此页中的最新提交的时间戳
count           | integer | 是      | 目录页中的项数

与 [包元数据资源](registration-base-url-resource.md) 相比，在某些情况下，inlines 留在索引中，目录叶从不内联到索引中，必须始终使用页面的 URL 来提取 `@id` 。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/catalog0/index.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>目录页

"目录" 页是目录项的集合。 它是使用 `@id` 目录索引中找到的值之一提取的文档。 目录页的 URL 不应是可预测的，只应使用目录索引来发现。

新的目录项仅添加到具有最高提交时间戳或新页的目录索引页面。 将具有较高提交时间戳的页面添加到目录后，将永远不会将较旧的页面添加到或更改。

目录页文档是包含以下属性的 JSON 对象：

名称            | 类型             | 必须 | 注释
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 与此页中的最新提交关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 此页中的最新提交的时间戳
count           | integer          | 是      | 页面中的项目数
items           | 对象数组 | 是      | 此页中的目录项
父级 (parent)          | 字符串           | 是      | 目录索引的 URL

数组中的每个元素 `items` 都是一个对象，其中包含有关目录项的一些最少的详细信息。 这些项对象不包含目录项的所有数据。 页的数组中项的顺序 `items` 未定义。 客户端可以使用其属性在内存中对项进行排序 `commitTimeStamp` 。

页中目录项的数目由服务器实现定义。 对于 nuget.org，每个页面中最多包含550个项目，但对于某些页面，实际数字可能较小，具体取决于下一个提交批处理的时间点大小。

引入新项 `count` 后，会递增，新目录项对象会出现在数组中 `items` 。

当向页面添加项时，所 `commitId` 做的更改和将 `commitTimeStamp` 增加。 这两个属性本质上是对 `commitId` 数组中所有和值的汇总 `commitTimeStamp` `items` 。

### <a name="catalog-item-object-in-a-page"></a>页面中的目录项对象

在目录页的属性中找到的目录项对象 `items` 具有以下属性：

名称            | 类型    | 必须 | 注释
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 要提取目录项的 URL
@type           | 字符串  | 是      | 目录项的类型
commitId        | 字符串  | 是      | 与此目录项关联的提交 ID
commitTimeStamp | 字符串  | 是      | 此目录项的提交时间戳
nuget： id        | 字符串  | 是      | 此叶相关的包 ID
nuget：版本   | 字符串  | 是      | 此叶相关的包版本

`@type`该值将是以下两个值之一：

1. `nuget:PackageDetails`：对应于 `PackageDetails` 目录叶文档中的类型。
1. `nuget:PackageDelete`：对应于 `PackageDelete` 目录叶文档中的类型。

有关每种类型含义的更多详细信息，请参阅下面的 [相应项类型](#item-types) 。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目录叶

目录叶包含某些时间点特定包 ID 和版本的相关元数据。 它是使用 `@id` 目录页中的值提取的文档。 目录叶的 URL 不应是可预测的，应仅使用目录页来发现。

目录叶文档是包含以下属性的 JSON 对象：

名称                    | 类型                       | 必须 | 注释
----------------------- | -------------------------- | -------- | -----
@type                   | 字符串或字符串数组 | 是      | 目录项 (s) 类型
目录： commitId        | 字符串                     | 是      | 与此目录项关联的提交 ID
目录： commitTimeStamp | 字符串                     | 是      | 此目录项的提交时间戳
id                      | 字符串                     | 是      | 目录项的包 ID
published               | 字符串                     | 是      | 包目录项的发布日期
版本                 | 字符串                     | 是      | 目录项的包版本

### <a name="item-types"></a>项类型

`@type`属性是字符串或字符串数组。 为方便起见，如果 `@type` 值为字符串，则应将其视为大小为1的任意数组。 并非的所有可能值 `@type` 都有记录。 但是，每个目录项都有以下两个字符串类型值中的一个：

1. `PackageDetails`：表示包元数据的快照
1. `PackageDelete`：表示已删除的包

### <a name="package-details-catalog-items"></a>包详细信息目录项

类型为的目录项 `PackageDetails` 包含特定包的包元数据的快照 (ID 和版本组合) 。 包源遇到以下任何情况时，将生成包详细信息目录项：

1. **推送** 包。
1. 已 **列出** 包。
1. 未 **列出** 包。
1. 包为 **重排**。

包重排是一种管理手势，它实质上生成了现有包的虚设推送，无对包本身的任何更改。 在 nuget.org 上，在使用目录的后台作业之一中修复 bug 后，将使用重排。

使用目录项的客户端不应尝试确定哪些方案生成了目录项。 相反，客户端只需用目录项中包含的元数据更新任何已维护的视图或索引。 此外，应妥善处理重复或冗余的目录项 (幂等方式) 。

包详细信息目录项除 [包含在所有目录叶上](#catalog-leaf)的属性外，还具有以下属性。

名称                    | 类型                       | 必须 | 注释
----------------------- | -------------------------- | -------- | -----
作者                 | string                     | 否       |
created                 | string                     | 否       | 首次创建包时的时间戳。 回退属性： `published` 。
dependencyGroups        | 对象数组           | 否       | 包的依赖项按目标框架分组 (与 [包元数据资源的格式相同](registration-base-url-resource.md#package-dependency-group)) 
弃用             | 对象 (object)                     | 否       | 与包关联的弃用 (与 [包元数据资源相同的格式](registration-base-url-resource.md#package-deprecation)) 
description             | 字符串                     | 否       |
iconUrl                 | 字符串                     | 否       |
isPrerelease            | boolean                    | 否       | 包版本是否为预发布版本。 可以从中检测到 `version` 。
语言                | 字符串                     | 否       |
licenseUrl              | string                     | 否       |
列出                  | boolean                    | 否       | 是否列出包
minClientVersion        | string                     | 否       |
packageHash             | 字符串                     | 是      | 包哈希，使用[标准基 64](https://tools.ietf.org/html/rfc4648#section-4)编码
packageHashAlgorithm    | 字符串                     | 是      |
packageSize             | integer                    | 是      | 包的大小（以字节为单位） nupkg
packageTypes            | 对象数组           | 否       | 作者指定的包类型。
projectUrl              | string                     | 否       |
releaseNotes            | string                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假设 `false` 排除
摘要                 | string                     | 否       |
tags                    | 字符串数组           | 否       |
title                   | 字符串                     | 否       |
verbatimVersion         | string                     | 否       | 最初在中找到的版本字符串。 nuspec
漏洞         | 对象数组           | 否       | 包的安全漏洞

Package `version` 属性是规范化后的完整版本字符串。 这意味着，可以在此处包括 SemVer 2.0.0 生成数据。

`created`时间戳是包源首次接收包时的时间戳，通常是目录项的提交时间戳之前的短暂时间。

`packageHashAlgorithm`是一个由服务器实现定义的字符串，该字符串表示用于生成的哈希算法 `packageHash` 。 nuget.org 始终使用的 `packageHashAlgorithm` 值 `SHA512` 。

`packageTypes`仅当作者指定了包类型时，才会显示该属性。 如果存在，它将始终至少具有一个 (1) 条目。 数组中的每一项 `packageTypes` 都是具有以下属性的 JSON 对象：

名称      | 类型    | 必须 | 注释
--------- | ------- | -------- | -----
name      | 字符串  | 是      | 包类型的名称。
版本    | string  | 否       | 包类型的版本。 只有在作者显式指定了 nuspec 中的版本时，才会出现此情况。

`published`时间戳是上次列出包的时间。

> [!Note]
> 在 nuget.org 上， `published` 当包未列出时，该值将设置为1900年。

#### <a name="vulnerabilities"></a>漏洞

一个 `vulnerability` 对象数组。 每个漏洞具有以下属性：

名称         | 类型   | 必须 | 注释
------------ | ------ | -------- | -----
advisoryUrl  | 字符串 | 是      | 包安全公告的位置
severity     | 字符串 | 是      | 公告的严重性： "0" = Low，"1" = 中等，"2" = 高，"3" = 严重

如果 `severity` 属性包含的值不是此处所列的值，则建议将其严重性视为 Low。

#### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>包删除目录项

类型为的目录项 `PackageDelete` 包含一组最小的信息，用于对客户端进行分类，指出包已从包源中删除，并且不再可用于任何包操作 (如 restore) 。

> [!NOTE]
> 包可能会被删除，以后使用相同的包 ID 和版本重新发布。 在 nuget.org 上，这种情况非常罕见，因为它打破了某个包 ID 和版本表示特定包内容的正式客户端假设。 有关 nuget.org 上的包删除的详细信息，请参阅 [策略](../nuget-org/policies/deleting-packages.md)。

除了 [所有目录叶上包含](#catalog-leaf)的属性外，包删除目录项还没有其他属性。

`version`属性是在 nuspec 中找到的原始版本字符串。

`published`属性是删除包的时间，通常是目录项的提交时间戳之前的短暂时间。

#### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json
```

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>游标

### <a name="overview"></a>概述

本部分介绍了尽管协议不一定是由协议强制的客户端概念，但它应是任何实际的目录客户端实现的一部分。

由于目录是按时间编制索引的仅限追加的数据结构，因此客户端应在本地存储 **游标** ，这表示客户端处理目录项的时间点。 请注意，此游标值永远不应使用客户端的计算机时钟生成。 相反，该值应来自目录对象的 `commitTimestamp` 值。

每当客户端想要处理包源上的新事件时，它只需查询其提交时间戳大于其存储游标的所有目录项的目录。 当客户端成功处理所有新的目录项后，它会记录刚刚作为新的游标值处理的目录项的最新提交时间戳。

使用此方法，客户端可以确保永远不会错过包源上发生的任何包事件。
此外，客户端永远不需要在游标记录的提交时间戳之前重新处理旧事件。

这一功能强大的游标概念用于 nuget.org 后台作业，并用于使 V3 API 本身保持最新。 

### <a name="initial-value"></a>初始值

当目录客户端首次启动时，如果 (，因此没有游标值) ，则它应使用的默认游标值。NET `System.DateTimeOffset.MinValue` 或一些这种类似的最小表示时间戳概念。

### <a name="iterating-over-catalog-items"></a>遍历目录项

若要查询下一组要处理的目录项，客户端应：

1. 从本地存储提取记录的游标值。
1. 下载并反序列化目录索引。
1. 查找提交时间戳 *大于* 游标的所有目录页。
1. 声明要处理的目录项的空列表。
1. 对于步骤3中匹配的每个目录页：
   1. 下载并反序列化目录页。
   1. 查找提交时间戳 *大于* 游标的所有目录项。
   1. 将所有匹配目录项添加到步骤4中声明的列表。
1. 按提交时间戳对目录项列表进行排序。
1. 按顺序处理每个目录项：
   1. 下载并反序列化目录项。
   1. 对目录项的类型做出适当的反应。
   1. 以客户端特定的方式处理目录项文档。
1. 将最后一个目录项的提交时间戳记录为新的游标值。

使用此基本算法，客户端实现可以生成包源上可用的所有包的完整视图。 客户端只需要定期执行此算法，以便始终了解包源的最新更改。

> [!Note]
> 这是 nuget.org 用于保持 [包元数据](registration-base-url-resource.md)、 [包内容](package-base-address-resource.md)、 [搜索](search-query-service-resource.md) 和 [自动完成](search-autocomplete-service-resource.md) 资源最新的算法。

### <a name="dependent-cursors"></a>依赖游标

假设有两个目录客户端具有固有的依赖项，其中一个客户端的输出依赖于另一个客户端的输出。 

#### <a name="example"></a>示例

例如，在 nuget.org 上，新发布的包在包元数据资源中出现之前不应出现在搜索资源中。 这是因为官方 NuGet 客户端执行的 "还原" 操作使用包元数据资源。 如果客户使用搜索服务发现包，他们应该能够使用包元数据资源成功还原该包。 换句话说，搜索资源依赖于包元数据资源。 每个资源都有一个更新该资源的目录客户端后台作业。 每个客户端都有自己的游标。

由于这两个资源都是从目录中生成的，因此，更新搜索资源的目录客户端的游标 *不得超出* 包元数据目录客户端的光标。

#### <a name="algorithm"></a>算法

若要实现此限制，只需将上述算法修改为：

1. 从本地存储提取记录的游标值。
1. 下载并反序列化目录索引。
1. 查找提交时间戳 *大于***或等于依赖项的游标** 的所有目录页。
1. 声明要处理的目录项的空列表。
1. 对于步骤3中匹配的每个目录页：
   1. 下载并反序列化目录页。
   1. 查找提交时间戳 *大于***或等于依赖项的游标** 的所有目录项。
   1. 将所有匹配目录项添加到步骤4中声明的列表。
1. 按提交时间戳对目录项列表进行排序。
1. 按顺序处理每个目录项：
   1. 下载并反序列化目录项。
   1. 对目录项的类型做出适当的反应。
   1. 以客户端特定的方式处理目录项文档。
1. 将最后一个目录项的提交时间戳记录为新的游标值。

使用此修改后的算法，可以生成依赖目录客户端的系统，所有这些客户端都生成其自己的特定索引、项目等。
