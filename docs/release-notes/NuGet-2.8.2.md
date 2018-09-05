---
title: NuGet 2.8.2 发行说明
description: NuGet 2.8.2 包括的发行说明的已知问题、 bug 修复、 新增的功能和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ed22aef6766bbe8e4b688e0587304a18eaeb8895
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551143"
---
# <a name="nuget-282-release-notes"></a>NuGet 2.8.2 发行说明

[NuGet 2.8.1 发行说明](../release-notes/nuget-2.8.1.md) | [NuGet 2.8.3 发行说明](../release-notes/nuget-2.8.3.md)

NuGet 2.8.2 已于 2014 年 5 月 22，发布。  此版本中，仅包含 nuget.exe 命令行，NuGet.Server 包与其他 NuGet 包的变化。  发布未包含的更新的 Visual Studio 扩展或 WebMatrix 扩展。

## <a name="notable-updates"></a>值得注意的更新

在 nuget.exe 命令行和 NuGet.Server 包 （适用于自承载的 NuGet 源） 中介绍了最值得注意的更新。

### <a name="important-nugetexe-bug-fixes"></a>重要的 nuget.exe Bug 修复

1. [nuget.exe 推送会失败，并保留重试](https://nuget.codeplex.com/workitem/4000)
1. [nuget.exe 推送不会正确发送基本身份验证凭据](https://nuget.codeplex.com/workitem/4109)
1. [nuget.exe 推送不遵循临时重定向](https://nuget.codeplex.com/workitem/4050)

### <a name="important-nugetserver-bug-fix"></a>重要 NuGet.Server 的 Bug 修复

1. [IsAbsoluteLatestVersion NuGet.Server 返回的值不正确](https://nuget.codeplex.com/workitem/4147)

## <a name="packages-updated"></a>更新包

Nuget.exe 命令行和 NuGet.Server 修补程序附带 NuGet 包更新。  没有使用 2.8.2 以及更新其他包。

下面是更新后的包的列表：

1. [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)
1. [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/)
1. [NuGet.Server](https://www.nuget.org/packages/NuGet.Server/)
1. [NuGet.Build](https://www.nuget.org/packages/NuGet.Build/)
1. [NuGet.VisualStudio](https://www.nuget.org/packages/NuGet.VisualStudio/) （包，不扩展）

## <a name="all-changes"></a>所有更改
出现了 10 个版本中解决的问题。 有关完整列表的工作项中已修复 NuGet 2.8.2，请查看[对于此版本的 NuGet 问题跟踪程序](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.2&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)。
