---
title: NuGet 5.8 发行说明
description: NuGet 5.8 的发行说明，包括新功能、bug 修复和 Dcr。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 09fb98eec79ee4ed08d85a1c557a420d6b265f11
ms.sourcegitcommit: f4b74b500e3db9e468f11142df48d87880382267
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2020
ms.locfileid: "94572826"
---
# <a name="nuget-58-release-notes"></a>NuGet 5.8 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.8**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.8](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装
  
> [!NOTE]
> Visual Studio 16.8、MSBuild 16.8 和 .NET 5.0 需要 NuGet.exe 5.8 或更高版本。


## <a name="summary-whats-new-in-58"></a>摘要：5.8 中的新增功能
🎉 **这是第一个版本，用于为面向 .net 5.0 的 NuGet 包提供完整创作和还原支持** 🎉

* 使用 mmap/ [#9807](https://github.com/NuGet/Home/issues/9807) CreateFileMapping 提高 nupkg 提取速度

* 包管理器 UI 包详细信息窗格中显示包漏洞详细信息- [#9850](https://github.com/NuGet/Home/issues/9850)

* 用新的命令 #8051 验证已签名 [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) 的[#8051](https://github.com/NuGet/Home/issues/8051) NuGet 包

* [`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) 支持 `--prerelease` 添加包的最新版本的选项，其中包括预发行版本- [#4699](https://github.com/NuGet/Home/issues/4699)

* 通过 [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) 命令[#9704](https://github.com/NuGet/Home/issues/9704)在 CLI 中搜索包

* [`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) 命令支持 `--verbosity` 选项 [#9600](https://github.com/NuGet/Home/issues/9600)

* 在 Visual Studio 中为基于 PackageReference 的 .csproj 样式的项目启用快速 No-Op 还原优化- [#9565](https://github.com/NuGet/Home/issues/9565)

* 解决方案级包管理器 UI 操作（如包安装和更新）的速度高达10倍- [#6010](https://github.com/NuGet/Home/issues/6010)

* Visual Studio 中的其他几个 NuGet 性能改进- [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052) [#9903](https://github.com/NuGet/Home/issues/9903)


### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Dcr**

* .NET 5.0 TFM：框架优先规则- [#9436](https://github.com/NuGet/Home/issues/9436)

* 分析 TargetFramework 时，NuGet 不应推断点平台版本 [#9842](https://github.com/NuGet/Home/issues/9842)

* 使用 TargetFrameworkMoniker & TargetPlatformMoniker 来推断框架，而不是使用单个 TFI、TFV、TPI、TPV 属性- [#9895](https://github.com/NuGet/Home/issues/9895)

* 更新 `GetReferenceNearestTargetFrameworkTask()` 以支持平台 (的目标框架，如 net 5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)

* .NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)

* 程序包管理器 UI：合并或更新包操作由于 (包降级等错误而不会被阻止 ) - [#9224](https://github.com/NuGet/Home/issues/9224)

* 对于具有功能的项目，NuGet 功能应会亮起;"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)

* 禁止在 Visual Studio 中 No-Op 还原消息- [#6384](https://github.com/NuGet/Home/issues/6384)

**漏洞**

* 不应在后台线程上调用 OutputWindowTextWriter 构造函数- [#9764](https://github.com/NuGet/Home/issues/9764)

* 在大 Endian Cpu 上还原签名包- [#9547](https://github.com/NuGet/Home/issues/9547)

* OutputConsoleLogger 不应调用 MEF 构造函数中的关联方法- [#9591](https://github.com/NuGet/Home/issues/9591)

* NuGet 中的 Bug `PrintJustified()` 方法- [#9737](https://github.com/NuGet/Home/issues/9737)

* 由于绑定错误而对包元数据进行垃圾回收时，包管理器 UI 内存泄漏 [#9757](https://github.com/NuGet/Home/issues/9757)

* 签名使用包管理器 UI 中的 packages.config 格式安装签名包时，错误列表中未显示任何警告- [#9798](https://github.com/NuGet/Home/issues/9798)

* XPlat 不应具有公共 Api- [#9821](https://github.com/NuGet/Home/issues/9821)

* 通过使用 #9822 阻止线程池线程来减少解决方案加载时的资源争用 `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)

* 在命令行还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息 [#9869](https://github.com/NuGet/Home/issues/9869)

* 通过 TargetFrameworkInformation 项读取运行时标识符图形- [#9874](https://github.com/NuGet/Home/issues/9874)

* 与 Visual Studio 和常规 MSBuild 评估还原相比，静态图形还原与 CrossTargeting 属性不一致 [#9881](https://github.com/NuGet/Home/issues/9881)

* 在静态图形还原中，对于多目标项目，NuGet 应从内部版本中读取与目标框架相关的信息。 - [#9870](https://github.com/NuGet/Home/issues/9870)

* 允许 `net5.0-platform` 在 Visual Studio 中加载和还原项目- [#9863](https://github.com/NuGet/Home/issues/9863)

* 在包管理器 UI 中显示解析的版本- [#9826](https://github.com/NuGet/Home/issues/9826)

* 程序包管理器 UI：解决方案资源管理器未显示所有 NuGet 包依赖项- [#9898](https://github.com/NuGet/Home/issues/9898)

* 更新 SPDX 许可证列表- [#9946](https://github.com/NuGet/Home/issues/9946)

* 打开 "管理 NuGet 包" 后发生 VS 2019 崩溃：图标导致图像 conversio 中出现未经处理的异常- [#9696](https://github.com/NuGet/Home/issues/9696)

* 需要 ilmerge 来排除 Newtonsoft.Js[#9966](https://github.com/NuGet/Home/issues/9966)

* 当没有错误时，具有 ContinuePackingAfterGeneratingNuspec = false 的装箱应失败- [#9786](https://github.com/NuGet/Home/issues/9786)

* 程序包管理器 UI：图标不能正确地反转颜色- [#10017](https://github.com/NuGet/Home/issues/10017)

* 还原时最新项目和 No-Op 项目的项目计数不正确- [#10026](https://github.com/NuGet/Home/issues/10026)

* 使用 `/p:RestoreUseStaticGraphEvaluation=true` 值中的结果不能为 Null- [#9280](https://github.com/NuGet/Home/issues/9280)

* `dotnet pack` 错误地将 alias 用于 WPF 库项目- [#10020](https://github.com/NuGet/Home/issues/10020)

* 程序包管理器 UI：签名验证失败时的 NullReferenceException- [#10042](https://github.com/NuGet/Home/issues/10042)

* Codespaces：不使用 `object` 项目元数据值的类型- [#10055](https://github.com/NuGet/Home/issues/10055)

* Codespaces：在 "工具选项" 中保存包源将覆盖凭据- [#9711](https://github.com/NuGet/Home/issues/9711)


**[此版本中已修复的所有问题的列表-5。8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**

**[此版本中已修复的问题/提交列表-5。8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**

### <a name="community-contributions"></a>社区参与

感谢所有有助于使此 NuGet 版本非常出色的参与者！

|谁|Pr|问题|
|----|----|----|
[omajid](https://github.com/omajid) | [3437](https://github.com/NuGet/NuGet.Client/pull/3437) | 错误消息中有拼写错误。 "管理员" 而不是 "administrator"- [#9662](https://github.com/NuGet/Home/issues/9662)
[odalet](https://github.com/odalet) | [3341](https://github.com/NuGet/NuGet.Client/pull/3341) | 具有无效 AssemblyInformationalVersion 报表的 NuGet 包 "说明是必需的"- [#5548](https://github.com/NuGet/Home/issues/5548)
[campersau](https://github.com/campersau) | [3501](https://github.com/NuGet/NuGet.Client/pull/3501) | `RepositoryMetadata.Equals()` 不考虑分支和提交属性- [#9613](https://github.com/NuGet/Home/issues/9613)
[Youssef1313](https://github.com/Youssef1313) | [3599](https://github.com/NuGet/NuGet.Client/pull/3599) | 单击 "Visual Studio 中的" "代码" 错误列表窗口应会转向 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)
[ChrisMaddock](https://github.com/ChrisMaddock) | [3624](https://github.com/NuGet/NuGet.Client/pull/3624) | 通过 Visual Studio 选项添加新包源时使用 "https://"- [#9974](https://github.com/NuGet/Home/issues/9974)
[Therzok](https://github.com/Therzok) | [3636](https://github.com/NuGet/NuGet.Client/pull/3636) | `RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989)上的性能问题
[thomaslevesque](https://github.com/thomaslevesque) | [3442](https://github.com/NuGet/NuGet.Client/pull/3442) | 为 SemanticVersion 类添加 TypeConverter- [#9125](https://github.com/NuGet/Home/issues/9125)


## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。  对于 NuGet 中的新问题，请报告 [GitHub 问题](hhttps://github.com/NuGet/Home/issues/new)。
对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题** 。
