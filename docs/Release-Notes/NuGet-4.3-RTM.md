---
title: NuGet 4.3 RTM 发行说明 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.3 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
keywords: NuGet 4.3 RTM 发行说明, bug 修复, 已知问题, 新增功能, DCR
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 3c798bde11548b866cad62697315e907dea91aa5
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-43-rtm-release-notes"></a>NuGet 4.3 RTM 发行说明

[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 NuGet 4.3 RTM，NuGet 4.3 RTM 添加了对新方案（例如 .NET Standard 2.0/.NET Core 2.0）的支持、包含多种质量修复和提升性体能。 此版本还提供多方面的提升，例如对语义化版本控制 2.0.0 的支持、NuGet 警告和错误的 MSBuild 集成等等。

## <a name="known-issues"></a>已知问题

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a>在某些情况下，NuGet 还原操作可能会将禁用的包源视作已启用进行处理

#### <a name="issue"></a>问题

以下还原命令行方法将被禁用的包源视为已启用。 [NuGet#5704](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- `dotnet restore`（不管是使用 VS 随附的 dotnet.exe，还是使用 NetCore SDK 2.0.0 随附的文件）

#### <a name="workaround"></a>解决方法

1. 使用 Visual Studio（2017 15.3 或更高版本）或 NuGet.exe（v4.3.0 或更高版本）
1. 删除禁用的源，并继续使用 msbuild 或 dotnet.exe。
1. 对于解决方案，可以在 NuGet.config 中使用“Clear”，再定义此解决方案所必需的源。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>使用包管理器控制台时，“Enter”键可能不起作用

#### <a name="issue"></a>问题

有时无法在包管理器控制台中使用 Enter 键。 如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>解决方法

打开该解决方案之前，重启 Visual Studio 并打开 PMC。 或者，请尝试删除 `project.lock.json`，然后再次还原。

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

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a>NuGet 4.3 RTM 时间框架中已修复的问题

[NuGet 4.0 RTM 发行说明](../release-notes/nuget-4.0-RTM.md) - 列出所有 NuGet 4.0 RTM 修复的问题

### <a name="features"></a>功能

- 提升 NuGet 还原性能 - 为命令行还原和 VS 实现更小的 NoOp - [#5080](https://github.com/NuGet/Home/issues/5080)

- NET Core 2.0: VS/Dotnet CLI 应开始使用现有的 NuGet 功能：FallBack 文件夹 - [#4939](https://github.com/NuGet/Home/issues/4939)

- NET Core 2.0：使得用户可以忽略特定还原警告（或提升为错误）- [#4898](https://github.com/NuGet/Home/issues/4898)

- NET Core 2.0：CLI 本地化程序集 - [#4896](https://github.com/NuGet/Home/issues/4896)

- NET Core 2.0：将所有警告/错误注册到资产文件（包括 PackageTargetFallback）- [#4895](https://github.com/NuGet/Home/issues/4895)

- 启用 TFM 支持：NetStandard2.0，Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)

- 减少 NuGet.Core 和 NuGet.Client 项目（和 DLL）的数量 - [#2446](https://github.com/NuGet/Home/issues/2446)

- 添加将 NuGet 警告标记为错误的功能 - [#2395](https://github.com/NuGet/Home/issues/2395)

### <a name="bugs"></a>Bug

- msbuild /t:pack 失败，“PackTask”任务不支持“DevelopmentDependency”参数 - [#5584](https://github.com/NuGet/Home/issues/5584)

- 如果未在 PackagePath 末尾添加 Windows 目录分隔符，则内容文件的目录结构会合并 - [#4795](https://github.com/NuGet/Home/issues/4795)

- netcore 项目不支持设置为 developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)

- 同步加载的 RestoreManagerPackage 锁定 UI 线程和死锁 VS - [#4679](https://github.com/NuGet/Home/issues/4679)

- dotnet Restore（和 msbuild /t:restore）跳过有显式解决方案项目依赖项的项目 [#4578](https://github.com/NuGet/Home/issues/4578)

- 如果解决方案有引用大小写不同的同一项目的 projectreference，则还原可能不起作用。 这还会影响大小写相同的不同相对路径 - [#4574](https://github.com/NuGet/Home/issues/4574)

- NuGet 包还原的可执行文件不能再使用 .NET Core 2.0 执行 - [#4424](https://github.com/NuGet/Home/issues/4424)

- NuGet.exe 在分析解决方案文件时吞并异常的详细信息 - [#4411](https://github.com/NuGet/Home/issues/4411)

- 如果 ContentTargetFolders 在 Windows 上包含以“/”结尾的路径，则包会将内容文件放在错误的位置 - [#4407](https://github.com/NuGet/Home/issues/4407)

- 不能还原面向 netcoreapp1.1 的工具包的 DotNetCliToolReference - [#4396](https://github.com/NuGet/Home/issues/4396)

- Nuget 更新 CLI 将旧包版本条件留在项目文件中 (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)

### <a name="dcrs"></a>DCR

- 从CPS nomation 读取 DotnetCliToolTargetFramework - [#5397](https://github.com/NuGet/Home/issues/5397)

- TPMinV check 应适用于 pj 样式 UWP - [#4763](https://github.com/NuGet/Home/issues/4763)

- 提升 AutoReferenced 包的 UI 说明 - [#4471](https://github.com/NuGet/Home/issues/4471)

- NuGet restore 从运行时部分选择编译资产。 - [#4207](https://github.com/NuGet/Home/issues/4207)

- 将依赖项诊断放在锁定文件中 - [#1599](https://github.com/NuGet/Home/issues/1599)

## <a name="links-to-github-issues-fixed-in-43-rtm"></a>4.3 RTM 中已修复 GitHub 问题的链接

[问题列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
