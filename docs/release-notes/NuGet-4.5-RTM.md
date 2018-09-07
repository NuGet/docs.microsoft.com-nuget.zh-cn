---
title: NuGet 4.5 RTM 发行说明
description: NuGet 4.5 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: anangaur
ms.author: anangaur
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 01ecd8c7de1a0f713766e3c413d889038522bac7
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548291"
---
# <a name="nuget-45-rtm-release-notes"></a>NuGet 4.5 RTM 发行说明

[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带有 [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe)。

## <a name="known-issues"></a>已知问题

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题 

.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。 [本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>无法使用 NuGet 包管理器查看、添加或更新 DotNetCLITools

#### <a name="issue"></a>问题

NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>解决方法

必须在项目文件中手动编辑 DotNetCLIToolReferences。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>对目标框架版本重定目标可能会导致 Intellisense 不完整

#### <a name="issue"></a>问题

在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。 将 PackageReferences 用作包管理器格式时可能出现这种情况。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>解决方法

手动进行还原。

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core 项目中的某个包内附具有无效签名的程序集，该包可触发还原操作无限循环

#### <a name="issue"></a>问题

有时，如果所用包内附具有无效签名的程序集或者包版本设置有“DateTime”贴标，这会导致包自动还原操作无限循环 [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457)。

#### <a name="workaround"></a>解决方法

目前没有解决方法。

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a>NuGet 4.5 RTM 时间框架中已修复的问题

有关 NuGet 4.4 RTM 中已修复问题的信息，请参阅[NuGet 4.4 RTM 发行说明](../release-notes/nuget-4.4-RTM.md) 

### <a name="features"></a>功能

- 禁用符号包的自动推送 - [#6113](https://github.com/NuGet/Home/issues/6113)

### <a name="bugs"></a>Bug

- [回归] 在 15.5p1 中，Portable0.0 被跳过 - [#6105](https://github.com/NuGet/Home/issues/6105)
- 还原后包中的资产丢失 - [#5995](https://github.com/NuGet/Home/issues/5995)
- 插件凭据提供程序不支持包含空格的 URI - [#5982](https://github.com/NuGet/Home/issues/5982)
- 如果包无法还原，应在输出中打印错误，即使最低详细级别为“ON”- [#5658](https://github.com/NuGet/Home/issues/5658)
- dotnet
  - 解决方案级别的 dotnetcore restore 不遵循 ProjectReference，且 ReferenceOutputAssembly 为 false，导致随机生成失败 - [#5490](https://github.com/NuGet/Home/issues/5490)
- PMC 中的自动完成无法与对象方法正确协作 -[#4800](https://github.com/NuGet/Home/issues/4800)
- 使用 Visual Studio 2015 工具集时 nuget.exe 还原失败 - [#4713](https://github.com/NuGet/Home/issues/4713)
- 在 vs2017 中实例化 perf - pmc 成本高昂 - [#4205](https://github.com/NuGet/Home/issues/4205)
- 慢速连接时获取依赖项信息速度缓慢 - [#4089](https://github.com/NuGet/Home/issues/4089)
- 如果多个包共享通用的依赖项，带 -RemoveDependencies 的 uninstall-package 将失败 - [#4026](https://github.com/NuGet/Home/issues/4026)
- 完成 NuGet.Core.nupkg 以便发布 - [#3581](https://github.com/NuGet/Home/issues/3581)
- 将 -IncludeProjectReferences 用于 csproj + project.json 时，NuGet 包会解析目录名称中的依赖项 ID - [#3566](https://github.com/NuGet/Home/issues/3566)
- “NuGet.ProxyCache”的类型初始值设定项引发异常 - [#3144](https://github.com/NuGet/Home/issues/3144)
- 使用 kudu 时的 nuget 还原性能问题 - [#3087](https://github.com/NuGet/Home/issues/3087)
- 搜索超出注册 blob 时，UI 客户端无法显示任何错误或警告 - [# 2149](https://github.com/NuGet/Home/issues/2149)
- Get-Packages -Updates 生成不正确的查询 - [# 2135](https://github.com/NuGet/Home/issues/2135)

## <a name="links-to-github-issues-fixed-in-45-rtm"></a>4.5 RTM 中已修复 GitHub 问题的链接

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
