---
title: 包详细信息 URL 模板，NuGet API
description: "\"包详细信息 URL\" 模板允许客户端在其 UI 中显示指向更多包详细信息的 web 链接"
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: aaeedea9750c11099b34e927bd8442656839d784
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773951"
---
# <a name="package-details-url-template"></a>包详细信息 URL 模板

客户端可能会生成一个 URL，用户可以使用该 URL 在其 web 浏览器中查看更多包详细信息。 当包源要显示与 NuGet 客户端应用程序所显示的范围不匹配的包的其他信息时，这非常有用。

用于生成此 URL 的资源是 `PackageDetailsUriTemplate` 在 [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值                     | 说明
------------------------------- | -----
PackageDetailsUriTemplate/5.1。0 | 初始版本

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不打算代表用户向包详细信息 URL 发出请求，但网页应支持方法，以便 `GET` 在 web 浏览器中轻松地打开已单击的 url。

## <a name="construct-the-url"></a>构造 URL

给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应显示此构造的 URL (或可单击的链接) 用户允许用户在 URL 中打开 web 浏览器并了解有关包的详细信息。 包详细信息页的内容由服务器实现确定。

URL 必须是绝对 URL，并且 (协议) 的方案必须为 HTTPS。

`@id`服务索引中的值是包含以下任何占位符标记的 URL 字符串：

### <a name="url-placeholders"></a>URL 占位符

名称        | 类型    | 必须 | 注释
----------- | ------- | -------- | -----
`{id}`      | string  | 否       | 要获取其详细信息的包 ID
`{version}` | string  | 否       | 要获取其详细信息的包版本

服务器应接受 `{id}` `{version}` 任何大小写形式的和值。 此外，服务器不应对版本是否 [规范化](../concepts/package-versioning.md#normalized-version-numbers)敏感。 换句话说，服务器还应接受非标准化版本。

例如，nuget 的包详细信息模板如下所示：

```http
https://www.nuget.org/packages/{id}/{version}
```

如果客户端实现需要显示4.3.0 的包详细信息的链接，它将生成以下 URL，并将其提供给用户：

```http
https://www.nuget.org/packages/NuGet.Versioning/4.3.0
```
