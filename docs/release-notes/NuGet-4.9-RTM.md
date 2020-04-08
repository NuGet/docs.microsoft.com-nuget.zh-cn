---
title: NuGet 4.9 RTM 发行说明
description: NuGet 4.9 发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: e0dea74fe179c0dce4996f3e498185bb3a491856
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/07/2020
ms.locfileid: "64496467"
---
# <a name="nuget-49-release-notes"></a>NuGet 4.9 发行说明

NuGet 分发车辆：

| NuGet 版本 | 适用于 Visual Studio 版本| 适用于 .NET SDK|
|:---|:---|:---|
| [**4.9.0**](https://nuget.org/downloads) | [Visual Studio 2017 版本 15.9.0](https://visualstudio.microsoft.com/downloads/) | [2.1.500、2.2.100](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.1**](https://nuget.org/downloads) | n/a | n/a |
| [**4.9.2**](https://nuget.org/downloads) |[Visual Studio 2017 版本 15.9.4](https://visualstudio.microsoft.com/downloads/) | [2.1.502，2.2.101](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [**4.9.3**](https://nuget.org/downloads) |[Visual Studio 2017 版本 15.9.6](https://visualstudio.microsoft.com/downloads/) | [2.1.504, 2.2.104](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a>摘要:4.9.0 版中的新增功能

* 签名：允许 ClientPolicies 要求必须使用 NuGet.Config 中列出的一组受信任作者和存储库 - [#6961](https://github.com/NuGet/Home/issues/6961)，[博客文章](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)

* 创建“.snupkg”文件以将符号包含在包中，即将 push 增强为了解 nuget 协议，以接受符号服务器的 snupkg 文件 - [#6878](https://github.com/NuGet/Home/issues/6878)，[博客文章](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)

* NuGet 凭据插件 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)

* 独立式 NuGet 包 - 许可证 - [#4628](https://github.com/NuGet/Home/issues/4628)，[公告](https://github.com/NuGet/Announcements/issues/32)

* 支持选择对 PackageReference 启用“GeneratePathProperty”元数据，以将每个包的 MSBuild 属性生成到“Foo.Bar\1.0\" 目录中 - [#6949](https://github.com/NuGet/Home/issues/6949)

* 改进了客户成功执行 NuGet 操作的体验 - [#7108](https://github.com/NuGet/Home/issues/7108)

* 使用锁定文件启用可重复的包还原 - [#5602](https://github.com/NuGet/Home/issues/5602)，[公告](https://github.com/NuGet/Announcements/issues/28)，[博客文章](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

* （通过 WarnAsErrors）提升为 PackageExtraction 抛出的错误的警告绝不得留下已提取包 - [#7445](https://github.com/NuGet/Home/issues/7445)

* 错误签名的包最终不得位于全局包文件夹中 - [#7423](https://github.com/NuGet/Home/issues/7423)

* 绑定重定向生成不得跳过外观程序集 - [#7393](https://github.com/NuGet/Home/issues/7393)

* VersionRange Equals 不比较浮动范围 - [#7324](https://github.com/NuGet/Home/issues/7324)

* 还原：使用新 .NET Core 2.1 HTTP 堆栈进行性能回归 - [#7314](https://github.com/NuGet/Home/issues/7314)

* 包更新不得修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)

* 签名：如果包内的条目太多 (> 65534)，签名应该会失败 - [#7248](https://github.com/NuGet/Home/issues/7248)

* “dotnet nuget push”代码路径应支持新凭据提供程序 - [#7233](https://github.com/NuGet/Home/issues/7233)

* 支持执行具有固定区域性的插件（就像在 Docker 中一样）- [#7223](https://github.com/NuGet/Home/issues/7223)

* nuget sources add 不得从 NuGet.config 中删除凭据 - [#7200](https://github.com/NuGet/Home/issues/7200)

* devDependency PackageReference 安装应默认采用 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)

* 将迁移程序选项修复为，在项目不兼容时对所有项目显示并显示错误 - [#6958](https://github.com/NuGet/Home/issues/6958)

* “dotnet add package”应提交对资产文件执行的还原 - [#6928](https://github.com/NuGet/Home/issues/6928)

* 签名：改进了与错误消息相关的签名 - [#6906](https://github.com/NuGet/Home/issues/6906)

* [测试失败][zh-TW]字符串“包管理器控制台”在包管理器控制台中未本地化 - [#6381](https://github.com/NuGet/Home/issues/6381)

* 与“找不到项目信息”相关的错误消息应在 VS 中更具体一点 - [#5350](https://github.com/NuGet/Home/issues/5350)

* 错误使用 nuget 包的 nuspec 版本标记时，错误消息毫无益处 - [#2714](https://github.com/NuGet/Home/issues/2714)

* DCR - 签名：支持 NuGet 协议：RepositorySignatures/4.9.0 资源 - [#7421](https://github.com/NuGet/Home/issues/7421)

* DCR - 现在 .nupkg.metadata 文件在包提取期间创建 - 包含“内容哈希”- [#7283](https://github.com/NuGet/Home/issues/7283)

* DCR - 在 Mono 上执行时，跳过插件的验证码验证 - [#7222](https://github.com/NuGet/Home/issues/7222)

[版本 4.9.0 中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a>摘要:4.9.1 版中的新增功能

* 现在支持通过新命令 trusted-signers 读取对 nuget.config 执行的写入操作 - [#7480](https://github.com/NuGet/Home/issues/7480)

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

* 修复了许可证链接生成 - [#7515](https://github.com/NuGet/Home/issues/7515)

* 用于验证签名的错误代码回归 - [#7492](https://github.com/NuGet/Home/issues/7492)

* NuGet.Build.Tasks.Pack 包没有许可证信息 - [#7379](https://github.com/NuGet/Home/issues/7379)

[版本 4.9.1 中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a>摘要:4.9.2 版中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题

* 如果源名称包含空格，VS/dotnet.exe/nuget.exe/msbuild.exe 还原不使用凭据 - [#7517](https://github.com/NuGet/Home/issues/7517)

* LicenseAcceptanceWindow 和 LicenseFileWindow 辅助功能问题 - [#7452](https://github.com/NuGet/Home/issues/7452)

* 修复 DateTimeConverter 中 DateTime.Parse 中的 FormatException -[#7539](https://github.com/NuGet/Home/issues/7539)

[版本 4.9.2 中所有已修复问题的列表](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a>摘要:4.9.3 中的新增功能

### <a name="issues-fixed-in-this-release"></a>此版本中已修复的问题
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a>“使用锁定文件启用可重复的包还原”问题

* 锁定模式不工作，因为未对以前缓存的包正确计算哈希 - [#7682](https://github.com/NuGet/Home/issues/7682)

* 还原解析为与 `packages.lock.json` 文件中定义的版本不同的版本 - [#7667](https://github.com/NuGet/Home/issues/7667)

* 涉及 ProjectReference 时，“--locked-mode / RestoreLockedMode”导致虚假的还原失败 - [#7646](https://github.com/NuGet/Home/issues/7646)

* MSBuild SDK 解析程序尝试验证在使用 packages.lock.json 时未能还原的 SDK 包的 SHA - [#7599](https://github.com/NuGet/Home/issues/7599)

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a>“使用可配置的信任策略锁定依赖关系”问题
* dotnet.exe 不应在签名包不受支持时评估受信任的签名者 - [#7574](https://github.com/NuGet/Home/issues/7574)

* 配置文件中 trustedSigners 的顺序影响信任评估 - [#7572](https://github.com/NuGet/Home/issues/7572)

* 无法实现 ISettings [由设置 API 重构导致以支持信任策略功能] - [#7614](https://github.com/NuGet/Home/issues/7614)

#### <a name="improved-debugging-experience-issues"></a>“提升了调试体验”问题

* 无法发布 .NET Core 全局工具的符号包 - [#7632](https://github.com/NuGet/Home/issues/7632)

#### <a name="self-contained-nuget-packages---license-issues"></a>“独立 NuGet 包 - 许可证”问题

* 使用嵌入的许可证文件时，生成符号 .snupkg 包出错 - [#7591](https://github.com/NuGet/Home/issues/7591)

[版本 4.9.3 中所有已修复问题的列表](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a>摘要:4.9.4 版中的新增功能

* 安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)


## <a name="known-issues"></a>已知问题

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a>dotnet nuget push --interactive 在 Mac 上抛出错误。 - [#7519](https://github.com/NuGet/Home/issues/7519)

#### <a name="issue"></a>问题
`--interactive` 参数无法由 dotnet cli 转发，因此导致错误 `error: Missing value for option 'interactive'` 出现

#### <a name="workaround"></a>解决方法
将 interactive 选项与其他任何 dotnet 命令一起运行（如 `dotnet restore --interactive`），并进行身份验证。 凭据提供程序可能会缓存身份验证。 然后，运行 `dotnet nuget push`。

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a>FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。 - [#7414](https://github.com/NuGet/Home/issues/7414)

#### <a name="issue"></a>问题
使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。 也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。

#### <a name="workaround"></a>解决方法
通过将 `RestoreAdditionalProjectSources` 设置为无，禁用回退文件夹。 请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。
