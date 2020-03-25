---
title: NuGet 5.5 发行说明
description: NuGet 5.5 的发行说明，包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0e8ab66c937058e84420bc3e3a5031cbc133aad7
ms.sourcegitcommit: 1a63a84da2719c8141823ac89a20bf507fd22b00
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2020
ms.locfileid: "80148281"
---
# <a name="nuget-55-release-notes"></a>NuGet 5.5 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**5.5.0**](https://nuget.org/downloads) | [Visual Studio 2019 版本16。5](https://visualstudio.microsoft.com/downloads/) | [3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装

## <a name="summary-whats-new-in-55"></a>摘要：5.5 中的新增功能

* 改进了 Visual Studio 中 NuGet 包管理器 UI 的辅助功能和屏幕阅读器体验
    * 屏幕阅读器体验中的辅助功能问题，缺少已安装文本框等的 altText 和可访问的名称， [#9059](https://github.com/NuGet/Home/issues/9059)
    * 包中的屏幕阅读器体验中的辅助功能问题列表- [#9077](https://github.com/NuGet/Home/issues/9077)
    * 屏幕阅读器体验中与 "浏览"、"安装" 和 "更新" 选项卡相关的辅助功能问题- [#9078](https://github.com/NuGet/Home/issues/9078)
    * 讲述人不会公告 "空白"、"无 Dependencies" "、" "nuget"、"MIT" 链接标签[#9157](https://github.com/NuGet/Home/issues/9157)

* 支持在 Visual Studio 包管理器 UI 中为本地源上承载的包提供自包含的图标- [#8189](https://github.com/NuGet/Home/issues/8189)

* 使用 `RestoreUseStaticGraphEvaluation` 提高了无操作还原性能，从而可通过调用 MSBuild 静态图形 Api 来加快评估- [8791](https://github.com/NuGet/Home/issues/8791)

* 通过跨平台身份验证插件改进 dotnet 的可靠性
    * dotnet restore 失败，TaskCanceledException- [#7842](https://github.com/NuGet/Home/issues/7842)
    * 插件： "已取消任务"-由于此原因，ADO 身份验证存在问题。 - [#8528](https://github.com/NuGet/Home/issues/8528)

* 添加 `dotnet nuget <add|remove|update|disable|enable|list> source` 命令- [#4126](https://github.com/NuGet/Home/issues/4126)

* 使用 dotnet nuget 推送[#8778](https://github.com/NuGet/Home/issues/8778)的 `--skip-duplicate` 的支持

* 支持 `packages.config` 与 msbuild/restore- [#8506](https://github.com/NuGet/Home/issues/8506)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

**Bug**

* 通过 V3 Api 改编自我更新程序- [#4197](https://github.com/NuGet/Home/issues/4197)

* 如果包依赖项版本设置为 "*"，则包依赖项版本错误- [#6697](https://github.com/NuGet/Home/issues/6697)

* ErrorUnsafePackageEntry 错误消息不指向问题的根源- [#7505](https://github.com/NuGet/Home/issues/7505)

* 锁定文件不采用 "*" 方案- [#8073](https://github.com/NuGet/Home/issues/8073)

* 在 PackageReference 中使用 * 时，Nuget.exe 不会解析为包的最新版本（MSBuild/Dotnet/VS restore do）- [#8432](https://github.com/NuGet/Home/issues/8432)

* 具有多个目标 WPF 项目的 dotnet 列表包- [#8463](https://github.com/NuGet/Home/issues/8463)

* 改善 ConcurrencyUtilities （降低 CPU 使用率）- [#8653](https://github.com/NuGet/Home/issues/8653)

* 不应在预览还原中编写已卸载项目方案的 DG 规范- [#8793](https://github.com/NuGet/Home/issues/8793)

* Visual Studio NuGet 包（RestoreManagerPackage）需要自动加载解决方案生成事件- [#8796](https://github.com/NuGet/Home/issues/8796)

* .Vssettings 初始化中的死锁- [#8842](https://github.com/NuGet/Home/issues/8842)

* 如果项目位于解决方案文件夹中，则不会从 NuGet 包填充 VisualStudio 工具箱- [#8868](https://github.com/NuGet/Home/issues/8868)

* VS：由于争用条件，解决方案还原永久失败- [#8881](https://github.com/NuGet/Home/issues/8881)

* "正在安装" 选项卡上的 "正在加载 ..." 和 "搜索 <term>... "更新选项卡- [#8890](https://github.com/NuGet/Home/issues/8890)

* 缓存过期后，VS PM UI 中缺少嵌入的图标- [#9069](https://github.com/NuGet/Home/issues/9069)

* FireAndForget PM UI 启动- [#9112](https://github.com/NuGet/Home/issues/9112)

* Restore： IncludeExcludeFiles （...）实现不正确- [#9167](https://github.com/NuGet/Home/issues/9167)

* Restore： PackageSpec （）创建不相等的克隆[#9211](https://github.com/NuGet/Home/issues/9211)

* 未选中错误列表 "如果生成完成但有错误，则显示错误列表" 的错误列表- [#8190](https://github.com/NuGet/Home/issues/8190)

* 静态图形还原不应传递空的 SolutionPath [#9061](https://github.com/NuGet/Home/issues/9061)

* 还原：计算每个项目4次的结束时间- [#9042](https://github.com/NuGet/Home/issues/9042)

* Restore： DependencyGraphSpec （...）不需要 JObject- [#9040](https://github.com/NuGet/Home/issues/9040)

* 还原：在大型对象堆（LOH）上创建的大型字符串- [#9031](https://github.com/NuGet/Home/issues/9031)

* 新 mono 上的自定义 nuget.exe 可能因 MSBuild SDK 解析程序而中断- [8848](https://github.com/NuGet/Home/issues/8848)

* dgspec "由其他进程使用" 时还原失败- [8692](https://github.com/NuGet/Home/issues/8692)

**Dcr**

* _GetRestoreProjectStyle 中的逻辑应在任务[#8804](https://github.com/NuGet/Home/issues/8804)

* 默认情况下，在 "已安装" 选项卡上添加弃用信息- [#8541](https://github.com/NuGet/Home/issues/8541)

**[此版本中已修复的所有问题的列表-5。5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**
