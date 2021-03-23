---
title: NuGet 5.9 发行说明
description: NuGet 5.9 的发行说明，包括新功能、bug 修复和 Dcr。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859523"
---
# <a name="nuget-59-release-notes"></a>NuGet 5.9 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本 | 适用于 .NET SDK |
|:---|:---|:---|
| [**5.9**](https://nuget.org/downloads) | [Visual Studio 2019 版本16。9](https://visualstudio.microsoft.com/downloads/) | [5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup> |

<sup>1</sup> 与带有 .net Core 工作负载的 Visual Studio 2019 一起安装
  
> [!NOTE]
> Visual Studio 16.9、MSBuild 16.9 和 .NET 5.0.3 + 要求 NuGet.exe 5.9 或更高版本。

## <a name="summary-whats-new-in-59"></a>摘要：5.9 中的新增功能

* 为包依赖项添加 "更新" 上下文菜单项，这些依赖项用于启动带有预选包的包管理器 UI 以更新- [#10378](https://github.com/NuGet/Home/issues/10378)

    ![右键单击 "更新" 包体验](media/releasenotes-59-update.png)

* 在解决方案级包管理器 UI 中显示 "项目" 列表的 "版本" 列中 (包括浮动版本或版本范围请求) 请求的版本- [#9827](https://github.com/NuGet/Home/issues/9827)

    ![解决方案级包管理器 UI 中的请求版本](media/releasenotes-59-requested-version.png)

* 包管理器 UI "浏览" 选项卡中的 IntelliCode 包建议，作为 A/B 测试 [#10053](https://github.com/NuGet/Home/issues/10053)

* 扩展 `.nupkg.metadata` 文件以包含安装源- [#10354](https://github.com/NuGet/Home/issues/10354)

* 引入一个新的 msbuild 属性，以便在包任务期间排除特定 Tfm 的生成输出- [#10396](https://github.com/NuGet/Home/issues/10396)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Dcr (设计更改请求) ：**

* 当安装了最新的包版本时，关闭图标图标是不是直观的。 旧的绿色勾选标记为完美 [#9789](https://github.com/NuGet/Home/issues/9789)

* Nuget 调试详细级别应指出包来自何处- [#3055](https://github.com/NuGet/Home/issues/3055)

* NuGet 包应不正确地省略句点 in 版本号- [#9215](https://github.com/NuGet/Home/issues/9215)

* [CPVM]禁用集中传递依赖项的固定- [#10132](https://github.com/NuGet/Home/issues/10132)

* net5 TFM：缺少 TPV 时产生错误 [#9441](https://github.com/NuGet/Home/issues/9441)

* 在提取) 期间 (还原日志记录期间记录包- [#10384](https://github.com/NuGet/Home/issues/10384)

* 为旧 PR 项目实现一种预先注册机制，在解决方案打开时调用 restore [#9986](https://github.com/NuGet/Home/issues/9986)

* 当在包管理器中选择多个源时，NuGet 包推荐器应该工作- [#10433](https://github.com/NuGet/Home/issues/10433)

* 如果按正常的详细级别还原，请记录正在从中还原包的源 [#10461](https://github.com/NuGet/Home/issues/10461)

**漏洞**

* INuGetPackageFileService-为 Codespaces 连接的和独立的[#10151](https://github.com/NuGet/Home/issues/10151)提取映像和嵌入式许可证

* VS OE： IProjectMetadataContextInfo 缺少格式化程序- [#10079](https://github.com/NuGet/Home/issues/10079)

* [CPVM]减少写入到 centralTransitiveDependencyGroups 的信息- [#10002](https://github.com/NuGet/Home/issues/10002)

* 由于未加载项目而引发的还原操作会报告为 `NoOp` 遥测- [#9985](https://github.com/NuGet/Home/issues/9985)

* 具有特定颜色托盘的图标导致 PM UI 崩溃与 [#10037](https://github.com/NuGet/Home/issues/10037)

* [CPVM]添加 CPVM 信息时减少 PackageSpec 克隆- [#10003](https://github.com/NuGet/Home/issues/10003)

* PM UI-asyncify 图标加载- [#10009](https://github.com/NuGet/Home/issues/10009)

* 在 PM UI 中加载图标 Url 时的 UI 延迟- [#8505](https://github.com/NuGet/Home/issues/8505)

* BitmapSource 和 WPF UI 线程中的线程关联- [#9161](https://github.com/NuGet/Home/issues/9161)

* Packastool 带有 targetframework 别名[#10097](https://github.com/NuGet/Home/issues/10097)时警告 NU5128

* 自定义生成中包目标中的 OutputPath 逻辑不能正常工作- [#9234](https://github.com/NuGet/Home/issues/9234)

* VS OE：在客户端上缓存 IServiceBroker 实例- [#10141](https://github.com/NuGet/Home/issues/10141)

* 创建用于从 PM UI 中卸载的 NuGetProjectActions 并行操作- [#9956](https://github.com/NuGet/Home/issues/9956)

* 性能：减少旧项目和非 PR 项目的 GetPackageSpecsAsync 中的 UIDelays- [#9953](https://github.com/NuGet/Home/issues/9953)

* ``dotnet nuget push *.nupkg`` 不推送多个文件 [#4393](https://github.com/NuGet/Home/issues/4393)

* 重[#10198](https://github.com/NuGet/Home/issues/10198)定向时，输出将在 macOS 上的80个字符处换行

* 还原失败，并出现-Source <Relative Path>  -  [#9406](https://github.com/NuGet/Home/issues/9406)

* netcoreapp 5.0-windows 不往返行程并且不分析平台信息- [#10177](https://github.com/NuGet/Home/issues/10177)

* 自定义 CPS 项目需要 AssemblyReferences 项目功能才能进行还原。 - [#8071](https://github.com/NuGet/Home/issues/8071)

* 许可证和图标文件存在检查应始终使用区分大小写的比较 [#9817](https://github.com/NuGet/Home/issues/9817)

* DotnetCLiToolReference 还原使得不项目计数/uptodateprojectscount 的原因非常困难- [#10038](https://github.com/NuGet/Home/issues/10038)

* 在深色主题中通过 "选择 NuGet 包管理器格式" 对话框导航到选项卡时，很难查看包格式的划线框- [#9729](https://github.com/NuGet/Home/issues/9729)

* 从 #10314 中排除传递框架引用 `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)

* 比较器静态属性应该是幂等的 [#10339](https://github.com/NuGet/Home/issues/10339)

* 解析内部协定程序集加载 (修复 RPS 或获取异常) - [#9919](https://github.com/NuGet/Home/issues/9919)

* 将 GetService 替换为 NuGet 中的 Getserviceasyn。客户端，第1部分- [#10362](https://github.com/NuGet/Home/issues/10362)

* CLI 安装不应安装未列出的包- [#7466](https://github.com/NuGet/Home/issues/7466)

* 静态 msbuild graph 恢复-有关 MSBuildStartupDirectory 的 unnnecessary 日志记录- [#10335](https://github.com/NuGet/Home/issues/10335)

* 标记为 PrivateAssets 的 Projectreference 的项目依赖项不应包含在 "锁定文件最新" 复选 [#8565](https://github.com/NuGet/Home/issues/8565)

* 包含错误数据的 SDK 项目未在 VS [#10406](https://github.com/NuGet/Home/issues/10406)中显示还原错误

* 使用 LockedMode [#9623](https://github.com/NuGet/Home/issues/9623)从 cmd 行还原具有混合旧项目和 netstandard2 项目的解决方案时，NU1004

* 包包含通过依赖项包引入的内容到当前项目的包中， (基于 SDK 的项目仅) - [#8867](https://github.com/NuGet/Home/issues/8867)

* 为 NuGet 的 VS 扩展性 API 故障添加遥测- [#10062](https://github.com/NuGet/Home/issues/10062)

* 在静态图形还原中添加 GenerateRestoreGraphFile 以改善 debugability。  - [#10365](https://github.com/NuGet/Home/issues/10365)

* 无法打开 NuGet 包管理器- [#10336](https://github.com/NuGet/Home/issues/10336)

* NVDA/讲述人未阅读 "Apache-2.0" 链接[#10425](https://github.com/NuGet/Home/issues/10425)的 "许可证" 标签

* 在 VS [#9402](https://github.com/NuGet/Home/issues/9402)中，最新状态栏消息不太好

* packages.config 上的 package.lock.js使用不正确的目标框架- [#10257](https://github.com/NuGet/Home/issues/10257)

* Codespaces：修复 https://github.com/NuGet/NuGet.Client/pull/3786  -  [#10439](https://github.com/NuGet/Home/issues/10439)的遥测

* 启用 "RestoreLockedMode" 后生成解决方案时，NU1004 错误消失- [#8973](https://github.com/NuGet/Home/issues/8973)

* 反向跳转到反向中的 PMUI 应向前镜像 [#10234](https://github.com/NuGet/Home/issues/10234)

* 在实验实例中调试 PMUI 有时会引发从 SolutionView 到 ProjectView [#10416](https://github.com/NuGet/Home/issues/10416)的 InvalidCastException

* 在 "浏览" 选项卡中单击弃用的包后，默认版本为 null- [#10380](https://github.com/NuGet/Home/issues/10380)

* 重新获得焦点时，Visual Studio 中的 NuGet 管理器将重新加载- [#4176](https://github.com/NuGet/Home/issues/4176)

* 删除 IPackageSourceProvider2 和相关类型- [#10098](https://github.com/NuGet/Home/issues/10098)

* 包 "NameOfPackage" 与项目中的 "全部" 框架不兼容- [#5127](https://github.com/NuGet/Home/issues/5127)

* CreateVersionsAsync 不必要的 NuGetVersion 比较- [#10436](https://github.com/NuGet/Home/issues/10436)

* NuGet。客户端应使用 ManagedImageMonikers 和[#9977](https://github.com/NuGet/Home/issues/9977) KnownMonikers 替换

* 不推荐使用的图标与浏览器选项卡中不推荐使用的包的版本重叠- [#10452](https://github.com/NuGet/Home/issues/10452)

* PackageReference NU1604 错误处理不同于 VS 和命令行 (Restore & 程序包管理器 UI) - [#9289](https://github.com/NuGet/Home/issues/9289)

* Codespaces：未注册必要的格式化程序- [#10467](https://github.com/NuGet/Home/issues/10467)

* 从 NuGet 将 net45 作为目标框架删除- [#10470](https://github.com/NuGet/Home/issues/10470)

* 实现-添加新的 telemetries 以跟踪与 PMC 和 Powershell 使用相关的事件。 - [#10142](https://github.com/NuGet/Home/issues/10142)

* 当包管理器 UI 中有多个可更新的包时，"预览更改" 窗口中只显示一个包- [#10483](https://github.com/NuGet/Home/issues/10483)

* 打包 multitargeted 项目时，应生成空的 frameworkReferences 组- [#10218](https://github.com/NuGet/Home/issues/10218)

* 如果 "更新" 选项卡上的 "更新" 选项卡[#8963](https://github.com/NuGet/Home/issues/8963))  (中的 "选择" 选项卡上的复选框为突出显示，则很难查看 "更新" 选项卡中的程序包

* "更新" 选项卡复选框无法很好地与屏幕阅读器一起使用- [#10449](https://github.com/NuGet/Home/issues/10449)

* 在 PMUI 中进行更新会导致对象引用未设置为对象的实例- [#9882](https://github.com/NuGet/Home/issues/9882)

* 实现-添加新的 telemetries 以跟踪与 PMC 相关的事件，并跟进 Powershell 使用情况。 - [#10478](https://github.com/NuGet/Home/issues/10478)

* V2FeedPackageInfo 中的复制粘贴错误- [#10480](https://github.com/NuGet/Home/issues/10480)

* NuGetPackageFileService 修复-使用 for 可释放 memorystream- [#10503](https://github.com/NuGet/Home/issues/10503)


**[此版本中已修复的所有问题的列表-5.9。0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**

**[此版本中的提交列表-5.9。0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**

### <a name="community-contributions"></a>社区参与

感谢所有有助于使此 NuGet 版本非常出色的参与者！

|谁|Pr|问题|
|----|----|----|
[omajid](https://github.com/omajid) | [3865](https://github.com/NuGet/NuGet.Client/pull/3865) | V2FeedPackageInfo 中的复制粘贴错误- [#10480](https://github.com/NuGet/Home/issues/10480)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3812](https://github.com/NuGet/NuGet.Client/pull/3812) | 对于用 PrivateAssets = "All" 属性引用包的情况，缺少测试 [#10397](https://github.com/NuGet/Home/issues/10397)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3739](https://github.com/NuGet/NuGet.Client/pull/3739) | 添加了推送多个包的支持- [#4393](https://github.com/NuGet/Home/issues/4393)
[marcin-krystianc](https://github.com/marcin-krystianc) | [3723](https://github.com/NuGet/NuGet.Client/pull/3723) | 禁用程序集签名时，NuGet 库的生成已断开- [#10173](https://github.com/NuGet/Home/issues/10173)
[kant2002](https://github.com/kant2002) | [3807](https://github.com/NuGet/NuGet.Client/pull/3807) | 清理参与的文档- [#10399](https://github.com/NuGet/Home/issues/10399)
[PathogenDavid](https://github.com/PathogenDavid) | [3754](https://github.com/NuGet/NuGet.Client/pull/3754) | 许可证和图标文件存在检查应始终使用区分大小写的比较 [#9817](https://github.com/NuGet/Home/issues/9817)
[campersau](https://github.com/campersau) | [3677](https://github.com/NuGet/NuGet.Client/pull/3677) | 使用 DecodePixelWidth [#10037](https://github.com/NuGet/Home/issues/10037)时，请使用 IGNORECOLORPROFILE 解决 WPF 问题
[bjorkstromm](https://github.com/bjorkstromm) | [3697](https://github.com/NuGet/NuGet.Client/pull/3697) | NuGet 中 Windows SDK 10 链接已断开。客户端贡献指南- [#10099](https://github.com/NuGet/Home/issues/10099)
[bjorkstromm](https://github.com/bjorkstromm) | [3696](https://github.com/NuGet/NuGet.Client/pull/3696) | NuGet 中的相对链接断开。客户端调试指南- [#10100](https://github.com/NuGet/Home/issues/10100)
[Nirmal4G](https://github.com/Nirmal4G) | [3637](https://github.com/NuGet/NuGet.Client/pull/3637) | 改善测试装置和相关的代码- [#9996](https://github.com/NuGet/Home/issues/9996)
[rolfbjarne](https://github.com/rolfbjarne) | [3743](https://github.com/NuGet/NuGet.Client/pull/3743) | 重[#10198](https://github.com/NuGet/Home/issues/10198)定向时，输出将在 macOS 上的80个字符处换行
[xen2](https://github.com/xen2) | [2861](https://github.com/NuGet/NuGet.Client/pull/2861) | 使 Nuget.exe 作为 .NET Standard 包提供 [#6150](https://github.com/NuGet/Home/issues/6150)
[Anipik](https://github.com/Anipik) | [3810](https://github.com/NuGet/NuGet.Client/pull/3810) | 引入一个新的 msbuild 属性，以便在包任务期间排除特定 tfm 的生成输出- [#10396](https://github.com/NuGet/Home/issues/10396)

## <a name="feedback-welcome"></a>欢迎反馈

反馈对我们非常重要。  如果此版本有任何问题，请查看有关现有问题的 [GitHub 问题](https://github.com/NuGet/Home/issues) 和 [Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/) 。  对于 NuGet 中的新问题，请报告 [GitHub 问题](https://github.com/NuGet/Home/issues/new)。
对于一般的 NuGet 体验问题，请通过 "帮助" 下的 "你喜欢的 IDE" 中的 " [报告问题](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) " 选项告知我们 **> 报告问题**。
