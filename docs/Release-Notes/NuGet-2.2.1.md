---
title: "NuGet 2.2.1 发行说明 |Microsoft 文档"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "发行说明，了解 NuGet 2.2.1 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。"
keywords: "NuGet 2.2.1 发行说明，bug 修复的已知问题，添加了一些功能，DCRs"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-221-release-notes"></a>NuGet 2.2.1 发行说明

[NuGet 2.2 发行说明](../release-notes/nuget-2.2.md) | [NuGet 2.5 发行说明](../release-notes/nuget-2.5.md)

NuGet 2.2.1 已于 2013 年 2 月 15 日发布。  在 VS 扩展版本号是 2.2.40116.9051。

## <a name="localization-refresh"></a>本地化刷新
当 NuGet 附带的 Visual Studio 2012 时，它已完全本地化为英语 + 13 其他语言。  此后，发运 NuGet 2.1 和 2.2 但具有未刷新本地化。  NuGet 2.2.1 版本刷新我们本地化。

NuGet 的 UI 和 PowerShell 控制台被本地化为以下语言：

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
如果生成 Visual Studio 模板，你可以使用 NuGet 到[预安装包](../visual-studio-extensibility/visual-studio-templates.md)作为模板的一部分。  到目前为止，此功能将有一个限制的所有包所需的来自同一源。  使用 NuGet 2.2.1 不过，你可以从多个存储库 （模板、 VSIX 或注册表中定义的磁盘上的文件夹） 中安装的包。

此功能的主要方案是自定义 ASP.NET 项目模板。  内置的 ASP.NET 模板使用预安装的程序包，提取包从本地磁盘。  现在，你可以创建使用 asp.net 安装的现有包的自定义 ASP.NET 项目模板，但将额外的 NuGet 包添加到你的模板。

## <a name="bug-fixes"></a>Bug 修复
NuGet 2.2.1 包括几个目标的 bug 修复。 有关工作的列表项固定在 NuGet 2.2.1，请查看[对于此版本的 NuGet 问题跟踪程序](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)。


## <a name="known-issues"></a>已知问题

所有预安装的包存储库扩展 ASP.NET 项目模板时，如果必须使用相同的值`isPreunzipped`属性。
