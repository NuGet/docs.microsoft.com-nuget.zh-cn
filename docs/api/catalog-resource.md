---
title: 目录资源，NuGet V3 API
description: 目录是创建和删除在 nuget.org 上的所有包的索引。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/30/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8554f9515b671dbececd94a025ec7e56037c2bd9
ms.sourcegitcommit: 055248d790051774c892b220eca12015babbd668
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
ms.locfileid: "34152430"
---
# <a name="catalog"></a>Catalog

**目录**是记录上的包源，如创建和删除的所有包操作的资源。 目录资源具有`Catalog`键入[服务索引](service-index.md)。

> [!Note]
> 由于官方 NuGet 客户端不使用该目录，并非所有包源都实现目录。

> [!Note]
> 目前，nuget.org 目录不是在中国提供的。 有关更多详细信息，请参阅[NuGet/NuGetGallery #4949](https://github.com/NuGet/NuGetGallery/issues/4949)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值   | 说明
------------- | -----
Catalog/3.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的入口点 URL 是值的`@id`与前面提到的资源关联的属性`@type`值。 本主题使用的占位符 URL `{@id}`。

## <a name="http-methods"></a>HTTP 方法

只有的 HTTP 方法位于目录资源支持的所有 Url`GET`和`HEAD`。

## <a name="catalog-index"></a>目录索引

目录索引是众所周知的位置具有目录项，按时间顺序排序的列表中的文档。 它是目录资源的入口点。

索引组成目录页。 每个目录页包含目录项。 每个目录项表示时间有关的某个点单个包的事件。 目录项可以表示已创建，未列出的、 重新列，或已删除程序包源中的包。 通过处理按时间顺序的目录项，客户端可以生成 V3 包源上存在的每个包的最新视图。

简单地说，目录的 blob 具有以下层次结构：

- **索引**: 目录的入口点。
- **页**： 目录项的分组。
- **叶**： 表示一个目录项，它是单个包的状态的快照的文档。

每个目录对象具有一个名为属性`commitTimeStamp`表示项添加到目录时。 目录项添加到名为提交的批次中的目录页中。 中的相同的提交的所有目录项都具有相同的提交时间戳 (`commitTimeStamp`) 并提交 ID (`commitId`)。 目录项放置在同一个提交表示时间上的包源绕相同点发生的事件。 目录提交内没有排序。

因为每个包 ID 和版本是唯一的将永远不会有多个目录项目中提交。 这可确保，在单个包的目录项可以始终是明确相对于排序的提交时间戳。

永远不会将多个提交给每个目录`commitTimeStamp`。 换而言之，`commitId`是冗余的`commitTimeStamp`。

与此相反[package 元数据资源](registration-base-url-resource.md)，哪些索引按包 ID，该目录是索引 （和可查询） 只能由时间。

目录项始终添加到单调递增，按时间顺序排列的顺序目录中。 这意味着，如果在时间 X 添加目录提交，则没有目录提交将不断添加带有时间小于或等于为 X。

以下请求获取目录索引。

    GET {@id}

目录索引是包含具有以下属性的对象的 JSON 文档：

名称            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 与最新提交关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 最新的提交时间戳
count           | 整数          | 是      | 在索引中的页面数
项           | 对象的数组 | 是      | 对象，表示页每个对象的数组

在每个元素`items`数组是具有一些有关每个页面的最小的详细信息的对象。 这些页对象不包含目录叶 （项）。 未定义此数组中元素的顺序。 可以按内存使用中的客户端排序页其`commitTimeStamp`属性。

引入新的页，`count`将递增，并且新的对象将会显示在`items`数组。

将项目添加到目录，索引的`commitId`将更改和`commitTimeStamp`将增加。 这两个属性均通过所有页实质上是摘要`commitId`和`commitTimeStamp`中值`items`数组。

### <a name="catalog-page-object-in-the-index"></a>在索引中的目录 page 对象

目录索引中找到的目录页对象`items`属性具有以下属性：

名称            | 类型    | 必需 | 说明
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 到提取目录页 URL
commitId        | 字符串  | 是      | 在此页中的最新提交与关联的唯一 ID
commitTimeStamp | 字符串  | 是      | 在此页中的最新提交的时间戳
count           | 整数 | 是      | 在目录页中的项的数目

与此相反[package 元数据资源](registration-base-url-resource.md)这在某些情况下，内联离开到索引，因此目录叶是永远不会内联到索引，始终必须通过使用页面的提取`@id`URL。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/catalog0/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-index.json](./_data/catalog-index.json)]

## <a name="catalog-page"></a>目录页

目录页是目录项的集合。 这是提取使用之一的文档`@id`目录索引中找到的值。 目录页的 URL 不应为可预测，并应使用只是目录索引发现。

中只能与最高的提交时间戳的目录索引页或到新页添加新的目录项。 一旦具有更高版本的提交时间戳的页添加到目录中，较早的页面永远不会添加或更改。

编录页文档是具有以下属性的 JSON 对象：

名称            | 类型             | 必需 | 说明
--------------- | ---------------- | -------- | -----
commitId        | 字符串           | 是      | 在此页中的最新提交与关联的唯一 ID
commitTimeStamp | 字符串           | 是      | 在此页中的最新提交的时间戳
count           | 整数          | 是      | 在页中的项的数目
项           | 对象的数组 | 是      | 此页中的目录项
父          | 字符串           | 是      | 指向目录索引的 URL

在每个元素`items`数组是具有一些有关的目录项的最小的详细信息的对象。 这些项对象不包含的所有目录项的数据。 在页中的项的顺序`items`未定义数组。 项目可以使用的内存中的客户端经过排序其`commitTimeStamp`属性。

在页中的目录项的数目由服务器实现定义。 对于 nuget.org，有最多 550 项在每个页中，尽管可能及时更小，以具体的点处的下一步提交批的大小取决于一些页的实际数目。

引入新的项，`count`是递增和新的目录项对象会显示在`items`数组。

将项目添加到页中，`commitId`更改和`commitTimeStamp`会增加。 这两个属性均通过所有实质上是摘要`commitId`和`commitTimeStamp`中值`items`数组。

### <a name="catalog-item-object-in-a-page"></a>目录在页中的项对象

在目录页中找到的目录项对象`items`属性具有以下属性：

名称            | 类型    | 必需 | 说明
--------------- | ------- | -------- | -----
@id             | 字符串  | 是      | 要提取的目录项的 URL
@type           | 字符串  | 是      | 目录项的类型
commitId        | 字符串  | 是      | 与此目录项关联的提交 ID
commitTimeStamp | 字符串  | 是      | 此目录项的提交时间戳
nuget:id        | 字符串  | 是      | 与此叶包 ID
nuget:version   | 字符串  | 是      | 与此叶包版本

`@type`值将为以下两个值之一：

1. `nuget:PackageDetails`： 这对应于`PackageDetails`目录叶文档中的类型。
1. `nuget:PackageDelete`： 这对应于`PackageDelete`目录叶文档中的类型。

有关详细信息的链接，意味着每个类型，请参阅[对应项类型](#item-types)下面。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3/catalog0/page2926.json

### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-page.json](./_data/catalog-page.json)]

## <a name="catalog-leaf"></a>目录叶

目录叶及时包含有关特定包 ID 和在某一时刻的版本的元数据。 这是提取使用的文档`@id`值在目录页中找到。 目录叶的 URL 不应为可预测，并且应使用仅目录页发现。

编录叶文档是具有以下属性的 JSON 对象：

名称                    | 类型                       | 必需 | 说明
----------------------- | -------------------------- | -------- | -----
@type                   | 字符串或字符串数组 | 是      | 目录项的类型
catalog:commitId        | 字符串                     | 是      | 与此目录项关联的提交 ID
catalog:commitTimeStamp | 字符串                     | 是      | 此目录项的提交时间戳
id                      | 字符串                     | 是      | 目录项的包 ID
发布               | 字符串                     | 是      | 包的目录项目发布的日期
version                 | 字符串                     | 是      | 目录项的包版本

### <a name="item-types"></a>项类型

`@type`属性是由字符串的数组。 为方便起见，如果`@type`值是一个字符串，它应视为一个大小的任何数组。 并非所有可能值`@type`中进行了说明。 但是，每个目录项具有完全的两个以下的字符串类型值之一：

1. `PackageDetails`： 表示包元数据的快照
1. `PackageDelete`： 表示已删除的包

### <a name="package-details-catalog-items"></a>包的详细信息的目录项

目录项类型的`PackageDetails`包含特定包 （ID 和版本组合） 的包元数据的快照。 如果包源遇到下列任一情况，则会生成对包的详细信息的目录项目：

1. 包是**推送**。
1. 包是**列出**。
1. 包是**未列出**。
1. 包是**重排**。

包重排是实质上是生成到包本身不进行任何更改的现有包的假推送管理手势。 在 nuget.org，重排 bug 修复使用该目录的后台作业之一后使用。

客户端使用的目录项不应尝试来确定哪种方案生成的目录项。 相反，客户端应只需使用更新任何维护的视图或索引中的目录项，包含的元数据。 此外，应适当处理重复或冗余目录项 （幂等方式）。

包详细信息目录项具有以下属性除了[包含在所有目录叶](#catalog-leaf)。

名称                    | 类型                       | 必需 | 说明
----------------------- | -------------------------- | -------- | -----
作者                 | 字符串                     | 否       |
created                 | 字符串                     | 否       | 首次创建包的时间戳。 回退属性： `published`。
dependencyGroups        | 对象的数组           | 否       | 相同的格式设置为[package 元数据资源](registration-base-url-resource.md#package-dependency-group)
说明             | 字符串                     | 否       |
iconUrl                 | 字符串                     | 否       |
isPrerelease            | boolean                    | 否       | 是否是预发布的包版本。 可以从检测到`version`。
语言                | 字符串                     | 否       |
licenseUrl              | 字符串                     | 否       |
列出                  | boolean                    | 否       | 该程序包是否将列
minClientVersion        | 字符串                     | 否       |
packageHash             | 字符串                     | 是      | 使用编码的包的哈希[标准 base 64](https://tools.ietf.org/html/rfc4648#section-4)
packageHashAlgorithm    | 字符串                     | 是      |
packageSize             | 整数                    | 是      | 包.nupkg 以字节为单位的大小
projectUrl              | 字符串                     | 否       |
releaseNotes            | 字符串                     | 否       |
requireLicenseAgreement | boolean                    | 否       | 假定`false`如果排除
摘要                 | 字符串                     | 否       |
标记                    | 字符串数组           | 否       |
标题                   | 字符串                     | 否       |
verbatimVersion         | 字符串                     | 否       | 因为它的版本字符串最初位于.nuspec

包`version`属性是完整的规范化的版本字符串。 这意味着，SemVer 2.0.0 生成数据可以是包含此处。

`created`时间戳是包源，这通常是目录项的提交时间戳之前短暂地先接收包的时间。

`packageHashAlgorithm`是由表示用于生成的哈希算法的服务器实现定义的字符串`packageHash`。 始终使用 nuget.org`packageHashAlgorithm`值`SHA512`。

`published`时间戳是上次列出包的时间。

> [!Note]
> 在 nuget.org，`published`值设置为 1900 年包时未列出。

#### <a name="sample-request"></a>示例请求

获取 https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-details.json](./_data/catalog-package-details.json)]

### <a name="package-delete-catalog-items"></a>包删除目录项

目录项类型的`PackageDelete`包含指明向目录客户端包从包源已被删除并且不再可用于任何包的操作 （如还原） 的信息的最小集。

> [!Note]
> 它是要删除的包和更高版本重新发布使用的相同包 ID 和版本的可能。 在 nuget.org，这是极少数情况下，因为这将打断包 ID 和版本表示特定包内容的正式客户端的假设。 有关删除该包在 nuget.org 上的详细信息，请参阅[我们策略](../policies/deleting-packages.md)。

包删除目录项不包含其他属性除了[包含在所有目录叶](#catalog-leaf)。

`version`属性是在包.nuspec 中找到的原始版本字符串。

`published`属性是当删除包，这通常是为目录项的提交时间戳之前的短时间的时间。

#### <a name="sample-request"></a>示例请求

获取 https://api.nuget.org/v3/catalog0/data/2017.11.02.00.40.00/netstandard1.4_lib.1.0.0-test.json

#### <a name="sample-response"></a>示例响应

[!code-JSON [catalog-package-delete.json](./_data/catalog-package-delete.json)]

## <a name="cursor"></a>Cursor

### <a name="overview"></a>概述

本部分介绍了一个客户端的概念，尽管不一定由该协议，规定应该是任何实际目录客户端实现的一部分。

由于该目录是按时间编制索引的仅限附加的数据结构，应将存储客户端**光标**本地，最多的时间点客户端表示已处理的目录项。 请注意，应永远不会使用客户端的计算机时钟生成此光标值。 相反，值应来自目录对象的`commitTimestamp`值。

每次客户端想要处理的包源上的新事件，它需要仅查询目录的所有目录项，提交时间戳大于其存储的光标。 客户端已成功处理所有新的目录项后，它记录只作为其新光标值处理的目录项的最新的提交时间戳。

使用此方法，而客户端可以确保永远不会丢失在包源发生的任何包事件。
此外，客户端从来不必重新处理旧事件之前光标的记录的提交时间戳。

此游标的非常强大的概念适用于许多 nuget.org 后台作业，用于使 V3 用 API 自身保持最新。 

### <a name="initial-value"></a>初始值

当目录客户端第一次启动 （并因此不具有任何游标值） 时，它应使用默认光标的值。NET 的`System.DateTimeOffset.MinValue`或某些最小可表示的时间戳的类似此类的概念。

### <a name="iterating-over-catalog-items"></a>循环访问目录项

若要查询的下一步的一套要处理的目录项，客户端应：

1. 从本地存储区中提取的记录的光标值。
1. 下载和反序列化的目录索引。
1. 查找所有目录提交时间戳的页*大于*光标。
1. 声明要处理的目录项的空列表。
1. 为在步骤 3 中匹配每个目录页：
   1. 下载和反序列化目录页。
   1. 查找所有目录项提交时间戳*大于*光标。
   1. 将所有匹配的目录项添加到在步骤 4 中声明的列表。
1. 目录项列表进行排序的提交时间戳。
1. 处理序列中的每个目录项：
   1. 下载和反序列化的目录项。
   1. 相应地作出反应到目录项的类型。
   1. 处理客户端特定方式中的目录项文档。
1. 记录作为新光标值的最后一个目录项的提交时间戳。

使用此基本算法，客户端实现可以生成的所有包可用包源上的完整视图。 客户端只需执行此算法定期需要始终注意的包源的最新更改。

> [!Note]
> 这是算法，该 nuget.org 用来保持[包元数据](registration-base-url-resource.md)，[包内容](package-base-address-resource.md)，[搜索](search-query-service-resource.md)和[记忆式键入功能](search-autocomplete-service-resource.md)最新的资源。

### <a name="dependent-cursors"></a>依赖的游标

假设有两个目录客户端具有的固有的依赖关系，其中一个客户端的输出取决于另一个客户端的输出。 

#### <a name="example"></a>示例

例如，在 nuget.org 上的新发布的包不应出现在搜索资源之前它将显示在包的元数据资源。 这是因为执行官方 NuGet 客户端的"还原"操作使用包元数据资源。 如果客户发现使用搜索服务包，它们应能够成功还原该包使用包元数据资源。 换而言之，搜索资源依赖于包元数据资源。 每个资源都有一个更新该资源的目录客户端后台作业。 每个客户端具有其自己的光标。

由于这两个资源生成从目录中，更新搜索资源的目录客户端游标中移出*必须不超过*包元数据目录客户端的光标。

#### <a name="algorithm"></a>算法

若要实现此限制，只需修改以上为算法：

1. 从本地存储区中提取的记录的光标值。
1. 下载和反序列化的目录索引。
1. 查找所有目录提交时间戳的页*大于*光标**小于或等于的依赖关系的光标。**
1. 声明要处理的目录项的空列表。
1. 为在步骤 3 中匹配每个目录页：
   1. 下载和反序列化目录页。
   1. 查找所有目录项提交时间戳*大于*光标**小于或等于的依赖关系的光标。**
   1. 将所有匹配的目录项添加到在步骤 4 中声明的列表。
1. 目录项列表进行排序的提交时间戳。
1. 处理序列中的每个目录项：
   1. 下载和反序列化的目录项。
   1. 相应地作出反应到目录项的类型。
   1. 处理客户端特定方式中的目录项文档。
1. 记录作为新光标值的最后一个目录项的提交时间戳。

使用此修改的算法，你可以构建系统依赖目录客户端的所有生成其自己的特定索引、 项目等。
