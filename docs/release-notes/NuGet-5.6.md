---
title: NuGet 5.6 发行说明
description: NuGet 5.6 的发行说明，包括新功能、bug 修复和 Dcr。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727805"
---
# <a name="nuget-56-release-notes"></a>NuGet 5.6 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.6.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.6](https://visualstudio.microsoft.com/downloads/) | [3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装

## <a name="summary-whats-new-in-56"></a>摘要：5.6 中的新增功能

* 支持浮动版本的预发布包。 `Version="*-*"`、 `Version="1.*-*"` 和类似浮动到最新版本，包括预发行版本（在指定范围内）- [#912](https://github.com/NuGet/Home/issues/912)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**漏洞**

* `nuget push *.nupkg`当 snupkg 不存在时失败- [#8148](https://github.com/NuGet/Home/issues/8148)

* Pack 和多个其他代码路径，依赖于区域设置。 使用 System.text.regularexpressions.regexoptions. Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)

* Perf：不应在预览还原中编写已卸载项目方案的 DG 规范- [#8793](https://github.com/NuGet/Home/issues/8793)

* 还原：通过缓存解决方案依赖项关系图规范提高性能[#9201](https://github.com/NuGet/Home/issues/9201)

* 使用 PM 控制台安装包后，PM UI 不适用于 SDK 样式项目- [#9203](https://github.com/NuGet/Home/issues/9203)

* 嵌入的图标无法在具有本地包源的 PM UI 中显示-具体取决于/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)

* 如果 NuGetVersion 无法[#9255](https://github.com/NuGet/Home/issues/9255)解析，则 TryParseStrict （）应返回 false

* `nuget.exe push`有关的帮助 `-source` ，应建议使用源名称，而不是源 URL- [#9265](https://github.com/NuGet/Home/issues/9265)

* `dotnet nuget add package SourceUri`创建错误的默认包源名称- [#9277](https://github.com/NuGet/Home/issues/9277)

* 屏幕阅读器未公布 "搜索 ..."切换选项卡时的消息- [#9307](https://github.com/NuGet/Home/issues/9307)

* 辅助功能：聚焦框的颜色不适用于深色主题中的 UI 选项卡- [#9336](https://github.com/NuGet/Home/issues/9336)

* 由于 MSBuild 14 或更低，无法还原 nuget.exe 5.5- [#9458](https://github.com/NuGet/Home/issues/9458)

* 请勿记录还原消息中的毫秒时间- [#8977](https://github.com/NuGet/Home/issues/8977)

* 使 IOutputConsole 异步[#9268](https://github.com/NuGet/Home/issues/9268)

* MSBuild 版本选取在某些非英语区域性上的运行效果很差- [#9322](https://github.com/NuGet/Home/issues/9322)

* #9337 上缺少格式默认值 `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)

* Perf： RestoreOperationLogger 具有不必要的线程关联性[#9288](https://github.com/NuGet/Home/issues/9288)

* 命令文档的自动创建 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)

* 默认详细级别不应报告每个项目的 noop 还原[#8792](https://github.com/NuGet/Home/issues/8792)

* `-DependencyVersion`的支持参数 `NuGet.exe update` ，类似于安装命令- [#7694](https://github.com/NuGet/Home/issues/7694)


**DCRs**

* 添加对 net 5.0 目标框架的初始支持- [#9584](https://github.com/NuGet/Home/issues/9584)

* 在 PM UI 的 "更新" 选项卡中按 ID 对包排序- [#9278](https://github.com/NuGet/Home/issues/9278)


**[此版本中已修复的所有问题的列表-5。6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**
