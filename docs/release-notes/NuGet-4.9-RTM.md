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
# <a name="nuget-49-release-notes"></a><span data-ttu-id="dc536-103">NuGet 4.9 发行说明</span><span class="sxs-lookup"><span data-stu-id="dc536-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="dc536-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="dc536-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="dc536-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="dc536-105">NuGet version</span></span> | <span data-ttu-id="dc536-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="dc536-106">Available in Visual Studio version</span></span>| <span data-ttu-id="dc536-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="dc536-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="dc536-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="dc536-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="dc536-109">Visual Studio 2017 版本 15.9.0</span><span class="sxs-lookup"><span data-stu-id="dc536-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="dc536-110">2.1.500、2.2.100</span><span class="sxs-lookup"><span data-stu-id="dc536-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="dc536-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="dc536-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="dc536-112">n/a</span><span class="sxs-lookup"><span data-stu-id="dc536-112">n/a</span></span> | <span data-ttu-id="dc536-113">n/a</span><span class="sxs-lookup"><span data-stu-id="dc536-113">n/a</span></span> |
| [<span data-ttu-id="dc536-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="dc536-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="dc536-115">Visual Studio 2017 版本 15.9.4</span><span class="sxs-lookup"><span data-stu-id="dc536-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="dc536-116">2.1.502，2.2.101</span><span class="sxs-lookup"><span data-stu-id="dc536-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="dc536-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="dc536-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="dc536-118">Visual Studio 2017 版本 15.9.6</span><span class="sxs-lookup"><span data-stu-id="dc536-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="dc536-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="dc536-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="dc536-120">摘要:4.9.0 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="dc536-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="dc536-121">签名：允许 ClientPolicies 要求必须使用 NuGet.Config 中列出的一组受信任作者和存储库 - [#6961](https://github.com/NuGet/Home/issues/6961)，[博客文章](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="dc536-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="dc536-122">创建“.snupkg”文件以将符号包含在包中，即将 push 增强为了解 nuget 协议，以接受符号服务器的 snupkg 文件 - [#6878](https://github.com/NuGet/Home/issues/6878)，[博客文章](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="dc536-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="dc536-123">NuGet 凭据插件 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="dc536-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="dc536-124">独立式 NuGet 包 - 许可证 - [#4628](https://github.com/NuGet/Home/issues/4628)，[公告](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="dc536-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="dc536-125">支持选择对 PackageReference 启用“GeneratePathProperty”元数据，以将每个包的 MSBuild 属性生成到“Foo.Bar\1.0\" 目录中 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="dc536-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="dc536-126">改进了客户成功执行 NuGet 操作的体验 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="dc536-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="dc536-127">使用锁定文件启用可重复的包还原 - [#5602](https://github.com/NuGet/Home/issues/5602)，[公告](https://github.com/NuGet/Announcements/issues/28)，[博客文章](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="dc536-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dc536-128">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="dc536-128">Issues fixed in this release</span></span>

* <span data-ttu-id="dc536-129">（通过 WarnAsErrors）提升为 PackageExtraction 抛出的错误的警告绝不得留下已提取包 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="dc536-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="dc536-130">错误签名的包最终不得位于全局包文件夹中 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="dc536-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="dc536-131">绑定重定向生成不得跳过外观程序集 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="dc536-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="dc536-132">VersionRange Equals 不比较浮动范围 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="dc536-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="dc536-133">还原：使用新 .NET Core 2.1 HTTP 堆栈进行性能回归 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="dc536-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="dc536-134">包更新不得修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="dc536-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="dc536-135">签名：如果包内的条目太多 (> 65534)，签名应该会失败 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="dc536-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="dc536-136">“dotnet nuget push”代码路径应支持新凭据提供程序 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="dc536-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="dc536-137">支持执行具有固定区域性的插件（就像在 Docker 中一样）- [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="dc536-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="dc536-138">nuget sources add 不得从 NuGet.config 中删除凭据 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="dc536-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="dc536-139">devDependency PackageReference 安装应默认采用 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="dc536-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="dc536-140">将迁移程序选项修复为，在项目不兼容时对所有项目显示并显示错误 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="dc536-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="dc536-141">“dotnet add package”应提交对资产文件执行的还原 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="dc536-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="dc536-142">签名：改进了与错误消息相关的签名 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="dc536-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="dc536-143">[测试失败][zh-TW]字符串“包管理器控制台”在包管理器控制台中未本地化 - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="dc536-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="dc536-144">与“找不到项目信息”相关的错误消息应在 VS 中更具体一点 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="dc536-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="dc536-145">错误使用 nuget 包的 nuspec 版本标记时，错误消息毫无益处 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="dc536-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="dc536-146">DCR - 签名：支持 NuGet 协议：RepositorySignatures/4.9.0 资源 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="dc536-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="dc536-147">DCR - 现在 .nupkg.metadata 文件在包提取期间创建 - 包含“内容哈希”- [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="dc536-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="dc536-148">DCR - 在 Mono 上执行时，跳过插件的验证码验证 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="dc536-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="dc536-149">版本 4.9.0 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="dc536-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="dc536-150">摘要:4.9.1 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="dc536-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="dc536-151">现在支持通过新命令 trusted-signers 读取对 nuget.config 执行的写入操作 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="dc536-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dc536-152">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="dc536-152">Issues fixed in this release</span></span>

* <span data-ttu-id="dc536-153">修复了许可证链接生成 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="dc536-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="dc536-154">用于验证签名的错误代码回归 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="dc536-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="dc536-155">NuGet.Build.Tasks.Pack 包没有许可证信息 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="dc536-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="dc536-156">版本 4.9.1 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="dc536-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="dc536-157">摘要:4.9.2 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="dc536-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dc536-158">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="dc536-158">Issues fixed in this release</span></span>

* <span data-ttu-id="dc536-159">如果源名称包含空格，VS/dotnet.exe/nuget.exe/msbuild.exe 还原不使用凭据 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="dc536-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="dc536-160">LicenseAcceptanceWindow 和 LicenseFileWindow 辅助功能问题 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="dc536-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="dc536-161">修复 DateTimeConverter 中 DateTime.Parse 中的 FormatException -[#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="dc536-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="dc536-162">版本 4.9.2 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="dc536-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="dc536-163">摘要:4.9.3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="dc536-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dc536-164">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="dc536-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="dc536-165">“使用锁定文件启用可重复的包还原”问题</span><span class="sxs-lookup"><span data-stu-id="dc536-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="dc536-166">锁定模式不工作，因为未对以前缓存的包正确计算哈希 - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="dc536-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="dc536-167">还原解析为与 `packages.lock.json` 文件中定义的版本不同的版本 - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="dc536-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="dc536-168">涉及 ProjectReference 时，“--locked-mode / RestoreLockedMode”导致虚假的还原失败 - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="dc536-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="dc536-169">MSBuild SDK 解析程序尝试验证在使用 packages.lock.json 时未能还原的 SDK 包的 SHA - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="dc536-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="dc536-170">“使用可配置的信任策略锁定依赖关系”问题</span><span class="sxs-lookup"><span data-stu-id="dc536-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="dc536-171">dotnet.exe 不应在签名包不受支持时评估受信任的签名者 - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="dc536-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="dc536-172">配置文件中 trustedSigners 的顺序影响信任评估 - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="dc536-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="dc536-173">无法实现 ISettings [由设置 API 重构导致以支持信任策略功能] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="dc536-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="dc536-174">“提升了调试体验”问题</span><span class="sxs-lookup"><span data-stu-id="dc536-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="dc536-175">无法发布 .NET Core 全局工具的符号包 - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="dc536-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="dc536-176">“独立 NuGet 包 - 许可证”问题</span><span class="sxs-lookup"><span data-stu-id="dc536-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="dc536-177">使用嵌入的许可证文件时，生成符号 .snupkg 包出错 - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="dc536-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="dc536-178">版本 4.9.3 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="dc536-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")

## <a name="summary-whats-new-in-494"></a><span data-ttu-id="dc536-179">摘要:4.9.4 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="dc536-179">Summary: What's New in 4.9.4</span></span>

* <span data-ttu-id="dc536-180">安全修复：~/.nuget 中针对所创建文件的权限过于开放 [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="dc536-180">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>


## <a name="known-issues"></a><span data-ttu-id="dc536-181">已知问题</span><span class="sxs-lookup"><span data-stu-id="dc536-181">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519"></a><span data-ttu-id="dc536-182">dotnet nuget push --interactive 在 Mac 上抛出错误。</span><span class="sxs-lookup"><span data-stu-id="dc536-182">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="dc536-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="dc536-183"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="dc536-184">问题</span><span class="sxs-lookup"><span data-stu-id="dc536-184">Issue</span></span>
<span data-ttu-id="dc536-185">`--interactive` 参数无法由 dotnet cli 转发，因此导致错误 `error: Missing value for option 'interactive'` 出现</span><span class="sxs-lookup"><span data-stu-id="dc536-185">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="dc536-186">解决方法</span><span class="sxs-lookup"><span data-stu-id="dc536-186">Workaround</span></span>
<span data-ttu-id="dc536-187">将 interactive 选项与其他任何 dotnet 命令一起运行（如 `dotnet restore --interactive`），并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="dc536-187">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="dc536-188">凭据提供程序可能会缓存身份验证。</span><span class="sxs-lookup"><span data-stu-id="dc536-188">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="dc536-189">然后，运行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="dc536-189">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="dc536-190">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="dc536-190">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="dc536-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="dc536-191"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="dc536-192">问题</span><span class="sxs-lookup"><span data-stu-id="dc536-192">Issue</span></span>
<span data-ttu-id="dc536-193">使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。</span><span class="sxs-lookup"><span data-stu-id="dc536-193">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="dc536-194">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="dc536-194">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="dc536-195">解决方法</span><span class="sxs-lookup"><span data-stu-id="dc536-195">Workaround</span></span>
<span data-ttu-id="dc536-196">通过将 `RestoreAdditionalProjectSources` 设置为无，禁用回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="dc536-196">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="dc536-197">请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。</span><span class="sxs-lookup"><span data-stu-id="dc536-197">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
