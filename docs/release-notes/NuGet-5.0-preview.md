---
title: NuGet 5.0 预览版发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 预览版的发行说明。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247654"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="27326-103">NuGet 5.0 预览版发行说明</span><span class="sxs-lookup"><span data-stu-id="27326-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="27326-104">NuGet 5.0 预览版本</span><span class="sxs-lookup"><span data-stu-id="27326-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="27326-105">2019 年 2 月 13 日- [NuGet 5.0 预览版 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="27326-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="27326-106">2019 年 1 月 23 日- [NuGet 5.0 预览版 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="27326-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="27326-107">摘要:什么是 NuGet 5.0 预览版 3 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="27326-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27326-108">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="27326-108">Issues fixed in this release</span></span> 

<span data-ttu-id="27326-109">**Bug:**</span><span class="sxs-lookup"><span data-stu-id="27326-109">**Bugs:**</span></span>

* <span data-ttu-id="27326-110">nuget.exe /?</span><span class="sxs-lookup"><span data-stu-id="27326-110">nuget.exe /?</span></span> <span data-ttu-id="27326-111">应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="27326-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="27326-112">NuGet.targets(498,5)： 错误：找不到部分路径 / tmp/NuGetScratch-mono-上[#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="27326-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="27326-113">还原不必要地枚举在计算机缓存中的引用包的所有版本的内容[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="27326-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="27326-114">MSBuild 自动检测后安装与 2019年预览-始终选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="27326-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="27326-115">一种解决方案上的 dotnet 列表包输出的框架的重复条目[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="27326-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="27326-116">异常"空路径名称不是合法的"时调用 IVsPackageInstaller.InstallPackage 上旧项目和包文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="27326-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="27326-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="27326-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="27326-118">msbuild /t: restore 最低详细级别应为更少的[#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="27326-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="27326-119">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="27326-119">**DCRs**</span></span>

* <span data-ttu-id="27326-120">允许程序包作者可定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="27326-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="27326-121">启用在 VS 成功如果项目不是解决方案的一部分或未加载，但以前已还原的还原[#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="27326-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="27326-122">摘要:什么是 5.0 预览版 2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="27326-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="27326-123">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="27326-123">Issues fixed in this release</span></span>

<span data-ttu-id="27326-124">**Bug:**</span><span class="sxs-lookup"><span data-stu-id="27326-124">**Bugs:**</span></span>

* <span data-ttu-id="27326-125">VS 16.0 的 NuGet UI 具有不可读的选项卡颜色问题-由于[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="27326-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="27326-126">NuGet.Core 和 NuGet.Clients License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="27326-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="27326-127">还原不必要地枚举全局包文件夹中尝试确定类型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="27326-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="27326-128">从锁定文件强制错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="27326-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="27326-129">修复 NuGet.Configuration 问题- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="27326-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="27326-130">适应 MSBuild 更新的安装位置。</span><span class="sxs-lookup"><span data-stu-id="27326-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="27326-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="27326-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="27326-132">NuGet.Build.Tasks.Pack 应该是开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="27326-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="27326-133">添加包扩展点包括调试符号的[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="27326-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="27326-134">dotnet 包应保留在创建 nupkg 的依赖项版本范围。</span><span class="sxs-lookup"><span data-stu-id="27326-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="27326-135">（即使使用浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="27326-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="27326-136">用户级配置还具有源-已经过身份验证源失败 dotnet 还原[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="27326-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="27326-137">包不应限制的内容文件-BuildActions 套[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="27326-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="27326-138">使用 projectreference，这要求 AssetTargetFallback 成功，应发出警告。</span><span class="sxs-lookup"><span data-stu-id="27326-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="27326-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="27326-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="27326-140">由于线程问题到 CPS (CommonProjectSystem) 的调用时的死锁[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="27326-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="27326-141">dotnet 添加包不会用于本地配置-中指定的源的凭据从全局配置[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="27326-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="27326-142">线程处理问题与 MEF 正在调用异步代码- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="27326-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="27326-143">签名： 报告两次，而无需调用堆栈的错误[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="27326-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="27326-144">使用不受信任的签名证书安装已签名的包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="27326-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="27326-145">NuGet 还原不正确 Noop 当 2 个项目共享 obj 目录- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="27326-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="27326-146">使用 Linux 上使用已经过身份验证源-中的包的 dotnet 还原不能使用 PAT [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="27326-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="27326-147">dotnet 还原由于已禁用计算机范围源-而失败[#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="27326-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="27326-148">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="27326-148">**DCRs**</span></span>

* <span data-ttu-id="27326-149">NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="27326-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="27326-150">从 NuGet.Packaging NuGetLicenseData 应为公共类型。</span><span class="sxs-lookup"><span data-stu-id="27326-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="27326-151">更新许可证元数据从 spdx 引入。</span><span class="sxs-lookup"><span data-stu-id="27326-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="27326-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="27326-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="27326-153">删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="27326-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="27326-154">解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="27326-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="27326-155">NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="27326-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="27326-156">Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="27326-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="27326-157">在此版本 5.0.0-preview2 中修复所有问题的列表</span><span class="sxs-lookup"><span data-stu-id="27326-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="27326-158">已知问题</span><span class="sxs-lookup"><span data-stu-id="27326-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="27326-159">dotnet nuget push --interactive 在 Mac 上抛出错误。</span><span class="sxs-lookup"><span data-stu-id="27326-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="27326-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="27326-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="27326-161">**问题**`--interactive`自变量不转发 dotnet cli，并且会导致错误`error: Missing value for option 'interactive'` 
**解决方法**使用如交互式选项运行任何其他dotnet命令`dotnet restore --interactive`并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="27326-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="27326-162">凭据提供程序可能会缓存身份验证。</span><span class="sxs-lookup"><span data-stu-id="27326-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="27326-163">然后，运行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="27326-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="27326-164">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="27326-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="27326-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="27326-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="27326-166">**问题**使用 dotnet.exe 时 2.x 以还原项目的多重目标 netcoreapp 1.x 和 netcoreapp 2.x，回退文件夹视为文件源。</span><span class="sxs-lookup"><span data-stu-id="27326-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="27326-167">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="27326-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="27326-168">**解决方法**通过设置来禁用回退文件夹的使用情况`RestoreAdditionalProjectSources`为 nothing。</span><span class="sxs-lookup"><span data-stu-id="27326-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="27326-169">请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。</span><span class="sxs-lookup"><span data-stu-id="27326-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
