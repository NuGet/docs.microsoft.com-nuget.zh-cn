---
title: 包内容，NuGet API
description: 包基址是一个简单的接口，用于提取包本身。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773934"
---
# <a name="package-content"></a>包内容

可以生成一个 URL，使用 V3 API)  (获取任意包的内容。 用于提取包内容的资源是 `PackageBaseAddress` 在 [服务索引](service-index.md)中找到的资源。 此资源还允许发现包的所有版本、列出或未列出。

此资源通常称为 "包基址" 或 "平面容器"。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值              | 说明
------------------------ | -----
PackageBaseAddress/3.0。0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是 `@id` 与上述资源值关联的属性的值 `@type` 。 在下面的文档中，将使用占位符基 URL `{@id}` 。

## <a name="http-methods"></a>HTTP 方法

注册资源中找到的所有 Url 都支持 HTTP 方法 `GET` 和 `HEAD` 。

## <a name="enumerate-package-versions"></a>枚举包版本

如果客户端知道包 ID 并想要发现包源有哪些包版本可用，则客户端可以构造可预测的 URL 来枚举所有包版本。 此列表应为下述包内容 API 的 "目录列表"。

> [!Note]
> 此列表包含列出和未列出的包版本。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>请求参数

名称     | In     | 类型    | 必须 | 注释
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 是      | 包 ID lowercased

`LOWER_ID`值是所需的包 ID lowercased，它使用由实现的规则。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 方法。

### <a name="response"></a>响应

如果包源没有提供的包 ID 版本，则返回404状态代码。

如果包源有一个或多个版本，则返回200状态代码。 响应正文是包含以下属性的 JSON 对象：

名称     | 类型             | 必须 | 注释
-------- | ---------------- | -------- | -----
versions | 字符串数组 | 是      | 可用版本

数组中的字符串 `versions` 是所有 lowercased 的 [规范化 NuGet 版本字符串](../concepts/package-versioning.md#normalized-version-numbers)。 版本字符串不包含任何 SemVer 2.0.0 生成元数据。

目的在于，在此数组中找到的版本字符串可以逐字用于 `LOWER_VERSION` 以下终结点中的标记。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a>示例响应

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下载包内容 ( nupkg) 

如果客户端知道包 ID 和版本并想要下载包内容，则它们只需构造以下 URL：

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a>请求参数

名称          | In     | 类型   | 必须 | 注释
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID，小写
LOWER_VERSION | URL    | string | 是      | 包版本（正常化和 lowercased）

`LOWER_ID`和 `LOWER_VERSION` 都是使用实现的规则 lowercased 的。网络[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)
方法。

`LOWER_VERSION`是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。

### <a name="response-body"></a>响应正文

如果包源上存在包，则返回200状态代码。 响应正文将是包内容本身。

如果包源中不存在包，则返回404状态代码。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a>示例响应

作为 Newtonsoft.Js上的的二进制流。

## <a name="download-package-manifest-nuspec"></a> ( 下载包清单。 nuspec) 

如果客户端知道包 ID 和版本并想要下载包清单，则它们只需构造以下 URL：

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a>请求参数

名称          | In     | 类型   | 必须 | 注释
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID，小写
LOWER_VERSION | URL    | string | 是      | 包版本（正常化和 lowercased）

`LOWER_ID`和 `LOWER_VERSION` 都是使用实现的规则 lowercased 的。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) 方法。

`LOWER_VERSION`是使用 NuGet 的版本[规范化规则](../concepts/package-versioning.md#normalized-version-numbers)规范化的所需包版本。 这意味着，在这种情况下必须排除 SemVer 2.0.0 规范允许的生成元数据。

### <a name="response-body"></a>响应正文

如果包源上存在包，则返回200状态代码。 响应正文将为包清单，即 nuspec 中包含的 nupkg。 Nuspec 是一个 XML 文档。

如果包源中不存在包，则返回404状态代码。

### <a name="sample-request"></a>示例请求

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a>示例响应

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
