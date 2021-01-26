---
title: 报表滥用 URL 模板，NuGet API
description: "\"报表滥用 URL\" 模板允许客户端在其用户界面中显示 \"报告滥用\" 链接。"
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775225"
---
# <a name="report-abuse-url-template"></a>报告滥用 URL 模板

客户端可能会生成一个 URL，用户可以使用该 URL 报告有关特定包的滥用。 当包源要启用所有客户端体验 (甚至第三方) 将滥用报表委托给包源时，此方法非常有用。

用于生成此 URL 的资源是 `ReportAbuseUriTemplate` 在 [服务索引](service-index.md)中找到的资源。

## <a name="versioning"></a>版本控制

使用以下 `@type` 值：

@type 值                       | 说明
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 初始版本
ReportAbuseUriTemplate/3.0.0-rc   | 别名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是 `@id` 与上述某个资源值关联的属性的值 `@type` 。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不打算代表用户向报表滥用 URL 发出请求，但网页应支持方法，以便 `GET` 在 web 浏览器中轻松地打开已单击的 url。

## <a name="construct-the-url"></a>构造 URL

给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应显示此构造的 URL (或可单击的链接，) 用户允许用户在 URL 中打开 web 浏览器，并进行任何必要的滥用报告。 滥用报表窗体的实现由服务器实现确定。

的值 `@id` 是包含以下任何占位符标记的 URL 字符串：

### <a name="url-placeholders"></a>URL 占位符

名称        | 类型    | 必须 | 注释
----------- | ------- | -------- | -----
`{id}`      | string  | 否       | 要为其报告滥用行为的包 ID
`{version}` | string  | 否       | 要为其报告滥用行为的包版本

`{id}` `{version}` 服务器实现解释的和值必须区分大小写，而不区分版本是否规范化。

例如，nuget.exe 的报表滥用模板如下所示：

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

如果客户端实现需要显示4.3.0 的报表滥用窗体的链接，它将生成以下 URL，并将其提供给用户：

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
