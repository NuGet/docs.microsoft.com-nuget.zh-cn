---
title: NuGet 2.8.2 发行说明
description: 发行说明，了解 NuGet 2.8.2 包括已知问题、 bug 修复、 增加的功能，以及 DCRs。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: a004c250d60a4ed1ca8dede1e83b2a68e10299bf
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821325"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 发行说明

[NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 已于 2014 年 5 月 22，发布。  此版本，仅包含对命令行 nuget.exe、 NuGet.Server 包和其他 NuGet 包的更改。  版本不包括使用更新的 Visual Studio 扩展或 WebMatrix 扩展。

## <a name="notable-updates"></a>值得注意的更新

最值得注意的更新中命令行 nuget.exe 和 NuGet.Server 包 （对于自承载 NuGet 源）。

### <a name="important-nugetexe-bug-fixes"></a>重要 nuget.exe Bug 修复

1. [nuget.exe 推送失败，并保留重试](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不会正确发送基本身份验证凭据](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送不会按照临时重定向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要 NuGet.Server Bug 修复

1. [IsAbsoluteLatestVersion NuGet.Server 返回的值不正确](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新的包

Nuget.exe 命令行和 NuGet.Server 修补程序都附带作为 NuGet 程序包更新。  没有更新 2.8.2 以及其他包。

以下是更新后的包的列表：

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （包，不要使用扩展名）

## <a name="all-changes"></a>所有更改
出现了 10 在版本中解决的问题。 有关工作的完整列表项固定在 NuGet 2.8.2，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
