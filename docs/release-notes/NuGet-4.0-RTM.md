---
title: NuGet 4.0 RC 发行说明
description: NuGet 4.0 RTM 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 03/03/2017
ms.topic: conceptual
ms.openlocfilehash: f1c5408f75966068e8fa11e63118426bbf562047
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-40-rtm-release-notes"></a>NuGet 4.0 RTM 发行说明

[Visual Studio 2017](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 采用的 NuGet 4.0 添加了 .NET Core 支持，拥有大量优质修补程序并可提高性能。 此版本还具有一些改进，如支持 PackageReference、作为 MSBuild 目标的 NuGet 命令、后台包还原等等。

## <a name="known-issues"></a>已知问题

### <a name="nuget-restore-may-fail-when-you-have-multiple-projects-referencing-another-project-in-a-solution"></a>当有多个项目引用解决方案中的另一项目时，NuGet 还原可能会失败

#### <a name="issue"></a>问题

如果解决方案中对同一项目的项目引用的大小写或路径不同，则 NuGet 还原可能会不起作用。 [NuGet#4574](https://github.com/NuGet/Home/issues/4574)

#### <a name="workaround"></a>解决方法

将所有项目引用的大小写和相对路径修复为相同。

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a>使用包管理器控制台时，“Enter”键可能不起作用

#### <a name="issue"></a>问题

有时无法在包管理器控制台中使用 Enter 键。 如果看到此内容，请在修补程序上签出进程，并提供有关重现步骤的其他任何有用信息。 [NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)

#### <a name="workaround"></a>解决方法

打开该解决方案之前，重启 Visual Studio 并打开 PMC。 或者，请尝试删除 `project.lock.json`，然后再次还原。

### <a name="in-net-core-projects-you-may-end-up-in-infinite-restore-loop-when-you-use-a-package-containing-an-assembly-with-an-invalid-signature"></a>在 .NET Core 项目中，使用包含具有无效签名的程序集的包时，可能会出现无限还原循环

#### <a name="issue"></a>问题

有时，使用包含具有无效签名的程序集的包或包版本设置有 'DateTime' 贴标时，会导致包自动还原无限循环运行。 [NuGet#4542](https://github.com/NuGet/Home/issues/4542)

#### <a name="workaround"></a>解决方法

目前没有解决方法。

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a>无法使用 NuGet 包管理器查看、添加或更新 DotNetCLITools

#### <a name="issue"></a>问题

NuGet 包管理器不显示，且不允许添加/更新 DotNetCLITools。 [NuGet#4256](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a>解决方法

必须在项目文件中手动编辑 DotNetCLIToolReferences。

### <a name="nuget-restore-will-fail-when-you-set-packageid-property-for-projects"></a>如果对项目设置 PackageId 属性，则 NuGet 包还原会失败

#### <a name="issue"></a>问题

对于 .NET Core 项目，Visual Studio 中的 NuGet 还原不遵从项目的 PackageId 属性。 [NuGet#4586](https://github.com/NuGet/Home/issues/4586)

#### <a name="workaround"></a>解决方法

使用命令行运行还原。

### <a name="when-your-project-does-not-have-obj-folder-package-restore-may-fail"></a>项目不包含 'obj' 文件夹时，包还原可能失败

#### <a name="issue"></a>问题

'obj' 文件夹被删除后 Visual Studio 无法还原 PackageReferences。 [NuGet#4528](https://github.com/NuGet/Home/issues/4528)

#### <a name="workaround"></a>解决方法

手动创建 'obj' 文件夹后应可正常进行还原。

### <a name="manually-updating-packages-using-update-package-in-console-may-fail"></a>在控制台中使用 Update-Package 手动更新包可能会失败

#### <a name="issue"></a>问题

在控制台中手动使用 Update-Package 对刚刚转换的 PackageReferences 项目仅适用一次。 [NuGet#4431](https://github.com/NuGet/Home/issues/4431)

#### <a name="workaround"></a>解决方法

目前没有解决方法。

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a>对目标框架版本重定目标可能会导致 Intellisense 不完整

#### <a name="issue"></a>问题

在 Visual Studio 中对目标框架版本重定目标可能会导致 Intellisense 不完整。 将 PackageReferences 用作包管理器格式时可能出现这种情况。 [NuGet#4216](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a>解决方法

手动进行还原。

### <a name="msbuild-trestore-fails-when-a-project-targeting-net461-references-another-project-targeting-netstandard"></a>面向 .NET461 的项目引用面向 .NETStandard 的另一项目时 msbuild /t:restore 出现失败

#### <a name="issue"></a>问题

面向 .NET461 的基于 PackageReferenece 的项目引用面向 .NETStandard 的另一基于 PackageReference 的项目时 msbuild /t:restore 出现失败。  [NuGet#4532](https://github.com/NuGet/Home/issues/4532)

#### <a name="workaround"></a>解决方法

目前没有解决方法。

## <a name="issues-fixed-in-nuget-40-rtm-timeframe"></a>NuGet 4.0 RTM 时间框架中已修复的问题

[NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md) - 列出了所有 NuGet 4.0 RC 中已修复的问题

### <a name="features"></a>功能

- 对 NuGet.Core.sln 中的字符串进行本地化 - [#2041](https://github.com/NuGet/Home/issues/2041)

- Nuget 强制加载 LSL 模式下的 Web 应用程序项目 - [#4258](https://github.com/NuGet/Home/issues/4258)

- 对于“已安装 SDK”的包，用于阻止 UI 中的版本更改的 AutoReferenced PackageReference 支持 - [#4044](https://github.com/NuGet/Home/issues/4044)

- 为任何项目依赖项 (PackageRef) 正确传达 PackageSpec.Version - [#3902](https://github.com/NuGet/Home/issues/3902)

- 支持从命令行删除引用到 `.csproj` 中 - [#4101](https://github.com/NuGet/Home/issues/4101)

- 支持对 PackageReference 项目（常规和 xplat）和轻型解决方案加载的还原 - [#4003](https://github.com/NuGet/Home/issues/4003)

- 支持将引用从命令行添加到 `.csproj` 中 - [#3751](https://github.com/NuGet/Home/issues/3751)

- 对于 `packages.config` 或 `project.json`，支持轻型解决方案加载的 NuGet 还原 - [#3711](https://github.com/NuGet/Home/issues/3711)

- 由 nuget 生成的目标文件中的 contentFiles 支持 - [#3683](https://github.com/NuGet/Home/issues/3683)

- 使用 MSBuild 在 Mac 上建立用于 nuget.exe 验证的 Mono CI - [#3646](https://github.com/NuGet/Home/issues/3646)

- 从 v2 NuGet.Core 依赖项中移出 NuGet - [#3645](https://github.com/NuGet/Home/issues/3645)

### <a name="bugs"></a>Bug

- Visual Studio 中的 NuGet 还原不遵从项目的 PackageId 属性 - [#4586](https://github.com/NuGet/Home/issues/4586)

- 在 vsix 包中添加包时，NuGet ProjectSystemCache 出现错误 - [#4545](https://github.com/NuGet/Home/issues/4545)

- 如果在具有多个 TFM 的项目中使用了 IncludeSource，包会引发异常 - [#4536](https://github.com/NuGet/Home/issues/4536)

- 使用解决方案范围的包管理的更新时，VS 2017 RC3 出现故障 - [#4474](https://github.com/NuGet/Home/issues/4474)

- 无法卸载新安装的包 - [#4435](https://github.com/NuGet/Home/issues/4435)

- 迁移到 PackageRef 时，混合解决方案出现异常还原行为 - [#4433](https://github.com/NuGet/Home/issues/4433)

- 如果在启动 NuGet 操作（安装、更新或还原）后立即进行生成操作，可能导致 VS 挂起 - [#4420](https://github.com/NuGet/Home/issues/4420)

- UI 挂起 - 死锁初始化 NuGet.SolutionRestoreManager.RestoreManagerPackage [#4371](https://github.com/NuGet/Home/issues/4371)

- add package 命令应将版本添加为属性（而不是元素）- [#4325](https://github.com/NuGet/Home/issues/4325)

- dotnet
  - dotnetcore Restore foo.sln - SLN 中的配置导致还原图中出现重复（但配置不同）项目时，此操作失败 - [#4316](https://github.com/NuGet/Home/issues/4316)

- 仅包含内容的包 - [#3668](https://github.com/NuGet/Home/issues/3668)

- 默认情况下，选择退出包格式选择器选项 - [#4468](https://github.com/NuGet/Home/issues/4468)

- 性能：CreateUAP_CSharp_VS.01.1.Create 项目使 Duration_TotalElapsedTime 回退了 3,153.570 毫秒 (149.1%)。 基线 26129.02 - [#4452](https://github.com/NuGet/Home/issues/4452)

- 性能：ManagedLangs_CS_DDRIT.0300.Rebuild 解决方案使 Duration_TotalElapsedTime 回退了 1.5 秒。 基线 26105 - [#4441](https://github.com/NuGet/Home/issues/4441)

- 多个 TFM 项目中出现提名失败 - [#4419](https://github.com/NuGet/Home/issues/4419)

- 性能：WebForms_DDRIT.1200.Close 解决方案使 VM_ImagesInMemory_Total_devenv 回退了 3.000 计数 (0.5%)。 基线 26123.04 - [#4408](https://github.com/NuGet/Home/issues/4408)

- vsfeedback - 面向 netcoreapp1.1 时出现包警告 - [#4397](https://github.com/NuGet/Home/issues/4397)

- 尝试将 NuGet 包添加到空 ASP.NET Core Web 应用程序中时，出现 PathTooLongException - [#4391](https://github.com/NuGet/Home/issues/4391)

- 包的运行过于频繁 -- dotnet
  - 目标依赖项关系图中存在涉及目标“包”的循环依赖时，dotnetcore 包失败 - [#4381](https://github.com/NuGet/Home/issues/4381)

- 包的运行过于频繁 - 生成 NuGet 包不包括所有配置 - [#4380](https://github.com/NuGet/Home/issues/4380)

- 使用 packageref 在 C++ 项目中添加 nuget 时，出现 NullReferenceException - [#4378](https://github.com/NuGet/Home/issues/4378)

- 辅助功能：讲述人不讲述用于选择要安装包的项目的复选框 - [#4366](https://github.com/NuGet/Home/issues/4366)

- NuGet VS17 偶尔无法连接到 VSO/VSTS 源 - VS Bug 365798 - [#4365](https://github.com/NuGet/Home/issues/4365)

- 如果 PackagePath 将路径指定为“contentFiles”，contentFiles 会输出到错误位置 - [#4348](https://github.com/NuGet/Home/issues/4348)

- 包目标将 VersionSuffix 追加到 PackageVersion 属性中 - [#4324](https://github.com/NuGet/Home/issues/4324)

- 指定包路径操作不适用于 dotnet 包 - [#4321](https://github.com/NuGet/Home/issues/4321)

- 在还原期间，NuGet 输出大量有关重复导入的警告 - [#4304](https://github.com/NuGet/Home/issues/4304)

- 在深色主题下，选择“NuGet 包管理器格式”对话框的显示不清晰 - [#4300](https://github.com/NuGet/Home/issues/4300)

- 生成还原时，VS 出现故障 - [#4298](https://github.com/NuGet/Home/issues/4298)

- 如果在 targetframeworks 中对 TFM 进行添加、保存和生成操作，Visual Studio 出现死锁。 10% 的时间 - [#4295](https://github.com/NuGet/Home/issues/4295)

- nuget 包不输出有关成功打包项目的成功消息 - [#4294](https://github.com/NuGet/Home/issues/4294)

- 由于找不到 System.IO.Compression 4.1，PackTask 失败 - [#4290](https://github.com/NuGet/Home/issues/4290)

- 包的运行过于频繁 - 由于文件访问冲突，PackTask 频繁失败 - [#4289](https://github.com/NuGet/Home/issues/4289)

- 在后台还原期间，NuGet 打开输出窗口 - [#4274](https://github.com/NuGet/Home/issues/4274)

- 将 ServiceProvider 作为危险编码模式删除（这可能导致挂起）- [#4268](https://github.com/NuGet/Home/issues/4268)

- 性能/UIHang - 改善 DownloadTimeoutStream 的读取 - [#4266](https://github.com/NuGet/Home/issues/4266)

- 若在完成 NuGet 还原之前尝试关闭项目，Visual Studio 出现死锁 - [#4257](https://github.com/NuGet/Home/issues/4257)

- 有关 PackTask 和打包 `.nuspec` 的问题 - [#4250](https://github.com/NuGet/Home/issues/4250)

- [vsfeedback] 无法在新项目上解析 nuget 包（需要重启 Visual Studio）- [#4217](https://github.com/NuGet/Home/issues/4217)

- [vsfeedback] 显示可用包版本的“版本”下拉列表难以与所选的 nuget 包同步... - [#4198](https://github.com/NuGet/Home/issues/4198)

- 与 CPS 交互时，Nuget.Client 应使用 CPS JoinableTaskFactory 以防止死锁 - [#4185](https://github.com/NuGet/Home/issues/4185)

- NuGet 3.5.0 不从包中解压缩 `.targets` - [#4171](https://github.com/NuGet/Home/issues/4171)

- dotnet
  - dotnetcore 包不支持 `.csproj` 中的标题 - [#4150](https://github.com/NuGet/Home/issues/4150)

- 安装包导致 VS2017 RC 中出现错误对话框 - [#4127](https://github.com/NuGet/Home/issues/4127)

- 针对 .net core 项目的更新包操作似乎不起作用，因为 UI 没有从提名中获取 CPS 更新。 - [#4035](https://github.com/NuGet/Home/issues/4035)

- 改进未解析的引用警告 - [#3955](https://github.com/NuGet/Home/issues/3955)

- dotnet
  - dotnetcore 包 - ProjectReference 丢失版本信息 - [#3953](https://github.com/NuGet/Home/issues/3953)

- 创建 UWP 应用、创建项目和重新生成的总运行时间回归 - [#3873](https://github.com/NuGet/Home/issues/3873)

- 尽管还原期间出现错误，仍显示成功还原消息。 - [#3799](https://github.com/NuGet/Home/issues/3799)

- 将 Nuget.CommandLine 3.4.4 重新发布到 Nuget.org - [# 2931](https://github.com/NuGet/Home/issues/2931)

- 在迁移期间，项目从 `project.json` 更改为 `.csproj` --- 还原失败 - [#4297](https://github.com/NuGet/Home/issues/4297)

- 在新创建的 xunit 测试项目上，还原失败 - [#4296](https://github.com/NuGet/Home/issues/4296)

- 核心项目可在打开状态下挂起和锁定 UI - [#4269](https://github.com/NuGet/Home/issues/4269)

- 修复生成任务的目标文件 - [#4267](https://github.com/NuGet/Home/issues/4267)

- 生成卸载引用的项目的解决方案后，错误列表中出现错误 - [#4208](https://github.com/NuGet/Home/issues/4208)

- MSB4057：项目中不存在目标“_GenerateRestoreGraphProjectEntry”。 - [#4194](https://github.com/NuGet/Home/issues/4194)

- vsfeedback：选择所有项目时，解决方案的 nuget 管理器 UI 出现故障 - [#4191](https://github.com/NuGet/Home/issues/4191)

- 存在尾随斜杠时，nuget.exe msbuildpath 失败 - [#4180](https://github.com/NuGet/Home/issues/4180)

- vsfeedback：NuGet 还原提供 LinqToTwitter 项目的多个项目引用警告 - [#4156](https://github.com/NuGet/Home/issues/4156)

- `.csproj` 的包不包括 minClientVersion 属性 - [#4135](https://github.com/NuGet/Home/issues/4135)

- 运送的 NuGet.Build.Tasks.Pack.dll 延迟了 VS2017 (d15rel 26014.00) 中的签名 - [#4122](https://github.com/NuGet/Home/issues/4122)

- VSFeedback：使用 CMake 3.7.1 生成的 VS 2015 项目的还原失败 - [#4114](https://github.com/NuGet/Home/issues/4114)

- VSFeedback：还原错误可能掩盖生成可提供的更完整的错误消息 - [#4113](https://github.com/NuGet/Home/issues/4113)

- [VSFeedback] 还原网站项目的 NuGet 包时出现错误：值不能为 Null。 - [#4092](https://github.com/NuGet/Home/issues/4092)

- 迁移在 NuGet.PackageManagement.VisualStudio.SolutionRestoreWorker 中引发“对象引用异常”- [#4067](https://github.com/NuGet/Home/issues/4067)

- dotnet
  - dotnetcore 包应使用生成包时所用的版本来打包工具 - [#4063](https://github.com/NuGet/Home/issues/4063)

- 还原需要花费数秒时，新的后台还原将毫秒写入状态栏 - [#4036](https://github.com/NuGet/Home/issues/4036)

- 由于拼写错误，未能解析所有项目引用 - [#4018](https://github.com/NuGet/Home/issues/4018)

- 在包引用方案中启用 PCM 工作流 - [#4016](https://github.com/NuGet/Home/issues/4016)

- 在包管理器 UI 中找不到已安装的包 - [#4015](https://github.com/NuGet/Home/issues/4015)

- dotnet
  - PackagePath 为空时，dotnetcore 包失败 - [#3993](https://github.com/NuGet/Home/issues/3993)

- 多用户方案中的还原任务失败 - [#3897](https://github.com/NuGet/Home/issues/3897)

- 使用 NuGet 包任务打包时，无法更改内容类型 - [#3895](https://github.com/NuGet/Home/issues/3895)

- 对于 MsBuild /t:pack，ContentFiles 的默认副本错误 - [#3894](https://github.com/NuGet/Home/issues/3894)

- 安装包还原将还原包的消息记录了两次 - [#3785](https://github.com/NuGet/Home/issues/3785)

- 删除 Guardrails - “运行时”部分的还原应仅应用于当前项目 - [#3768](https://github.com/NuGet/Home/issues/3768)

- 包任务在“content/”和“contentFiles/”中均放置了内容文件 - [#3718](https://github.com/NuGet/Home/issues/3718)

- dotnet
  - dotnetcore pack3 执行额外标记拆分操作 - [#3701](https://github.com/NuGet/Home/issues/3701)

- dotnet
  - dotnetcore 包：打包具有包引用的项目导致重复导入警告 - [#3665](https://github.com/NuGet/Home/issues/3665)

- VS 中并非始终显示还原日志记录 - [#3633](https://github.com/NuGet/Home/issues/3633)

- nuget 局部变量可帮助文本仍提到的包缓存 - [#3592](https://github.com/NuGet/Home/issues/3592)

- Restore3 将 PackageReferences 与 TargetFrameworks 结合。 - [#3504](https://github.com/NuGet/Home/issues/3504)

- 在 VS“15”Preview 4 dev. 命令提示符中， Nuget 选取意外的 MSBuild 版本 - [#3408](https://github.com/NuGet/Home/issues/3408)

- 还原失败时，写出目标/属性文件 - [#3399](https://github.com/NuGet/Home/issues/3399)

- 在 VS 15 命令提示符中运行时，还原期间的 NuGet 所遵循的兼容性填充码与 MSBuild 不同 - [#3387](https://github.com/NuGet/Home/issues/3387)

- 为 VS15 重新启用 PackFromProjectWithDevelopmentDependencySet - [#3272](https://github.com/NuGet/Home/issues/3272)

- NuGet 的 Blend 出现问题 - [#4043](https://github.com/NuGet/Home/issues/4043)

- 将 4.0.0.2067 集成到 CLI 和 SDK 存储库以与 RC2 共同传送 - [#4029](https://github.com/NuGet/Home/issues/4029)

- 创建新核心控制台应用、关闭解决方案、打开解决方案和关闭解决方案时，VS 挂起 - [#4008](https://github.com/NuGet/Home/issues/4008)

- 针对 d15prerel.25916.01 打开项目时，点击出现挂起 - [#3982](https://github.com/NuGet/Home/issues/3982)

- 修复 dotnet/nuget.exe 局部变量的 doc/help 消息 - [#3919](https://github.com/NuGet/Home/issues/3919)

- 检查 PackTask 是否存在尾随或前导空格的问题 - [#3906](https://github.com/NuGet/Home/issues/3906)

- dotnet
  - dotnetcore 包从 obj（而不是 bin）进行打包 - [#3880](https://github.com/NuGet/Home/issues/3880)

- dotnet
  - dotnetcore 包似乎始终将 ProjectReference 版本设置为 1.0.0 - [#3874](https://github.com/NuGet/Home/issues/3874)

- dotnet
  - 由于项目引用和 <TargetFramework>，dotnetcore 包失败 - [#3865](https://github.com/NuGet/Home/issues/3865)

- ProjectSystemCache.TryGetProjectNameByShortName 中的 LockRecursionException - [#3861](https://github.com/NuGet/Home/issues/3861)

- 删除 MSBuild 属性中的空格 - [#3819](https://github.com/NuGet/Home/issues/3819)

- 合并在项目加载上引发的两个项目事件 - [#3759](https://github.com/NuGet/Home/issues/3759)

- `project.assets.json` 文件中的 P2P 库版本不正确 - [#3748](https://github.com/NuGet/Home/issues/3748)

- 由于源无响应且包不可用，还原出现故障 - [#3672](https://github.com/NuGet/Home/issues/3672)

- 出现大量 MSBuild 错误输出时，nuget.exe 可能挂起 - [#3572](https://github.com/NuGet/Home/issues/3572)

- Blend 的 Restore-on-build 第一次失败，第二次成功（修复了 VS 方案）- [#2121](https://github.com/NuGet/Home/issues/2121)

### <a name="dcrs"></a>DCR

- 将 vsix 从 v2 vsix 迁移到 v3 vsix - [#4196](https://github.com/NuGet/Home/issues/4196)

- NuGet 应具有一个机制，该机制用于获取指向 MSBuild 中的锁定文件的路径 - [#3351](https://github.com/NuGet/Home/issues/3351)

- 将生成资产添加到 TFM 兼容性检查和资产文件 - [#3296](https://github.com/NuGet/Home/issues/3296)

- 在包目标中定义新的 ProjectCapability“包”，用于启用与包相关的功能 - [#4146](https://github.com/NuGet/Home/issues/4146)

- 以“GeneratePackageOnBuild”MSBuild 属性为条件，将包作为后期生成目标运行 - [#4145](https://github.com/NuGet/Home/issues/4145)

- 使用 NuGet 属性 RestoreProjectStyle 创建特定的 NuGet 项目 - [#4134](https://github.com/NuGet/Home/issues/4134)

- 为可传递的项目引用更改调整还原 - [#4076](https://github.com/NuGet/Home/issues/4076)

- 在非 UWP 项目的目标文件中添加 NuGet 属性 - [#4030](https://github.com/NuGet/Home/issues/4030)

- UWP TargetPlatformVersion 支持 - [#3923](https://github.com/NuGet/Home/issues/3923)

- 将项目引用元数据传达到 NuGet 项目系统 - [#3922](https://github.com/NuGet/Home/issues/3922)

- 针对打包模式添加 UI - [#3921](https://github.com/NuGet/Home/issues/3921)

- 旧版 `.csproj` 需要在项目/目标中设置 NugetTargetMoniker 和 RuntimeIdentifiers - [#3854](https://github.com/NuGet/Home/issues/3854)

- 安装包可能与自动还原重叠 - [#3836](https://github.com/NuGet/Home/issues/3836)

- 未加载 VSPackage 时，不会发生上下文菜单 QueryStatus - [#3835](https://github.com/NuGet/Home/issues/3835)

- 解决方案还原和生成还原时仍显示对话框 - [#3789](https://github.com/NuGet/Home/issues/3789)

- 在 NuGet.Clients 解决方案生成中隔离 VSSDK 版本 - [#3890](https://github.com/NuGet/Home/issues/3890)

## <a name="links-to-github-issues-fixed-in-rtm"></a>RTM 中已修复 GitHub 问题的链接
[问题列表 1](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RTM")  
[问题列表 2](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC4")  
[问题列表 3](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC3")  
[问题列表 4](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC2")  
[问题列表 5](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.0%20RC")
