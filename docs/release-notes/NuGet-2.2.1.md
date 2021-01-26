---
title: NuGet 2.2.1 发行说明
description: NuGet 2.2.1 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776811"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 发行说明

[NuGet 2.2 发行说明](../release-notes/nuget-2.2.md)  | [NuGet 2.5 发行说明](../release-notes/nuget-2.5.md)

NuGet 2.2.1 于2013年2月15日发布。  VS 扩展版本号为2.2.40116.9051。

## <a name="localization-refresh"></a>本地化刷新
当 NuGet 作为 Visual Studio 2012 的一部分提供时，它已完全本地化为英语 + 13 其他语言。  自那时起，已发布 NuGet 2.1 和2.2，但尚未刷新本地化。  NuGet 2.2.1 版本会刷新我们的本地化。

NuGet 的 UI 和 PowerShell 控制台已本地化为以下语言：

1. 中文(简体)
1. 中文(繁体)
1. 捷克语
1. 英语
1. 法语
1. 德语
1. 意大利语
1. 日语
1. 朝鲜语
1. 波兰语
1. 葡萄牙语(巴西)
1. 俄语
1. 西班牙语
1. 土耳其语

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio 模板支持多个预安装的包存储库
如果生成 Visual Studio 模板，则可以使用 NuGet 来 [预安装包](../visual-studio-extensibility/visual-studio-templates.md) 作为模板的一部分。  到现在为止，此功能有一个限制，即所有包都需要来自同一源。  不过，对于 NuGet 2.2.1，可以从模板、VSIX 或在注册表) 中定义的磁盘上的文件夹中 (的多个存储库安装包。

此功能的主要方案是自定义 ASP.NET 项目模板。  内置的 ASP.NET 模板使用预安装的包，从本地磁盘提取包。  你现在可以创建自定义的 ASP.NET 项目模板，该模板使用 ASP.NET 安装的现有包，但将额外的 NuGet 包添加到模板中。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2.1 包含一些有针对性的 bug 修复程序。 有关 NuGet 2.2.1 中修复的工作项列表，请查看 [此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。


## <a name="known-issues"></a>已知问题

如果要扩展 ASP.NET 项目模板，所有预安装的包存储库都必须为该属性使用相同的值 `isPreunzipped` 。
