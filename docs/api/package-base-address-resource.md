---
title: 包的内容，NuGet API
description: 包基址是提取包本身的一个简单接口。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2f0f93e0cee78ea03cbd53194cdc2a10871fd7e1
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426756"
---
# <a name="package-content"></a>包内容

就可以生成用于提取任意包的内容 （.nupkg 文件） 使用 V3 API 的 URL。 用于提取包内容的资源是`PackageBaseAddress`资源中找到[服务索引](service-index.md)。 此资源还允许包，列出的所有版本的发现或未列出。

此资源通常称为与任一"包基址"或"平面容器"。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值              | 说明
------------------------ | -----
PackageBaseAddress/3.0.0 | 初始版本

## <a name="base-url"></a>基 URL

以下 Api 的基 URL 是的值`@id`属性与前面提到的资源相关联`@type`值。 在以下文档中，占位符基 URL`{@id}`将使用。

## <a name="http-methods"></a>HTTP 方法

中的注册资源支持的 HTTP 方法找到的所有 Url`GET`和`HEAD`。

## <a name="enumerate-package-versions"></a>枚举的包版本

如果客户端知道包 ID，并想要发现的包版本包源具有可用，客户端可以构建一个可预测的 URL 来枚举所有包版本。 下面所述的内容包 API 的情况下，此列表应为"目录列表"。

> [!Note]
> 此列表包含这两个列出和取消列出包版本。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>请求参数

名称     | 内     | 类型    | 必需 | 说明
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 是      | 包 ID 小写

`LOWER_ID`值是小写使用通过实施的规则的所需的包 ID。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

### <a name="response"></a>响应

如果包源不具有提供的包 ID 的任何版本，则返回 404 状态代码。

如果包源具有一个或多个版本，则返回 200 状态代码。 响应正文是使用下面的属性的 JSON 对象：

名称     | 类型             | 必需 | 说明
-------- | ---------------- | -------- | -----
版本 | 字符串数组 | 是      | 包 Id 可用

中的字符串`versions`所有小写数组，[规范化 NuGet 版本字符串](../reference/package-versioning.md#normalized-version-numbers)。 版本字符串不包含任何 SemVer 2.0.0 生成元数据。

目的是，在此数组中找到的版本字符串可用于按原义`LOWER_VERSION`以下终结点中找到令牌。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>示例响应

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>下载包内容 (.nupkg)

如果客户端知道包 ID 和版本，并且想要下载包内容，只需构造以下 URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>请求参数

名称          | 内     | 类型   | 必需 | 说明
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID 小写
LOWER_VERSION | URL    | string | 是      | 包版本中，规范化和小写

这两`LOWER_ID`和`LOWER_VERSION`小写使用通过实施的规则。NET 的 [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
方法。

`LOWER_VERSION`所需的包版本规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。 这意味着必须在这种情况下排除允许的 SemVer 2.0.0 规范的生成元数据。

### <a name="response-body"></a>响应正文

如果包存在于包源，则返回 200 状态代码。 响应正文将为包内容本身。

如果包不存在对包源，则返回 404 状态代码。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>示例响应

Newtonsoft.Json 9.0.1.nupkg 二进制流。

## <a name="download-package-manifest-nuspec"></a>下载包清单 (.nuspec)

如果客户端知道包 ID 和版本，并且想要下载包清单，只需构造以下 URL:

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>请求参数

名称          | 内     | 类型   | 必需 | 说明
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 是      | 包 ID 小写
LOWER_VERSION | URL    | string | 是      | 包版本中，规范化和小写

这两`LOWER_ID`和`LOWER_VERSION`小写使用通过实施的规则。NET 的[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)方法。

`LOWER_VERSION`所需的包版本规范化使用 NuGet 的版本[规范化规则](../reference/package-versioning.md#normalized-version-numbers)。 这意味着必须在这种情况下排除允许的 SemVer 2.0.0 规范的生成元数据。

### <a name="response-body"></a>响应正文

如果包存在于包源，则返回 200 状态代码。 响应正文将为包清单，其中是包含在相应的.nupkg.nuspec。 .Nuspec 是一个 XML 文档。

如果包不存在对包源，则返回 404 状态代码。

### <a name="sample-request"></a>示例请求

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>示例响应

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
