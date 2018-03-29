---
title: 报告滥用行为 URL 模板，NuGet API |Microsoft 文档
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
ms.technology: ''
description: 报告滥用行为 URL 模板允许客户端在其用户界面中显示的报告滥用行为链接。
keywords: NuGet API 报告滥用行为、 NuGet API 文件合规、 nuget.org 报表 URL 模板
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: ded861e3eaf73e45b8d4bd80b96d54bfeb38e9d6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="report-abuse-url-template"></a>报告滥用行为 URL 模板

它是客户端来生成可由用户有关特定包报告滥用行为的 URL。 当包源想要启用所有客户端的体验，（甚至是第三方） 以委托到包源的滥用行为报表，这非常有用。

用于提取包内容的资源是`ReportAbuseUriTemplate`资源位于[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`将使用值：

@type 值                       | 说明
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 初始版本
ReportAbuseUriTemplate/3.0.0-rc   | 别名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是值`@id`与前面提到的资源之一相关联的属性`@type`值。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不打算代表用户对报表滥用行为 URL 发出请求，但应支持网页`GET`方法，以便允许一个被单击的 URL，以轻松地在 web 浏览器中打开。

## <a name="construct-the-url"></a>构造 URL

给定已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应给此用户，从而允许它们以打开 web 浏览器的 url 并进行任何必要的滥用行为报表显示此构造的 URL （或可单击的链接）。 由服务器实现确定滥用行为报表窗体的实现。

值`@id`是一个包含任何以下占位符令牌的 URL 字符串：

### <a name="url-placeholders"></a>URL 占位符

名称        | 类型    | 必需 | 说明
----------- | ------- | -------- | -----
`{id}`      | 字符串  | 否       | 将包 ID 与报表有关的滥用行为
`{version}` | 字符串  | 否       | 包版本到有关报告滥用行为

`{id}`和`{version}`由服务器实施解释的值必须是区分大小写和对版本进行了规范化是否不敏感。

例如，nuget.org 的报告滥用行为模板类似如下所示：

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

如果客户端实现需要为 NuGet.Versioning 4.3.0 到报告滥用行为窗体中显示一个链接，它将产生以下 URL 并将其提供给用户：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
