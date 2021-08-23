---
title: NuGet 5.11 发行说明
description: NuGet 5.11 的发行说明，包括新功能、bug 修复和 dcr。
author: erdembayar
ms.author: eryondon
ms.date: 8/10/2021
ms.topic: conceptual
ms.openlocfilehash: 97b59be0fa3da2bfb788e540fef795522d938ed4
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2021
ms.locfileid: "122728418"
---
# <a name="nuget-511-release-notes"></a>NuGet 5.11 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.11.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.11 版](https://visualstudio.microsoft.com/downloads/) | [5.0.400](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup>随 .net Core 工作负载一起安装了 Visual Studio 2019
  
> [!NOTE]
> Visual Studio 16.11、MSBuild 16.11 和 .net 5.0.400 + 需要 NuGet.exe 5.11 或更高版本。

## <a name="summary-whats-new-in-511"></a>摘要：5.11 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**漏洞**

* 工具-> 选项-> NuGet 程序包管理器字符串被截断- [#10779](https://github.com/NuGet/Home/issues/10779)

* 触发 PackagesMissingStatusChanged 事件时挂起- [#10854](https://github.com/NuGet/Home/issues/10854)

* NuGet 客户端忽略 NO_PROXY 设置- [#10902](https://github.com/NuGet/Home/issues/10902)

**[此版本中已修复的所有问题的列表-5.11](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTk5MDE)**

**[此版本中的提交列表-5.11](https://github.com/NuGet/NuGet.Client/compare/5.10.0.7240...5.11.0.17)**

## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本有任何问题，请查看[GitHub 问题](https://github.com/NuGet/Home/issues)并[Visual Studio 开发人员 Community](https://developercommunity.visualstudio.com/)了解现有问题。  NuGet 中的新问题，请报告[GitHub 问题](https://github.com/NuGet/Home/issues/new)。
如果遇到问题，请通过 "帮助" 中的 "报告问题" 选项（位于 "帮助" 下的 "[报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)" 选项来了解 NuGet **> 报告问题**。
