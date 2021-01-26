---
title: NuGet 2.8.2 发行说明
description: NuGet 2.8.2 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d39f2dc9a429ed264461174325c2080468fa8aae
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780371"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 发行说明

[NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md)  | [NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 于2014年5月22日发布。  此版本仅包括对 nuget.exe 命令行、NuGet 包和其他 NuGet 包的更改。  版本未包括更新的 Visual Studio 扩展或 WebMatrix 扩展。

## <a name="notable-updates"></a>重要更新

最值得注意的更新在 nuget.exe 命令行和 NuGet. 服务器包 (中，用于自承载的 NuGet 源) 。

### <a name="important-nugetexe-bug-fixes"></a>重要 nuget.exe Bug 修复

1. [nuget.exe 推送失败并继续重试](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不会正确发送基本身份验证凭据](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送不会跟随暂时重定向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要说明 NuGet。服务器错误修复

1. [NuGet 返回的 IsAbsoluteLatestVersion 值错误。](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>已更新包

nuget.exe 的命令行和 NuGet。服务器修补程序作为 NuGet 包更新提供。  还更新了2.8.2 的其他包。

下面是已更新包的列表：

1. [Nuget.exe](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet 命令行](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet。生成](https://www.nuget.org/packages/NuGet.Build/)
1. [VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) (包，而不是扩展) 

## <a name="all-changes"></a>所有更改
此版本中解决了10个问题。 有关 NuGet 2.8.2 中修复的工作项的完整列表，请查看 [此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
