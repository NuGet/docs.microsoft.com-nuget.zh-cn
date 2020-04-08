---
title: NuGet 4.8 RTM 发行说明
description: NuGet 4.8.1 的发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: e6f6d9f703dd4761236d166f3772618c100aca09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "76813762"
---
# <a name="nuget-48-release-notes"></a>NuGet 4.8 发行说明

[Visual Studio 2017 15.8 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 附带 NuGet 4.8 功能。


此外提供了相同功能的命令行版本：
* NuGet.exe 4.8 - [nuget.org/downloads](https://nuget.org/downloads)
* DotNet.exe - [.NET Core SDK 2.1.400](https://www.microsoft.com/net/download/visual-studio-sdks)


## <a name="summary-whats-new-in-480"></a>摘要:4.8.0 版中的新增功能
* NuGet.exe 现支持 Windows 10 上的 longfilenames - [#6937](https://github.com/NuGet/Home/issues/6937)
* 身份验证插件现适用于 MsBuild、DotNet.exe、NuGet.exe 和 Visual Studio（包括跨平台使用）。 MsBuild 的 DotNet.exe 中不支持第一代身份验证插件。 注意：VS 2017 15.9 预览内部版本包含 VSTS 身份验证插件。 [#6486](https://github.com/NuGet/Home/issues/6486)
* MsBuild 的 SDK 解析程序现作为 NuGet 的一部分生成，并通过 VS 的 NuGet 工具安装。 这将避免版本无法同步的问题。[#6799](https://github.com/NuGet/Home/issues/6799)
* PackageReference 现支持 DevelopmentDependency 元数据 - [#4125](https://github.com/NuGet/Home/issues/4125)

## <a name="summary-whats-new-in-482"></a>摘要:4.8.2 版中的新增功能

* 安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)

## <a name="known-issues"></a>已知问题
### <a name="installing-signed-packages-on-a-ci-machine-or-in-an-offline-environment-takes-longer-than-usual"></a>在 CI 计算机或在脱机环境中安装签名包所需的时间要比平常长

#### <a name="issue"></a>问题
如果计算机的 Internet 访问受限（如 CI/CD 方案中的生成计算机），安装/还原签名的 nuget 包将导致警告 ([NU3028](../reference/errors-and-warnings/nu3028.md))，因为吊销服务器不可访问。 这是预期情况。 但是，在某些情况下，这可能会产生意外的结果，如安装/还原包花费的时间比平常长。

#### <a name="workaround"></a>解决方法
更新到 Visual Studio 15.8.4 和 NuGet.exe 4.8.1，我们在其中引入了一个环境变量来切换吊销检查模式。
将 `NUGET_CERT_REVOCATION_MODE` 环境变量设置为 `offline` 将迫使 NuGet 仅针对缓存证书吊销列表检查证书吊销状态，NuGet 不会尝试访问吊销服务器。 如果吊销检查模式设置为 `offline`，警告将降级为信息。

> [!Warning]
> 不建议在正常情况下将吊销检查模式切换到脱机。 执行此操作将导致 NuGet 跳过联机吊销检查，并只对可能过期的缓存证书吊销列表执行脱机吊销检查。 这意味着将继续安装/还原签名证书可能已经吊销的包，否则吊销检查将失败，并且不会安装。

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a>`Migrate packages.config to PackageReference...` 选项在右键单击上下文菜单中不可用

#### <a name="issue"></a>问题

首次打开项目时，在执行 NuGet 操作之前，NuGet 可能不会进行初始化。 这将导致迁移选项不会显示在 `packages.config` 或 `References` 的右键单击上下文菜单中。

#### <a name="workaround"></a>解决方法

执行以下 NuGet 操作之一：
* 打开包管理器 UI - 右键单击 `References` 并选择 `Manage NuGet Packages...`
* 打开“包管理器控制台” - 从 `Tools > NuGet Package Manager` 中选择 `Package Manager Console`
* 运行 NuGet 还原 - 在“解决方案资源管理器”中，右键单击该解决方案节点，然后选择 `Restore NuGet Packages`
* 生成还会触发 NuGet 还原的项目

现在应能够看到迁移选项。 请注意，此选项不受支持且不会对 ASP.NET 和 C++ 项目类型显示。
注意：此问题已在 VS 2017 15.9 预览版 3 中修复

## <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

### <a name="bugs"></a>Bug
#### <a name="signing"></a>签名
* 签名：在脱机环境中安装签名包 [#7008](https://github.com/NuGet/Home/issues/7008) -- 已在 4.8.1 中修复
* 签名：不正确的 URL 检查 - [#7174](https://github.com/NuGet/Home/issues/7174)
* 签名：当包是存储库副署包时，检查 RepositorySignatureVerifier 中包的完整性 - [#6926](https://github.com/NuGet/Home/issues/6926)
* “包完整性检查失败。” 消息中应具有包 ID（和错误代码） - [#6944](https://github.com/NuGet/Home/issues/6944)
* 存储库签名包验证允许由不同证书对包进行签名 - [#6884](https://github.com/NuGet/Home/issues/6884)
* NuGet - 签名 - 时间戳 URL 不能是 https:// ? - [#6871](https://github.com/NuGet/Home/issues/6871)
* 不要在 NuSpec 封装方案中使用 NULL 引用，还可以改进选项 - [#6866](https://github.com/NuGet/Home/issues/6866)
* 如果将时间戳添加到副署，更新签名者信息时内存无效 - [#6840](https://github.com/NuGet/Home/issues/6840)
* 签名：删除 CTL 异常 - [#6794](https://github.com/NuGet/Home/issues/6794)
* 签名：contentUrl 必须是 HTTPS - [#6777](https://github.com/NuGet/Home/issues/6777)
* 签名：未使用 SignedPackageVerifierSettings.VSClientDefaultPolicy - [#6601](https://github.com/NuGet/Home/issues/6601)


#### <a name="pack"></a>打包
* 使用 dotnet.exe 打包 nuspec 时不需要还原和生成 - [#6866](https://github.com/NuGet/Home/issues/6866)
* 允许在 NuspecProperties中使用空的替换令牌 - [#6722](https://github.com/NuGet/Home/issues/6722)
* 当指定 NuspecProperties 时，PackTask 将引发 NullReferenceException - [#4649](https://github.com/NuGet/Home/issues/4649)

#### <a name="accessibility"></a>可访问性
* [可访问性]包按钮下的字符串“预发行版”在 PM UI 中被包描述覆盖 - [#4504](https://github.com/NuGet/Home/issues/4504)
* [可访问性]当选择 PM UI 中的“Microsoft Visual Studio 脱机包”时，包源下拉列表和设置按钮被截断 - [#4502](https://github.com/NuGet/Home/issues/4502)

#### <a name="powershell-management-console-pmc"></a>Powershell 管理控制台 (PMC)
* `Update-Package` 忽略 PackageReference 版本范围 - [#6775](https://github.com/NuGet/Home/issues/6775)
* `Update-Package -reinstall` 解决方案级别的问题 - [#3127](https://github.com/NuGet/Home/issues/3127)
* `Update-Package [packagename] -reinstall` 重新安装所有包，而不仅仅是指定包 - [#737](https://github.com/NuGet/Home/issues/737)
* 可以从包管理器控制台中更新到未列出的 NuGet 包 - [#4553](https://github.com/NuGet/Home/issues/4553)

#### <a name="misc"></a>杂项
* 若要修复 `NuGet update self`，NuGet.Commandline nupkg 不应为 semver2.0 - [#7116](https://github.com/NuGet/Home/issues/7116)
* 改进 NU1107 安装失败的体验 - [#7107](https://github.com/NuGet/Home/issues/7107)
* GetAuthenticationCredentialRequest 的序列化不正确 - [#6983](https://github.com/NuGet/Home/issues/6983)
* 关闭 UI 线程初始化时 NuGet Visual Studio AsyncPackage 加载失败 - [#6976](https://github.com/NuGet/Home/issues/6976)
* 还原操作报告误导性错误，指示不需要 project.json - [#6959](https://github.com/NuGet/Home/issues/6959)
* 包管理器 UI：预览更改，“确定”按钮不可自动通过键盘使用 - [#6893](https://github.com/NuGet/Home/issues/6893)
* 对于使用 p2p 引用的项目，会忽略 RestoreSources - [#6776](https://github.com/NuGet/Home/issues/6776)
* 使用 .NET Framework 模板创建单元测试项目将使用 packages.config 打开较旧的项目模型 - [#6736](https://github.com/NuGet/Home/issues/6736)
* 允许项目引用重写包依赖项 - [#6536](https://github.com/NuGet/Home/issues/6536)
* 在 MSBuild 任务中公开 NoDefaultExcludes - [#6450](https://github.com/NuGet/Home/issues/6450)
* 调整窗口大小时，可以隐藏“清除所有 NuGet 缓存”的状态消息 - [#5938](https://github.com/NuGet/Home/issues/5938)


[此版本中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.8")
