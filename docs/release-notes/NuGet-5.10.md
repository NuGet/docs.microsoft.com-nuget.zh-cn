---
title: NuGet 5.10 发行说明
description: NuGet 5.10 的发行说明，包括新功能、bug 修复和 DCR。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356496"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本 16.10](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 随 2019 Visual Studio .NET Core 工作负载一起安装
  
> [!NOTE]
> Visual Studio 16.10、MSBuild 16.10 和 .NET 5.0.300+ 需要 NuGet.exe 5.10 或更高版本。

## <a name="summary-whats-new-in-510"></a>摘要：5.10 中的新增功能

* 签名：实现 dotnet trusted-signers 命令 - [#8053](https://github.com/NuGet/Home/issues/8053)

* 在 Linux 上禁用默认验证，但在 Windows 上默认启用 - [#10713](https://github.com/NuGet/Home/issues/10713)

* 在 .NET 5+ Linux/MAC 上为包签名验证添加 ENV 变量 - [#10742](https://github.com/NuGet/Home/issues/10742)

* 提高大型解决方案的安装新包性能 - [#10166](https://github.com/NuGet/Home/issues/10166)

* 将项目类型 `nfproj` 添加到 Nuget CLI 的 supportedProjectExtensions 列表中。 - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

* 打包 <requireLicenseAcceptance> 项目时取消元素 - [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] 预览警告应显示在 dotnet cli 上 - [#10226](https://github.com/NuGet/Home/issues/10226)

* 将 PMUI 的背景和前景色标记更新为 CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash]在 PM UI 中快速切换选项卡时，错误"用户取消的操作"显示在"错误列表"窗口中 - [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI：提高解决方案级别的包安装性能 - [#10210](https://github.com/NuGet/Home/issues/10210)

* 将 GetService 替换为 NuGet.Clients 中所有位置的 GetServiceAsync - [#3784](https://github.com/NuGet/Home/issues/3784)

* NuGet.exe相对路径的包 `..` 性能问题 - [#5016](https://github.com/NuGet/Home/issues/5016)

* "nuget pack"的性能随源路径中的级别增加而降低 - [#5706](https://github.com/NuGet/Home/issues/5706)

* 使用重复文件打包 nuspec 时，NuGet 不会出错。 - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet 包"指定的 DateTimeOffset 不能转换为 Zip 文件时间戳"- [#7001](https://github.com/NuGet/Home/issues/7001)

* 打包包文件的时间戳按时区移动 - [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 应包含更多可操作的信息 - [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash][测试失败]运行 "dotnet restore --use-lock-file --locked-mode" 时，不应更新空的/格式错误的锁文件 - [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange 允许分析逻辑上不正确的范围 - [#9145](https://github.com/NuGet/Home/issues/9145)

* PM UI 无法显示所选包源和悬停包源之间的可区分背景色[-](https://github.com/NuGet/Home/issues/9538) #9538

* 屏幕阅读器无法读取选择要安装到的项目的复选框[-](https://github.com/NuGet/Home/issues/9578) #9578

* 详细信息窗格版本下拉列表的默认选择应为"已安装/更新"选项卡上的"已安装/最新""#9887 [](https://github.com/NuGet/Home/issues/9887)

* 删除某些 .NET 5 SDK 报表 TargetPlatformMoniker 的解决方法 ` ,Version= `  -  [帐户](https://github.com/NuGet/Home/issues/9913)#9913

* dotnet nuget verify 太静默 - [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange 无法分析单位数范围 - [#10342](https://github.com/NuGet/Home/issues/10342)

* VS 解决方案管理器在调试期间为 引发 null 异常 - [#10352](https://github.com/NuGet/Home/issues/10352)

* 将 CLI 异常消息移动到字符串资源文件 - [#10392](https://github.com/NuGet/Home/issues/10392)

* 删除 TabItemButtonAutomationPeer (死) - [#10435](https://github.com/NuGet/Home/issues/10435)

* 更新上下文菜单应滚动到第一个选定项 - [#10498](https://github.com/NuGet/Home/issues/10498)

* 解决方案 PMUI 详细信息具有重叠的水平条 - [#10533](https://github.com/NuGet/Home/issues/10533)

* 签名：证书过期且时间戳不受信任时不显示主签名详细信息 - [#10535](https://github.com/NuGet/Home/issues/10535)

* 如果没有启用的源，PM UI 将阻止显示 - [#10541](https://github.com/NuGet/Home/issues/10541)

* 包元数据 (详细信息，弃) 有时不会从 CodeSpaces 中的 nuget.org 请求 - [#10549](https://github.com/NuGet/Home/issues/10549)

* PMUI 初始化在调试会话期间失败，异常 - [#10559](https://github.com/NuGet/Home/issues/10559)

* nuget 还原会导致 big endian 系统上的包完整性检查失败 - [#10567](https://github.com/NuGet/Home/issues/10567)

* 引发 FormatException 而不是 PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM - 图形步进算法中的并发问题 - [#10598](https://github.com/NuGet/Home/issues/10598)

* 添加 PMC powershell 版本遥测 - [#10609](https://github.com/NuGet/Home/issues/10609)

* 提高 NuGetVersion 排序性能 - [#10611](https://github.com/NuGet/Home/issues/10611)

* Trusted-signers Add 具有不一致的参数 - [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v16.9.0：将 NuGet 程序包管理器中的选项卡从"更新"切换为"已安装"不会更新帧。 - [#10654](https://github.com/NuGet/Home/issues/10654)

* 从 PMUI 中的版本号中删除"v"- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService.GetInstalledPackagesAsync 在收到 CPS 项目系统提名前引发 - [#10681](https://github.com/NuGet/Home/issues/10681)

* 嵌入的图标会导致源"Microsoft Visual Studio脱机包"拒绝访问[-](https://github.com/NuGet/Home/issues/10687) #10687

* 未设置 MSBuildProjectExtensionsPath 时，INuGetProjectService.GetInstalledPackagesAsync 引发 - [#10739](https://github.com/NuGet/Home/issues/10739)

* "dotnet nuget remove source nuget.org"第一次不起作用 - [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget 阻止异步方法中的线程池线程对 UI 线程进行同步调用 - [#10775](https://github.com/NuGet/Home/issues/10775)

* 工具 ->选项 -> NuGet 程序包管理器字符串被截断 - [#10779](https://github.com/NuGet/Home/issues/10779)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 是死代码并损害性能 - [#10790](https://github.com/NuGet/Home/issues/10790)

* 在 NuGet SDK 包中使用嵌入式图标 - [#10795](https://github.com/NuGet/Home/issues/10795)

* 更新 SPDX 许可证列表 - [#10806](https://github.com/NuGet/Home/issues/10806)

**[此版本中已修复的所有问题的列表 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[此版本中的提交列表 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>社区参与

感谢所有参与者，他们帮助使此 NuGet 版本变得出色！

|谁|拉/拉|问题|
|----|----|----|
[将](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange 无法分析单位数范围 - [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet.Client build.sh 中断 - [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet.Client build.sh 中断 - [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | "nuget pack"的性能随源路径中的级别增加而降低 - [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe包性能问题。 相对路径 - [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM - 图形步进算法中的并发问题 - [#10598](https://github.com/NuGet/Home/issues/10598)
[一些](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | 将项目类型 nfproj 添加到 Nuget CLI 的 supportedProjectExtensions 列表中。 - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。  对于 NuGet 中的新问题，请报告 [GitHub 问题](https://github.com/NuGet/Home/issues/new)。
对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题**。
