---
title: NuGet 5.10 发行说明
description: NuGet 5.10 的发行说明，包括新功能、bug 修复和 dcr。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 80a372074604f5c0073f78927b84de00e78acc74
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726946"
---
# <a name="nuget-510-release-notes"></a>NuGet 5.10 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.10.0**](https://nuget.org/downloads) | [Visual Studio 2019 16.10 版](https://visualstudio.microsoft.com/downloads/) | [5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup>随 .net Core 工作负载一起安装了 Visual Studio 2019
  
> [!NOTE]
> Visual Studio 16.10、MSBuild 16.10 和 .net 5.0.300 + 需要 NuGet.exe 5.10 或更高版本。

## <a name="summary-whats-new-in-510"></a>摘要：5.10 中的新增功能

* 签名：实现 dotnet 受信任的签名者命令- [#8053](https://github.com/NuGet/Home/issues/8053)

* 在 Linux 上禁用默认验证并在默认情况下启用 Windows- [#10713](https://github.com/NuGet/Home/issues/10713)

* 为 .NET 5 + Linux/MAC 上的包签名验证添加一个 ENV 变量- [#10742](https://github.com/NuGet/Home/issues/10742)

* 为大型解决方案提高安装新包性能- [#10166](https://github.com/NuGet/Home/issues/10166)

* 将项目类型添加 `nfproj` 到 NUGET CLI 的 supportedProjectExtensions 列表中。 - [#10562](https://github.com/NuGet/Home/issues/10562)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

* `<requireLicenseAcceptance>`封装项目时禁止显示元素- [#5133](https://github.com/NuGet/Home/issues/5133)

* [CPVM] 预览警告应显示在 dotnet cli 上- [#10226](https://github.com/NuGet/Home/issues/10226)

* 将 PMUI 的背景色和前景色标记更新为 CommonDocumentColors- [#10608](https://github.com/NuGet/Home/issues/10608)

* [Bug Bash]在 PM UI 中快速切换选项卡时错误列表窗口中显示错误 "用户已取消操作"- [#10671](https://github.com/NuGet/Home/issues/10671)

* PM UI：提高解决方案级别的包安装性能- [#10210](https://github.com/NuGet/Home/issues/10210)

* 在 NuGet 中的任何位置将 GetService 替换为 Getserviceasyn。客户端- [#3784](https://github.com/NuGet/Home/issues/3784)

* 相对路径 NuGet.exe 包性能问题 `..` - [#5016](https://github.com/NuGet/Home/issues/5016)

* "Nuget 包" 的性能随着源路径中增加的级别而降低- [#5706](https://github.com/NuGet/Home/issues/5706)

* 将 nuspec 与重复文件一起打包时，NuGet 不会出错。 - [#6941](https://github.com/NuGet/Home/issues/6941)

* NuGet pack "指定的 DateTimeOffset 无法转换为 Zip 文件时间戳"- [#7001](https://github.com/NuGet/Home/issues/7001)

* 已打包包的文件的时间戳按时区 [#7395](https://github.com/NuGet/Home/issues/7395)

* NU1004 应包含更具可操作性的信息 [#7696](https://github.com/NuGet/Home/issues/7696)

* [Bug Bash][测试失败]在运行 "dotnet restore--------lock--锁定模式" 时，不应更新空/格式错误的锁定文件- [#8640](https://github.com/NuGet/Home/issues/8640)

* NuGetVersionRange 允许对逻辑上错误的范围进行分析- [#9145](https://github.com/NuGet/Home/issues/9145)

* PM UI 无法显示所选和悬停包源之间的区分背景色- [#9538](https://github.com/NuGet/Home/issues/9538)

* 屏幕阅读器未读取用于选择要安装到的项目的复选框- [#9578](https://github.com/NuGet/Home/issues/9578)

* 详细信息窗格版本下拉列表应在 "已安装/更新" 选项卡上安装/LatestStable- [#9887](https://github.com/NuGet/Home/issues/9887)

* 删除某些 .net 5 sdk 报表 TargetPlatformMoniker 的解决方法帐户 ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)

* dotnet nuget 验证过安静- [#10316](https://github.com/NuGet/Home/issues/10316)

* VersionRange 无法分析一位数的范围- [#10342](https://github.com/NuGet/Home/issues/10342)

* VS 解决方案管理器在调试期间引发 null 异常- [#10352](https://github.com/NuGet/Home/issues/10352)

* 将 CLI 异常消息移动到字符串资源文件- [#10392](https://github.com/NuGet/Home/issues/10392)

*  (TabItemButtonAutomationPeer) 删除死代码- [#10435](https://github.com/NuGet/Home/issues/10435)

* 更新上下文菜单应该滚动到首个选定项- [#10498](https://github.com/NuGet/Home/issues/10498)

* 解决方案 PMUI 详细信息具有重叠的水平栏 [#10533](https://github.com/NuGet/Home/issues/10533)

* 签名：证书过期和时间戳不受信任时未显示主签名详细信息- [#10535](https://github.com/NuGet/Home/issues/10535)

* 没有启用的源会阻止 PM UI 显示- [#10541](https://github.com/NuGet/Home/issues/10541)

* 包元数据 (详细信息、弃用) 有时不会从 CodeSpaces 中的 nuget.org 提取- [#10549](https://github.com/NuGet/Home/issues/10549)

* 调试会话期间，PMUI 初始化失败并出现异常 [#10559](https://github.com/NuGet/Home/issues/10559)

* nuget 还原导致大型 endian 系统上的包完整性检查失败- [#10567](https://github.com/NuGet/Home/issues/10567)

* 引发 FormatException 而不是 PackagingException- [#10595](https://github.com/NuGet/Home/issues/10595)

* CPVM-图形遍历算法中的并发问题- [#10598](https://github.com/NuGet/Home/issues/10598)

* 添加 PMC powershell 版本遥测- [#10609](https://github.com/NuGet/Home/issues/10609)

* 提高 NuGetVersion 排序性能- [#10611](https://github.com/NuGet/Home/issues/10611)

* 受信任的签名者添加具有不一致的参数- [#10647](https://github.com/NuGet/Home/issues/10647)

* Vs2019 v 16.9.0：将 NuGet 程序包管理器中的选项卡从 "更新" 切换到 "已安装" 不会更新框架。 - [#10654](https://github.com/NuGet/Home/issues/10654)

* 从 PMUI 中的版本号删除 "v"- [#10677](https://github.com/NuGet/Home/issues/10677)

* INuGetProjectService 在接收 CPS 项目系统提名前引发 GetInstalledPackagesAsync [#10681](https://github.com/NuGet/Home/issues/10681)

* "浏览" 选项卡上的嵌入图标导致拒绝访问源 "Microsoft Visual Studio 脱机包"- [#10687](https://github.com/NuGet/Home/issues/10687)

* MSBuildProjectExtensionsPath 未设置时，将引发 INuGetProjectService GetInstalledPackagesAsync- [#10739](https://github.com/NuGet/Home/issues/10739)

* 第一次时，"dotnet nuget remove source nuget.org" 不起作用- [#10745](https://github.com/NuGet/Home/issues/10745)

* Nuget 在异步方法中阻止 threadpool 线程，该线程对 UI 线程进行同步调用- [#10775](https://github.com/NuGet/Home/issues/10775)

* `PackageLoadContext.GetInstalledAndTransitivePackagesAsync` 为死信，并对性能产生影响- [#10790](https://github.com/NuGet/Home/issues/10790)

* 在 NuGet SDK 包中使用嵌入的图标- [#10795](https://github.com/NuGet/Home/issues/10795)

* 更新 SPDX 许可证列表- [#10806](https://github.com/NuGet/Home/issues/10806)

**[此版本中已修复的所有问题的列表-5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**
  
**[此版本中的提交列表-5.10。0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**
  
### <a name="community-contributions"></a>社区参与

感谢所有有助于使此 NuGet 完全发布的参与者！

|谁|Pr|问题|
|----|----|----|
[港-z](https://github.com/louis-z) | [3991](https://github.com/NuGet/NuGet.Client/pull/3991) | VersionRange 无法分析一位数的范围- [#10342](https://github.com/NuGet/Home/issues/10342)
[omajid](https://github.com/omajid) | [3860](https://github.com/NuGet/NuGet.Client/pull/3860) | NuGet。客户端 build.sh 已断开- [#10139](https://github.com/NuGet/Home/issues/10139)
[Nirmal4G](https://github.com/Nirmal4G) | [3623](https://github.com/NuGet/NuGet.Client/pull/3623) | NuGet。客户端 build.sh 已断开- [#10139](https://github.com/NuGet/Home/issues/10139)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | "Nuget 包" 的性能随着源路径中增加的级别而降低- [#5706](https://github.com/NuGet/Home/issues/5706)
[BlackGad](https://github.com/BlackGad) | [3953](https://github.com/NuGet/NuGet.Client/pull/3953) | NuGet.exe 包性能问题。 相对路径- [#5016](https://github.com/NuGet/Home/issues/5016)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3940](https://github.com/NuGet/NuGet.Client/pull/3940) | CPVM-图形遍历算法中的并发问题- [#10598](https://github.com/NuGet/Home/issues/10598)
[josesimoes](https://github.com/josesimoes) | [3943](https://github.com/NuGet/NuGet.Client/pull/3943) | 将项目类型 nfproj 添加到 Nuget CLI 的 supportedProjectExtensions 列表。 - [#10562](https://github.com/NuGet/Home/issues/10562)

## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本有任何问题，请查看[GitHub 问题](https://github.com/NuGet/Home/issues)并[Visual Studio 开发人员 Community](https://developercommunity.visualstudio.com/)了解现有问题。  NuGet 中的新问题，请报告[GitHub 问题](https://github.com/NuGet/Home/issues/new)。
如果遇到问题，请通过 "帮助" 中的 "报告问题" 选项（位于 "帮助" 下的 "[报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)" 选项来了解 NuGet **> 报告问题**。
