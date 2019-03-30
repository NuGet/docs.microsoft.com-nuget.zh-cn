---
title: 包详细信息 URL 模板，NuGet API
description: 包详细信息 URL 模板允许客户端 web 链接到更多包详细信息及其用户界面中显示
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638068"
---
# <a name="package-details-url-template"></a>包详细信息 URL 模板

就可以生成用户可以用来查看其 web 浏览器中的更多包详细信息的 URL 的客户端。 当包源想要显示的 NuGet 客户端应用程序的显示范围内可能容纳不下的包有关的其他信息时，这很有用。

用于生成此 URL 使用的资源是`PackageDetailsUriTemplate`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                     | 说明
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 初始版本

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不应代表用户向包的详细信息 URL 发出请求，但应支持 web 页`GET`方法，以允许单击的 URL 来轻松地在 web 浏览器中打开。

## <a name="construct-the-url"></a>构造的 URL

提供了已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应显示此构造的 URL （或可单击的链接） 向允许其用户若要打开 web 浏览器的 url，若要了解有关包的详细信息。 包详细信息页的内容取决于服务器实现。

该 URL 必须是绝对 URL，该方案 （协议） 必须是 HTTPS。

值`@id`索引服务中是一个包含任何以下占位符令牌的 URL 字符串：

### <a name="url-placeholders"></a>URL 占位符

名称        | 类型    | 必需 | 说明
----------- | ------- | -------- | -----
`{id}`      | string  | 否       | 要获取的详细信息的包 ID
`{version}` | string  | 否       | 要获取的详细信息的包版本

服务器应接受`{id}`和`{version}`任何大小写的值。 此外，服务器不应为版本是否为敏感[规范化](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)。 换而言之，应接受服务器还接受非规范化的版本。

例如，nuget.org 的包的详细信息模板如下所示：

    https://www.nuget.org/packages/{id}/{version}

如果客户端实现需要为 NuGet.Versioning 4.3.0 显示包详细信息的链接，它将产生以下 URL 并将其提供给用户：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
