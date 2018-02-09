---
title: "NuGet 4.0 RC 发行说明 | Microsoft Docs"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/17/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 4.0 RC 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。"
keywords: "NuGet 4.0 RC 发行说明, bug 修复, 已知问题, 新增功能, DCR"
ms.reviewer:
- kraigb
ms.openlocfilehash: 9156f75edc9cf72cbb1d122f01d8a071ed56a124
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-40-rc-release-notes"></a>NuGet 4.0 RC 发行说明

[NuGet 3.5 RTM 发行说明](../release-notes/nuget-3.5-RTM.md)

[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) 重点增加了对 .NET Core 方案的支持，解决了主要客户反馈，并提高了各种方案的性能。 此版本引入了一些改进，如支持 PackageReference、作为 MSBuild 目标的 NuGet 命令、后台包还原等。

## <a name="bug-fixes"></a>Bug 修复

- `dotnet pack --version-suffix foo` 中的行为更改 - [#3838](https://github.com/NuGet/Home/issues/3838)

- VS“15”计算机上的 nuget.exe restore 总是失败 - [#3834](https://github.com/NuGet/Home/issues/3834)

- .NET Core“文件”>“新建项目”在还原过程中应阻止生成 - [#3780](https://github.com/NuGet/Home/issues/3780)

- 从 VS2015 迁移到 VS“15”的 ASP.NET Core Web 应用无法还原 - [#3773](https://github.com/NuGet/Home/issues/3773)

- [测试失败]“jQuery 验证”包无法通过 PM UI 卸载 - [#3755](https://github.com/NuGet/Home/issues/3755)

- 将包安装到 UWP `project.json` 时，还应还原父项目 - [#3731](https://github.com/NuGet/Home/issues/3731)

- 修改 NuGet 目标以将包源记录为高度详细而非普通 - [#3719](https://github.com/NuGet/Home/issues/3719)

- dotnet pack3 应默认包含 XML 文档 - [#3698](https://github.com/NuGet/Home/issues/3698)

- 当第一个为无包的源且选中全部源时，从 UI 的批量更新失败 - [#3696](https://github.com/NuGet/Home/issues/3696)

- Nuget pack 命令不包含所有文件 - [#3678](https://github.com/NuGet/Home/issues/3678)

- OOM 问题 - [#3661](https://github.com/NuGet/Home/issues/3661)

- 资产文件的 ProjectFileDependencyGroups 部分应使用项目的库名称 - [#3611](https://github.com/NuGet/Home/issues/3611)

- “dotnet restore”和递归目录 - [#3517](https://github.com/NuGet/Home/issues/3517)

- Restore3 失败记录为警告而非错误 - [#3503](https://github.com/NuGet/Home/issues/3503)

- TFS 问题：“在工作区中找不到[文件]，或者你无权访问”- [#2805](https://github.com/NuGet/Home/issues/2805)

- 在 VS 快速启动搜索框中键入“nuget <packagename>”，会保留“nuget ”前缀 - [#2719](https://github.com/NuGet/Home/issues/2719)

- System.Xml.XmlException：核心属性部分存在无法识别的根元素。 行：2，位置：2 - [#2718](https://github.com/NuGet/Home/issues/2718)

- 文本字段中具有转义 &lt; 或 &gt; 的 `.nuspec` 不再生成 - [#2651](https://github.com/NuGet/Home/issues/2651)

- nuget.exe delete 不会提示输入凭据（处于非交互模式）- [#2626](https://github.com/NuGet/Home/issues/2626)

- nuget.exe delete 警告本地源的 API 密钥（即使没有任何意义）- [#2625](https://github.com/NuGet/Home/issues/2625)

- 安装 EF -pre 包时出现错误，体验不佳 - [#2566](https://github.com/NuGet/Home/issues/2566)

- 在包管理器中更改选择后，Visual Studio 崩溃 - [#2551](https://github.com/NuGet/Home/issues/2551)

- 使用可变版本时，Dotnet restore 在简单列表本地存储库上执行区分大小写的 ID 查找 - [#2516](https://github.com/NuGet/Home/issues/2516)

- 对于 V2 源，nuget.exe delete 已被破坏 - [#2509](https://github.com/NuGet/Home/issues/2509)

- nuget.exe push timeout 需要更好的错误消息 - [#2503](https://github.com/NuGet/Home/issues/2503)

- 不包含正确导入的工具还原失败且没有任何提示 - [#2462](https://github.com/NuGet/Home/issues/2462)

- 即使从 nuget.org 进行安装，NuGet 也会在有专用源时提示输入凭据 - [#2346](https://github.com/NuGet/Home/issues/2346)

- ApplicationInsights 2.0 包已列出但尚不存在 - [#2317](https://github.com/NuGet/Home/issues/2317)

- VS“15”预览 5 分支中的 UI 延迟 - [#3500](https://github.com/NuGet/Home/issues/3500)

- 在针对 UWP 生成的过程中，首个 OnBuild 事件未还原 - [#3489](https://github.com/NuGet/Home/issues/3489)

- PowerShell5 中断 EntityFramework 安装 - [#3312](https://github.com/NuGet/Home/issues/3312)

- 将源添加到详细的日志记录（考虑为 3.5）- [#3294](https://github.com/NuGet/Home/issues/3294)

- NoCache 参数在 nuget 客户端版本 3.4+ 中无效 - [#3074](https://github.com/NuGet/Home/issues/3074)

- 当凭据提供程序在 VS 中加载失败时，请勿中断 NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)

## <a name="features"></a>功能

- 设置 CI 以运行 x86 - [#3868](https://github.com/NuGet/Home/issues/3868)

- 自动还原 3/3：非阻止 UI - [#3658](https://github.com/NuGet/Home/issues/3658)

- 自动还原 2/3：在指定的计算机上进行后台还原 - [#3657](https://github.com/NuGet/Home/issues/3657)

- 还原项目引用以匹配生成行为（递归）- [#3615](https://github.com/NuGet/Home/issues/3615)

- VS“15”中支持 DPL - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)

- 将设置文件移动到 Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)

- 生成的还原属性和目标需要跨目标参与支持 - [#3496](https://github.com/NuGet/Home/issues/3496)

- NuGet 还原支持 PackageTargetFallback（以前称为导入）- [#3494](https://github.com/NuGet/Home/issues/3494)

- ToolsRef 实现 - [#3472](https://github.com/NuGet/Home/issues/3472)

- RID 的 Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)

- 支持添加/删除/更新 PackageRefs 的 NuGet UI - [#3457](https://github.com/NuGet/Home/issues/3457)

- 自动还原 1/3：通过缓存项目还原信息实现指定 API - [#3456](https://github.com/NuGet/Home/issues/3456)

- [0] NuGet 还原任务和目标 - [#2994](https://github.com/NuGet/Home/issues/2994)

- [1] 在 MSBuild 中启用解决方案级别还原 - [#2993](https://github.com/NuGet/Home/issues/2993)

- 在 Visual Studio 中支持凭据提供程序公共扩展性 - [#2909](https://github.com/NuGet/Home/issues/2909)

- 递归 NuGet 还原 - [#2533](https://github.com/NuGet/Home/issues/2533)

- 无法在 dev15 上加载 Microsoft.TeamFoundation.Client，对于 VS“15”预览，需要将 Microsoft.TeamFoundation.Client 版本更新为 15.0 - [#2392](https://github.com/NuGet/Home/issues/2392)

- 无法在 VS“15”预览中将 C++ 包安装到 C++ UWP 项目 - [#2369](https://github.com/NuGet/Home/issues/2369)

- Nupkg 需要支持 \buildCrossTargeting\ 文件夹 - 并导入 `.targets` / `.props` 来跨越 MSBuild 范围目标 - [#3499](https://github.com/NuGet/Home/issues/3499)

- ToolsReference 设计 - [#3462](https://github.com/NuGet/Home/issues/3462)

- 修复 NuGet UI 以支持使用 `.csproj` 中的 PackageReferences 进行还原 - [#3455](https://github.com/NuGet/Home/issues/3455)

- 将清除缓存按钮添加到 VS 包管理器设置 - [#3289](https://github.com/NuGet/Home/issues/3289)

## <a name="dcrs"></a>DCR

- 发生自动还原时，应阻止解决方案还原 - [#3797](https://github.com/NuGet/Home/issues/3797)

- 从 NuGet 包管理器 UI 进行的 NetCore 安装将安装到每个 TFM，而不是该包支持的那个 TFM - [#3721](https://github.com/NuGet/Home/issues/3721)

- 还原指定 API 还需要支持 DotNetCliToolsReferences - [#3702](https://github.com/NuGet/Home/issues/3702)

- 将我们的 VS“15”vsix 标记为 systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)

- 从引用 MS.VS.Services.Client 迁移到 MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)

- 应按还原在项目级别考虑 $(RestoreLegacyPackagesDirectory) - [#3618](https://github.com/NuGet/Home/issues/3618)

- 使用单个 TargetFramework 还原到项目不得调整属性 - [#3588](https://github.com/NuGet/Home/issues/3588)

- dotnet restore3 foo.csproj 应遵循 projectref 依赖项，同时还原那些依赖项， 如生成 - [#3577](https://github.com/NuGet/Home/issues/3577)

- “类型”：“平台”依赖项在锁定文件中表示为“类型”：“包”- [#2695](https://github.com/NuGet/Home/issues/2695)

- nuget.exe 详细模式应显示下载 URL - [#2629](https://github.com/NuGet/Home/issues/2629)

- 将 NuGet xplat 移动到 Microsoft.NetCore.App 和 netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)

- 推送 - 从命令行推送时，应该可以替代符号服务器 - [#2348](https://github.com/NuGet/Home/issues/2348)

- 合并用于查找全局包路径的代码 - [#2296](https://github.com/NuGet/Home/issues/2296)

- 需要一个比 suppressParent 更好的名称 - [#2196](https://github.com/NuGet/Home/issues/2196)

- 决定用于 MSBuild 项目的`project.json` 依赖项名称 - [#1914](https://github.com/NuGet/Home/issues/1914)

- 将 SemVer 2.0.0 支持添加到 NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)

- 允许具有 `.targets` 的传递依赖项 NuPkgs 在 MSBuild 中可用 - [#3342](https://github.com/NuGet/Home/issues/3342)

- 命令行中的 NuGet 还原明显慢于 VS - [#3330](https://github.com/NuGet/Home/issues/3330)

- 使包 ID 和版本比较不区分大小写 - [#2522](https://github.com/NuGet/Home/issues/2522)

- NoCache 选项不适用于基于 `packages.config` 的还原/安装 (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)

- FindPackageByIdResource 资源需要一个默认的缓存上下文和记录器 - [#1357](https://github.com/NuGet/Home/issues/1357)
