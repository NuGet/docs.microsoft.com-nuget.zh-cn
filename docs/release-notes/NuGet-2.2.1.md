---
title: NuGet 2.2.1 发行说明
description: NuGet 2.2.1 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550693"
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 发行说明

[NuGet 2.2 发行说明](../release-notes/nuget-2.2.md) | [NuGet 2.5 发行说明](../release-notes/nuget-2.5.md)

NuGet 2.2.1 已于 2013 年 2 月 15 日发布。  在 VS 扩展版本编号是 2.2.40116.9051。

## <a name="localization-refresh"></a>本地化刷新
当 NuGet 作为 Visual Studio 2012 的一部分提供时，它已完全本地化为英语 + 13 种其他语言。  从那时起，NuGet 2.1 和 2.2 已装运，但有未刷新本地化。  NuGet 2.2.1 版本刷新本地化。

NuGet 的 UI 和 PowerShell 控制台已本地化为以下语言版本：

1. 中文（简体）
1. 和 SharePoint 2010 显示的“中文(繁体)”
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
如果生成 Visual Studio 模板，则可以使用 NuGet[预安装包](../visual-studio-extensibility/visual-studio-templates.md)作为模板的一部分。  到目前为止，此功能有限制的所有包需要来自同一源。  使用 NuGet 2.2.1 不过，您可以从多个存储库 （在模板中，VSIX 或在注册表中定义的磁盘上的文件夹） 安装的包。

此功能的主要方案是自定义 ASP.NET 项目模板。  内置的 ASP.NET 模板使用预安装的包，提取程序包从本地磁盘。  现在，您可以创建使用 ASP.NET 所安装的现有包的自定义 ASP.NET 项目模板，但将额外的 NuGet 包添加到你的模板。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2.1 包含几个目标的 bug 修补程序。 有关工作的列表项中已修复 NuGet 2.2.1，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。


## <a name="known-issues"></a>已知问题

当扩展 ASP.NET 项目模板，所有预安装的包存储库必须使用相同的值为`isPreunzipped`属性。
