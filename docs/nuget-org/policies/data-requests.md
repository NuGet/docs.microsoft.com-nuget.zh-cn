---
title: 用户数据请求
description: 请求用户数据导出和删除的策略
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775719"
---
# <a name="user-data-requests"></a>用户数据请求

nuget.org 用户可通过 [nuget.org](https://www.nuget.org) 提交信息删除请求和信息导出请求。这两种类型均以支持请求的形式提交，并由 nuget.org 管理员在 30 天内执行。

可通过 nuget.org 直接访问以下用户数据：

* 与电子邮件地址、登录帐户、个人资料图片、电子邮件通知设置等数据相关的帐户
* 拥有的 API 密钥
* 拥有包列表

此数据不包含在通过支持请求导出的数据中。

## <a name="identifying-customer-data"></a>标识客户数据

可以将客户数据标识为 nuget.org 用户帐户名。

## <a name="deleting-customer-data"></a>删除客户数据

请求从 nuget.org 删除用户数据：

1. 用户必须登录到 [nuget.org](https://www.nuget.org)
1. 用户必须通过 [nuget.org/account/delete](https://www.nuget.org/account/delete) 提交请求，才能删除帐户

若用户为包的唯一所有者，建议其在请求删除帐户前找到新的所有者。 如果不转移包所有权，则不会列出 NuGet 包，因此，它不会再显示在 Visual Studio 的搜索查询中或 nuget.org 网站上。 删除帐户前，nuget.org 管理员需与用户协作，为其所拥有的包寻找新的所有者。

nuget.org 管理员将在请求提交后 30 天内完成帐户删除操作。

帐户删除后，所有用户数据都将从 nuget.org 系统中删除，并会执行以下操作：

* 从 nuget.org 中注销已删除的帐户
* 删除所有拥有的 API 密钥
* 释放所有保留命名空间
* 删除所有包所有权

不会删除拥有包  。 虽然搜索结果中未列出这些包，但依赖于它们的项目仍可通过包还原进行使用。

## <a name="exporting-customer-data"></a>导出客户数据

登录到 nuget.org 后，用户可通过 [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) 提交导出请求

用户可以通过 Azure Blob 在 48 小时内下载导出的数据。 48 小时后，访问过期，用户必须根据需要提交新的导出请求。

导出的数据包括：

* 用户的支持请求
* 审核日志中保存的用户操作（发布包、创建帐户）
* IIS 日志中保存的任何用户信息
