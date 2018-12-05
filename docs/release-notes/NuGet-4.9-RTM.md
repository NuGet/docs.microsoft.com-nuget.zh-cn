---
title: NuGet 4.9 RTM 发行说明
description: NuGet 4.9 发行说明，包括已知问题、bug 修复、新增功能和 DCR。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453767"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="3c60b-103">NuGet 4.9 发行说明</span><span class="sxs-lookup"><span data-stu-id="3c60b-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="3c60b-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) 随附 NuGet 4.9.0 功能。</span><span class="sxs-lookup"><span data-stu-id="3c60b-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="3c60b-105">此外提供了相同功能的命令行版本：</span><span class="sxs-lookup"><span data-stu-id="3c60b-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="3c60b-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="3c60b-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="3c60b-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="3c60b-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="3c60b-108">摘要：4.9.0 中的新变化</span><span class="sxs-lookup"><span data-stu-id="3c60b-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="3c60b-109">签名：允许 ClientPolicies 要求必须使用 NuGet.Config 中列出的一组受信任作者和存储库 - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="3c60b-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="3c60b-110">创建“.snupkg”文件以将符号包含在包中，即将 push 增强为了解 nuget 协议，以接受符号服务器的 snupkg 文件 - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="3c60b-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="3c60b-111">NuGet 凭据插件 V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="3c60b-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="3c60b-112">独立式 NuGet 包 - 许可证 - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="3c60b-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="3c60b-113">支持选择对 PackageReference 启用“GeneratePathProperty”元数据，以将每个包的 MSBuild 属性生成到“Foo.Bar\1.0”目录中 - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="3c60b-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="3c60b-114">改进了客户成功执行 NuGet 操作的体验 - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="3c60b-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3c60b-115">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-115">Issues fixed in this release</span></span>

* <span data-ttu-id="3c60b-116">（通过 WarnAsErrors）提升为 PackageExtraction 抛出的错误的警告绝不得留下已提取包 - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="3c60b-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="3c60b-117">错误签名的包最终不得位于全局包文件夹中 - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="3c60b-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="3c60b-118">绑定重定向生成不得跳过外观程序集 - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="3c60b-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="3c60b-119">VersionRange Equals 不比较浮动范围 - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="3c60b-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="3c60b-120">还原：使用新 .NET Core 2.1 HTTP 堆栈进行性能回归 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="3c60b-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="3c60b-121">包更新不得修改 PackageReference 的 PrivateAssets - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="3c60b-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="3c60b-122">签名：如果包内的条目太多 (> 65534)，签名应该会失败 - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="3c60b-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="3c60b-123">“dotnet nuget push”代码路径应支持新凭据提供程序 - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="3c60b-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="3c60b-124">支持执行具有固定区域性的插件（就像在 Docker 中一样）- [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="3c60b-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="3c60b-125">nuget sources add 不得从 NuGet.config 中删除凭据 - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="3c60b-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="3c60b-126">devDependency PackageReference 安装应默认采用 excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="3c60b-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="3c60b-127">将迁移程序选项修复为，在项目不兼容时对所有项目显示并显示错误 - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="3c60b-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="3c60b-128">“dotnet add package”应提交对资产文件执行的还原 - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="3c60b-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="3c60b-129">签名：改进了与错误消息相关的签名 - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="3c60b-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="3c60b-130">[测试失败][zh-TW]字符串“包管理器控制台”在包管理器控制台中未本地化 - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="3c60b-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="3c60b-131">与“找不到项目信息”相关的错误消息应在 VS 中更具体一点 - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="3c60b-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="3c60b-132">错误使用 nuget 包的 nuspec 版本标记时，错误消息毫无益处 - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="3c60b-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="3c60b-133">DCR - 签名：支持 NuGet 协议：RepositorySignatures/4.9.0 资源 - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="3c60b-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="3c60b-134">DCR - 现在 .nupkg.metadata 文件在包提取期间创建 - 包含“内容哈希”- [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="3c60b-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="3c60b-135">DCR - 在 Mono 上执行时，跳过插件的验证码验证 - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="3c60b-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="3c60b-136">版本 4.9.0 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="3c60b-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="3c60b-137">摘要：4.9.1 中的新变化</span><span class="sxs-lookup"><span data-stu-id="3c60b-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="3c60b-138">现在支持通过新命令 trusted-signers 读取对 nuget.config 执行的写入操作 - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="3c60b-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3c60b-139">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-139">Issues fixed in this release</span></span>

* <span data-ttu-id="3c60b-140">修复了许可证链接生成 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="3c60b-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="3c60b-141">用于验证签名的错误代码回归 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="3c60b-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="3c60b-142">NuGet.Build.Tasks.Pack 包没有许可证信息 - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="3c60b-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="3c60b-143">版本 4.9.1 中所有已修复问题的列表</span><span class="sxs-lookup"><span data-stu-id="3c60b-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="3c60b-144">已知问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="3c60b-145">如果源名称包含空格，dotnet.exe/nuget.exe 不使用凭据 - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="3c60b-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="3c60b-146">问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-146">Issue</span></span>
<span data-ttu-id="3c60b-147">如果源名称中有空格，nuget.exe 会抛出错误，如 `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span><span class="sxs-lookup"><span data-stu-id="3c60b-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c60b-148">解决方法</span><span class="sxs-lookup"><span data-stu-id="3c60b-148">Workaround</span></span>
<span data-ttu-id="3c60b-149">将源名称更改为不包含空格。</span><span class="sxs-lookup"><span data-stu-id="3c60b-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="3c60b-150">dotnet nuget push --interactive 在 Mac 上抛出错误。</span><span class="sxs-lookup"><span data-stu-id="3c60b-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="3c60b-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="3c60b-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="3c60b-152">问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-152">Issue</span></span>
<span data-ttu-id="3c60b-153">`--interactive` 参数无法由 dotnet cli 转发，因此导致错误 `error: Missing value for option 'interactive'` 出现</span><span class="sxs-lookup"><span data-stu-id="3c60b-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c60b-154">解决方法</span><span class="sxs-lookup"><span data-stu-id="3c60b-154">Workaround</span></span>
<span data-ttu-id="3c60b-155">将 interactive 选项与其他任何 dotnet 命令一起运行（如 `dotnet restore --interactive`），并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="3c60b-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="3c60b-156">凭据提供程序可能会缓存身份验证。</span><span class="sxs-lookup"><span data-stu-id="3c60b-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="3c60b-157">然后，运行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="3c60b-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="3c60b-158">LicenseAcceptanceWindow 和 LicenseFileWindow 辅助功能问题 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="3c60b-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="3c60b-159">问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-159">Issue</span></span>
<span data-ttu-id="3c60b-160">许可证接受窗口和许可证文件窗口存在辅助功能问题，不支持键盘导航和使用屏幕阅读器和 JAWS 提供旁白。</span><span class="sxs-lookup"><span data-stu-id="3c60b-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c60b-161">解决方法</span><span class="sxs-lookup"><span data-stu-id="3c60b-161">Workaround</span></span>
<span data-ttu-id="3c60b-162">无解决方法。</span><span class="sxs-lookup"><span data-stu-id="3c60b-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="3c60b-163">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="3c60b-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="3c60b-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="3c60b-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="3c60b-165">问题</span><span class="sxs-lookup"><span data-stu-id="3c60b-165">Issue</span></span>
<span data-ttu-id="3c60b-166">使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。</span><span class="sxs-lookup"><span data-stu-id="3c60b-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="3c60b-167">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="3c60b-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="3c60b-168">解决方法</span><span class="sxs-lookup"><span data-stu-id="3c60b-168">Workaround</span></span>
<span data-ttu-id="3c60b-169">通过将 `RestoreAdditionalProjectSources` 设置为无，禁用回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="3c60b-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="3c60b-170">请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。</span><span class="sxs-lookup"><span data-stu-id="3c60b-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
