---
title: 报告滥用 URL 模板，NuGet API
description: 报告滥用 URL 模板允许客户端在其 UI 中显示的报告滥用行为链接。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020435"
---
# <a name="report-abuse-url-template"></a>报告滥用 URL 模板

就可以生成可由用户报告滥用行为有关特定包的 URL 的客户端。 当包源想要启用所有客户端体验 （甚至是第三方） 委派对包源的滥用报告时，这很有用。

用于生成此 URL 使用的资源是`ReportAbuseUriTemplate`资源中找到[服务索引](service-index.md)。

## <a name="versioning"></a>版本管理

以下`@type`使用值：

@type 值                       | 说明
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 初始版本
ReportAbuseUriTemplate/3.0.0-rc   | 别名 `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL 模板

以下 API 的 URL 是的值`@id`属性与前面提到的资源之一相关联`@type`值。

## <a name="http-methods"></a>HTTP 方法

尽管客户端不应代表用户向报告滥用 URL 发出请求，但应支持 web 页`GET`方法，以允许单击的 URL 来轻松地在 web 浏览器中打开。

## <a name="construct-the-url"></a>构造的 URL

提供了已知的包 ID 和版本，客户端实现可以构造用于访问 web 界面的 URL。 客户端实现应显示给用户允许应用来打开 web 浏览器到 URL 并进行任何必要的滥用报告此构造的 URL （或可单击的链接）。 滥用报告表单的实现取决于服务器实现。

值`@id`是 URL 的字符串包含任何以下占位符标记：

### <a name="url-placeholders"></a>URL 占位符

name        | 类型    | 必需 | 说明
----------- | ------- | -------- | -----
`{id}`      | 字符串  | 否       | 将包 ID 与举报违规帖子
`{version}` | 字符串  | 否       | 将包版本到举报违规帖子

`{id}`和`{version}`解释服务器实现的值必须是不区分大小写和不敏感到是否规范化版本。

例如，nuget.org 的报告滥用行为模板如下所示：

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

如果需要有关 NuGet.Versioning 4.3.0 报告滥用行为窗体显示的链接的客户端实现，它将产生以下 URL 并将其提供给用户：

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
