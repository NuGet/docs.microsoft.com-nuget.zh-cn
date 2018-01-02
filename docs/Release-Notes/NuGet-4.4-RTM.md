---
title: "NuGet 4.4 RTM 发行说明 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: unniravindranathan
ms.date: 08/14/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5ffca6f6-a126-4407-b22f-1323e7dc44a3
description: "NuGet 4.3 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。"
keywords: "NuGet 4.3 RTM 发行说明, bug 修复, 已知问题, 新增功能, DCR"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 479f14db0b402476eccab23283a029a839cf51dd
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/14/2017
---
# <a name="44-rtm-release-notes"></a>4.4 RTM 发行说明

[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 NuGet 4.4 RTM。

## <a name="known-issues"></a>已知问题

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a>使用 .NET Framework 和 NuGet 的 .NET Standard 2.0 的问题 
.NET Standard 及其工具旨在使面向 .NET Framework 4.6.1 的项目可使用面向 .NET Standard 2.0 或更早版本的 NuGet 包和项目。 [本文档](https://github.com/dotnet/standard/issues/481)总结了该方案相关问题、解决问题的计划以及可使用当前工具状态部署的变通方法。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>使用包管理器控制台时，“Enter”键可能不起作用

#### <a name="issue"></a>问题：
有时无法在包管理器控制台中使用 Enter 键。 如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>解决方法：
打开该解决方案之前，重启 Visual Studio 并打开 PMC。 或者，请尝试删除 `project.lock.json`，然后再次还原。

### <a name="you-will-be-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>无法使用 Nuget 包管理器查看、添加或更新 DotNetCLITools

#### <a name="issue"></a>问题：
NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>解决方法：
必须在项目文件中手动编辑 DotNetCLIToolReferences。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>对目标框架版本重定目标可能会导致 Intellisense 不完整

#### <a name="issue"></a>问题：
在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。 将 PackageReferences 用作包管理器格式时可能出现这种情况。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>解决方法：
手动进行还原。


### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a>.NET Core 项目中的某个包内附具有无效签名的程序集，该包可触发还原操作无限循环

#### <a name="issue"></a>问题：
有时，如果所用包内附具有无效签名的程序集或者包版本设置有“DateTime”贴标，这会导致包自动还原操作无限循环 (dotnet/project-system#1457)。

#### <a name="workaround"></a>解决方法：
目前没有解决方法。


## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a>NuGet 4.4 RTM 时间框架中已修复的问题

[NuGet 4.3 RTM 发行说明](../release-notes/nuget-4.3-RTM.md)- 列出了 NuGet 4.3 RTM 已修复的所有问题

**功能：**

* 支持 PMC 和 NuGet PM UI 方案中的轻量型解决方案加载 - [#5180](https://github.com/NuGet/Home/issues/5180)

* msbuild 包目标应具有公共挂钩，以用于在其本身之前运行用户目标 - [#5143](https://github.com/NuGet/Home/issues/5143)

* 功能：将 dependencyVersion 开关添加到 nuget 安装 - [#1806](https://github.com/NuGet/Home/issues/1806)

* uap10.0.TODO.0 应映射到适用于 NuGet 的 .NET Standard 2.0 - [#5684](https://github.com/NuGet/Home/issues/5684)

* 支持使用 msbuild/t:restore 的 Visual Studio 生成工具 SKU - [#5562](https://github.com/NuGet/Home/issues/5562)

* 还原期间，如果需要适用于 .NET Standard 2.0 的 .NET 4.6.1 支持但尚未安装，则会出现错误 - [#5325](https://github.com/NuGet/Home/issues/5325)

* 包 ID 前缀保留客户端 UI - [#5572](https://github.com/NuGet/Home/issues/5572)

* 提供本地化 nuget 组件以支持 dotnet.exe 本地化 - [#4336](https://github.com/NuGet/Home/issues/4336)

**Bug：**

* 项目路径大小写不同可能导致还原丢失 PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)

* 将带警告编号的错误代码移动到错误范围 - [#5824](https://github.com/NuGet/Home/issues/5824)

* 未知 .NET Standard 版本与目标框架兼容时，出现误导性错误 - [#5818](https://github.com/NuGet/Home/issues/5818)

* 测试文件的许可证混乱 - [#5776](https://github.com/NuGet/Home/issues/5776)

* EndToEnd 测试模板中缺少许可证标头 - [#5774](https://github.com/NuGet/Home/issues/5774)

* packages.config restore 显示错误为 NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)

* nuget.exe install 应在 mono 上具有 DisableParallelProcessing - [#5741](https://github.com/NuGet/Home/issues/5741)

* nuget.exe install 不正确地禁用缓存 - [#5737](https://github.com/NuGet/Home/issues/5737)

* 禁用 Restore 时，运行 packages.config 的还原命令的 VS 会显示不正确消息 - [#5718](https://github.com/NuGet/Home/issues/5718)

* VS；禁用 Restore 时，运行还原命令显示令人混乱的消息 - [#5659](https://github.com/NuGet/Home/issues/5659)

* 缺少版本元数据时，GetRestoreDotnetCliToolsTask 失败 - [#5716](https://github.com/NuGet/Home/issues/5716)

* dotnet 添加包可从 csproj 清除空行 - [#5697](https://github.com/NuGet/Home/issues/5697)

* NuGet.Config 中凭据设置的源名称要区分大小写 - [#5695](https://github.com/NuGet/Home/issues/5695)

* 启用 GeneratePackageOnBuild 删除了包的整个历史记录 - [#5676](https://github.com/NuGet/Home/issues/5676)

* Restore 不会还原 mono.cecil 或 semver 包，但所有其他包都会还原。 - [#5649](https://github.com/NuGet/Home/issues/5649)

* 错误和警告 - 源不可用时发生严重错误。  - [#5644](https://github.com/NuGet/Home/issues/5644)

* [DesignConsistency] NuGet 安装状态文本目前在深色主题方面看起来不正确。 - [#5642](https://github.com/NuGet/Home/issues/5642)

* 解决方案中的更新包会对所有项目进行更新/安装 - [#5508](https://github.com/NuGet/Home/issues/5508)

* 根据 TargetFramework 与 TargetFrameworks，dotnet pack 的行为有所不同 - [#5281](https://github.com/NuGet/Home/issues/5281)

* “工具”文件夹中包含的 DLL 引发警告 - [#5020](https://github.com/NuGet/Home/issues/5020)

* NuGet.ContentModel 将过多内存用于字符串操作 -[#4714](https://github.com/NuGet/Home/issues/4714)

* 对于 OSX，RuntimeEnvironmentHelper.IsLinux 返回 true - [#4648](https://github.com/NuGet/Home/issues/4648)

* “dotnet 包”将 nuspec 置于 obj 下，而不是 obj\Debug 下 - [#4644](https://github.com/NuGet/Home/issues/4644)

* Nuget 极其缓慢的包升级 - [#4534](https://github.com/NuGet/Home/issues/4534)

* CPS 与尚未开启 LSL（轻量型解决方案还原）的较大型解决方案中的 Restore 不同步 - [#4307](https://github.com/NuGet/Home/issues/4307)

* SemVer 2.0 - 具有提供版本的 nuget pack 忽略元数据 (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)

* 带版本号和 ExcludeVersion 标志的 Nuget.exe (3.+) 安装包不能将包更新到较新版本 - [#2405](https://github.com/NuGet/Home/issues/2405)

* 顶级包违反约束时，Project.json restore 应发出警告 - [#2358](https://github.com/NuGet/Home/issues/2358)

* -ConfigFile 不在安装命令上设置自定义配置 - [#1646](https://github.com/NuGet/Home/issues/1646)

* nuget.exe install 不遵循“-DisableParallelProcessing”开关 - [#1556](https://github.com/NuGet/Home/issues/1556)

* DotNet.exe 或 msbuild.exe 仍在使用已禁用的源 - [#5704](https://github.com/NuGet/Home/issues/5704)

* 修复在 LSL 方案中挂起 - [#5685](https://github.com/NuGet/Home/issues/5685)

**DCR：**

* nuget.exe install TargetFramework 支持 - [#5736](https://github.com/NuGet/Home/issues/5736)

* 添加不同的 msbuild 任务 UserAgent 字符串（netcore 与桌面 msbuild）- [#5709](https://github.com/NuGet/Home/issues/5709)

* PackagePathResolver.GetPackageDirectoryName 应为虚拟 - [#5700](https://github.com/NuGet/Home/issues/5700)

* [DesignConsistency] 添加 NuGet 包时，消息混乱 - [#5641](https://github.com/NuGet/Home/issues/5641)

* [警告和错误] NoWarn 不通过 P2P 引用间接流动 - [#5501](https://github.com/NuGet/Home/issues/5501)

* 轻量型解决方案加载：PM UI、PMC 和 IV 的共同核心* - [#5057](https://github.com/NuGet/Home/issues/5057)

* 轻量型解决方案加载：支持 - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)

* 添加对 Visual Studio 触发的还原前 MSBuild 目标的支持 - [#4781](https://github.com/NuGet/Home/issues/4781)

* 将公共目标添加到可使用 BeforeTargets 引用的 NuGet.targets - [#4634](https://github.com/NuGet/Home/issues/4634)

* 包目标不能正确使用生成操作创建 contentFile - [#4166](https://github.com/NuGet/Home/issues/4166)

* RestoreOperationLogger.Do 会阻止线程池线程 - [#5663](https://github.com/NuGet/Home/issues/5663)

**Docs：**

* 用于安装命令 DependencyVersion 和 Framework 标志的文档 - [#5858](https://github.com/NuGet/Home/issues/5858)

* 文档中有关 NuGet 警告和错误的更新 - [#5857](https://github.com/NuGet/Home/issues/5857)

## <a name="link-to-github-issues-fixed-in-44-rtm"></a>4.4 RTM 中已修复 GitHub 问题的链接

[问题列表 1](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[问题列表 2](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[问题列表 3](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
