---
title: NuGet 5.8 发行说明
description: 5.8 NuGet的发行说明，包括新功能、bug 修复和 DCR。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: fca9d2d068aadec207bfbf12f3ea82af872825a5
ms.sourcegitcommit: adb261dd4b2a8cd75447f7b5ea6a9e5a1a54d61d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2021
ms.locfileid: "122209925"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |
| [**5.8.1**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.8.4](https://visualstudio.microsoft.com/downloads/) | |

<sup>1 随</sup>.NET Core Visual Studio 2019 一起安装
  
> [!NOTE]
> Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 NuGet.exe 5.8 或更高版本。


## <a name="summary-whats-new-in-58"></a>摘要：5.8 版中的新增功能
🎉 这是第一个提供针对 **面向 .NET 5.0** NuGet 包的完整创作和还原支持🎉

* 使用 mmap/CreateFileMapping 加快 nupkg 提取 - [#9807](https://github.com/NuGet/Home/issues/9807)

* 在"UI 包详细信息"窗格中程序包管理器包漏洞详细信息 - [#9850](https://github.com/NuGet/Home/issues/9850)

* 使用新NuGet验证已签名的包 [`dotnet nuget verify`](/dotnet/core/tools/dotnet-nuget-verify) - [#8051](https://github.com/NuGet/Home/issues/8051)

* [`dotnet add package`](/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支持 `--prerelease` 添加包的最新版本（包括预发行版本）的选项 - [#4699](https://github.com/NuGet/Home/issues/4699)

* 使用 命令在 CLI 中搜索 [`nuget.exe search`](../reference/cli-reference/cli-ref-search.md) 包 - [#9704](https://github.com/NuGet/Home/issues/9704)

* [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) command 支持 `--verbosity` 选项 - [#9600](https://github.com/NuGet/Home/issues/9600)

* 为 No-Op 中基于 packageReference 的 csproj 样式项目启用快速Visual Studio还原优化 - [#9565](https://github.com/NuGet/Home/issues/9565)

* 解决方案级别程序包管理器 UI 操作（如包安装和更新）的速度高达 10 倍 - [#6010](https://github.com/NuGet/Home/issues/6010)

* 其他NuGet性能改进Visual Studio [-](https://github.com/NuGet/Home/issues/9982)#9982、#9984、#10052、#9903 [](https://github.com/NuGet/Home/issues/9984) [](https://github.com/NuGet/Home/issues/10052) [](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**DCR：**

* .NET 5.0 TFM：框架优先规则 - [#9436](https://github.com/NuGet/Home/issues/9436)

* NuGet TargetFramework 时，不应推断点平台版本 - [#9842](https://github.com/NuGet/Home/issues/9842)

* 使用 TargetFrameworkMoniker & TargetPlatformMoniker 推断框架，而不是使用单个 TFI、TFV、TPI、TPV 属性 - [#9895](https://github.com/NuGet/Home/issues/9895)

* 更新 `GetReferenceNearestTargetFrameworkTask()` 以支持具有 net5.0-windows (等平台的目标框架 -) - [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0 Visual Studio API - [#9650](https://github.com/NuGet/Home/issues/9650)

* 程序包管理器UI：由于包降级等错误，不应阻止合并或更新 (包操作 - ) - [#9224](https://github.com/NuGet/Home/issues/9224)

* NuGet功能的项目应会亮起;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* 禁止No-Op中还原消息 - Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)

**错误：**

* 不应在后台线程上调用 OutputWindowTextWriter 构造函数 - [#9764](https://github.com/NuGet/Home/issues/9764)

* 还原 Big Endian CPU 上的已签名包 - [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger 不应在 MEF 构造函数中调用关系方法 - [#9591](https://github.com/NuGet/Home/issues/9591)

* 代码中的NuGet。CommandLine.Console `PrintJustified()` 方法 - [#9737](https://github.com/NuGet/Home/issues/9737)

* 程序包管理器由于绑定错误而垃圾回收包元数据时 UI 内存泄漏 - [#9757](https://github.com/NuGet/Home/issues/9757)

* [签名]在 UI 中安装格式为 packages.config 的已签名包时，错误列表中程序包管理器警告 - [#9798](https://github.com/NuGet/Home/issues/9798)

* NuGet。CommandLine.XPlat 不应具有公共 API - [#9821](https://github.com/NuGet/Home/issues/9821)

* 减少在解决方案加载时因阻止线程池线程而引发的资源 `BlockingCollection.Take()`  -  [争用](https://github.com/NuGet/Home/issues/9822)，同时#9822

* 在命令行还原中，对于多目标项目，NuGet应从内部生成中读取目标框架相关信息 - [#9869](https://github.com/NuGet/Home/issues/9869)

* 通过 TargetFrameworkInformation 项读取运行时标识符关系图 - [#9874](https://github.com/NuGet/Home/issues/9874)

* 静态图形还原与 CrossTargeting 属性相比Visual Studio和常规MSBuild还原 - [#9881](https://github.com/NuGet/Home/issues/9881)

* 在静态图形还原中，对于多目标项目，NuGet应从内部生成中读取目标框架相关信息。 - [#9870](https://github.com/NuGet/Home/issues/9870)

* 允许在 Visual Studio 中加载和还原 `net5.0-platform` 项目 - [#9863](https://github.com/NuGet/Home/issues/9863)

* 在 UI 中显示程序包管理器版本 - [#9826](https://github.com/NuGet/Home/issues/9826)

* 程序包管理器UI：解决方案资源管理器未显示所有NuGet依赖项 - [#9898](https://github.com/NuGet/Home/issues/9898)

* 更新 SPDX 许可证列表 - [#9946](https://github.com/NuGet/Home/issues/9946)

* 打开"管理包"后，VS 2019 NuGet崩溃：图标导致图像 conversio 中出现未经处理异常 - [#9696](https://github.com/NuGet/Home/issues/9696)

* NuGet。Packaging.Extraction 需要 ilmerge 来排除 Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)

* 没有错误时，使用 ContinuePackingAfterGeneratingNuspec=false 打包[不应失败](https://github.com/NuGet/Home/issues/9786)- #9786

* 程序包管理器UI：图标未正确反转颜色 - [#10017](https://github.com/NuGet/Home/issues/10017)

* 还原 - 还原时，最新项目和No-Op项目 [的项目计数#10026](https://github.com/NuGet/Home/issues/10026)

* 在 `/p:RestoreUseStaticGraphEvaluation=true` 值中使用结果不能为 null - [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` 错误地将别名用于 WPF 库项目 - [#10020](https://github.com/NuGet/Home/issues/10020)

* 程序包管理器UI：签名验证失败时 NullReferenceException - [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces：请勿将 `object` 类型用于项目元数据值 - [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces：在工具选项中保存包源将覆盖凭据 - [#9711](https://github.com/NuGet/Home/issues/9711)


**[此版本中已修复的所有问题的列表 - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[此版本中的问题列表 - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>社区参与

感谢所有参与者，他们帮助使此版本NuGet出色！

|谁|拉/拉|问题|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | 错误消息中的拼写错误。 "管理员"而不是"管理员 ["- #9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | NuGet包含无效 AssemblyInformationalVersion 报表的包"需要说明["- #5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` 不考虑 Branch 和 Commit 属性 - [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | 单击"错误Visual Studio窗口中的 NU 代码应转到#9934 [https://docs.microsoft.com/nuget/reference/errors-and-warnings/](/nuget/reference/errors-and-warnings/)  -  [](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | 通过 https:// 选项添加新包源时，请使用"Visual Studio " - [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio` Mono 上的性能问题 - [#9989](https://github.com/NuGet/Home/issues/9989)
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | 为 SemanticVersion 类添加 TypeConverter - [#9125](https://github.com/NuGet/Home/issues/9125)

## <a name="summary-whats-new-in-581"></a>摘要：5.8.1 中的新增功能

* packages.config package.lock.js5.8 - #10257 [](https://github.com/NuGet/Home/issues/10257)

* 5.8 + 16.8 混合 PackageReference 和 packages.config 时无法解析可传递的项目依赖项 - [#10326](https://github.com/NuGet/Home/issues/10326)

**[此版本中已修复的所有问题的列表 - 5.8.1](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5ff7aeae16150e3b19910391)**

**[此版本中的提交列表 - 5.8.1](https://github.com/NuGet/NuGet.Client/compare/5.8.0.6930...5.8.1.7021)**

## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本存在任何问题，请查看我们的GitHub[问题](https://github.com/NuGet/Home/issues)Visual Studio[开发人员](https://developercommunity.visualstudio.com/)Community了解现有问题。  对于问题中的NuGet，请报告GitHub[问题](https://github.com/NuGet/Home/issues/new)。
对于NuGet问题，请通过"帮助和报告问题"下的"[](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)报告问题"选项> **IDE 中发现的问题**。