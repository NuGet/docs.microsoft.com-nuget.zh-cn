---
title: NuGet 5.0 预览版发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 预览版的发行说明。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084933"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="a6e14-103">NuGet 5.0 预览版发行说明</span><span class="sxs-lookup"><span data-stu-id="a6e14-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="a6e14-104">摘要:什么是 5.0 预览版 2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a6e14-104">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a6e14-105">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="a6e14-105">Issues fixed in this release</span></span>

#### <a name="bugs"></a><span data-ttu-id="a6e14-106">Bug:</span><span class="sxs-lookup"><span data-stu-id="a6e14-106">Bugs:</span></span>

* <span data-ttu-id="a6e14-107">VS 16.0 的 NuGet UI 具有不可读的选项卡颜色问题-由于[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="a6e14-107">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="a6e14-108">NuGet.Core 和 NuGet.Clients License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="a6e14-108">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="a6e14-109">还原不必要地枚举全局包文件夹中尝试确定类型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="a6e14-109">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="a6e14-110">从锁定文件强制错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="a6e14-110">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="a6e14-111">修复 NuGet.Configuration 问题- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="a6e14-111">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="a6e14-112">适应 MSBuild 更新的安装位置。</span><span class="sxs-lookup"><span data-stu-id="a6e14-112">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="a6e14-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="a6e14-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="a6e14-114">NuGet.Build.Tasks.Pack 应该是开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="a6e14-114">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="a6e14-115">添加包扩展点包括调试符号的[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="a6e14-115">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="a6e14-116">dotnet 包应保留在创建 nupkg 的依赖项版本范围。</span><span class="sxs-lookup"><span data-stu-id="a6e14-116">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="a6e14-117">（即使使用浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="a6e14-117">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="a6e14-118">用户级配置还具有源-已经过身份验证源失败 dotnet 还原[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="a6e14-118">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="a6e14-119">包不应限制的内容文件-BuildActions 套[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="a6e14-119">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="a6e14-120">使用 projectreference，这要求 AssetTargetFallback 成功，应发出警告。</span><span class="sxs-lookup"><span data-stu-id="a6e14-120">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="a6e14-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="a6e14-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="a6e14-122">由于线程问题到 CPS (CommonProjectSystem) 的调用时的死锁[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="a6e14-122">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="a6e14-123">dotnet 添加包不会用于本地配置-中指定的源的凭据从全局配置[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="a6e14-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="a6e14-124">线程处理问题与 MEF 正在调用异步代码- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="a6e14-124">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="a6e14-125">签名： 报告两次，而无需调用堆栈的错误[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="a6e14-125">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="a6e14-126">使用不受信任的签名证书安装已签名的包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="a6e14-126">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="a6e14-127">NuGet 还原不正确 Noop 当 2 个项目共享 obj 目录- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="a6e14-127">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="a6e14-128">使用 Linux 上使用已经过身份验证源-中的包的 dotnet 还原不能使用 PAT [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="a6e14-128">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="a6e14-129">dotnet 还原由于已禁用计算机范围源-而失败[#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="a6e14-129">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

#### <a name="dcrs"></a><span data-ttu-id="a6e14-130">DCR</span><span class="sxs-lookup"><span data-stu-id="a6e14-130">DCRs</span></span>

* <span data-ttu-id="a6e14-131">NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="a6e14-131">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="a6e14-132">从 NuGet.Packaging NuGetLicenseData 应为公共类型。</span><span class="sxs-lookup"><span data-stu-id="a6e14-132">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="a6e14-133">更新许可证元数据从 spdx 引入。</span><span class="sxs-lookup"><span data-stu-id="a6e14-133">Update license metadata ingested from spdx.</span></span><span data-ttu-id="a6e14-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="a6e14-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="a6e14-135">删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="a6e14-135">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="a6e14-136">解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="a6e14-136">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="a6e14-137">NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="a6e14-137">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="a6e14-138">Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="a6e14-138">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="a6e14-139">在此版本 5.0.0-preview2 中修复所有问题的列表</span><span class="sxs-lookup"><span data-stu-id="a6e14-139">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a><span data-ttu-id="a6e14-140">已知问题</span><span class="sxs-lookup"><span data-stu-id="a6e14-140">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="a6e14-141">dotnet nuget push --interactive 在 Mac 上抛出错误。</span><span class="sxs-lookup"><span data-stu-id="a6e14-141">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="a6e14-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="a6e14-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="a6e14-143">问题</span><span class="sxs-lookup"><span data-stu-id="a6e14-143">Issue</span></span>
<span data-ttu-id="a6e14-144">`--interactive` 参数无法由 dotnet cli 转发，因此导致错误 `error: Missing value for option 'interactive'` 出现</span><span class="sxs-lookup"><span data-stu-id="a6e14-144">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="a6e14-145">解决方法</span><span class="sxs-lookup"><span data-stu-id="a6e14-145">Workaround</span></span>
<span data-ttu-id="a6e14-146">将 interactive 选项与其他任何 dotnet 命令一起运行（如 `dotnet restore --interactive`），并进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6e14-146">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="a6e14-147">凭据提供程序可能会缓存身份验证。</span><span class="sxs-lookup"><span data-stu-id="a6e14-147">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="a6e14-148">然后，运行 `dotnet nuget push`。</span><span class="sxs-lookup"><span data-stu-id="a6e14-148">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="a6e14-149">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="a6e14-149">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="a6e14-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="a6e14-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="a6e14-151">问题</span><span class="sxs-lookup"><span data-stu-id="a6e14-151">Issue</span></span>
<span data-ttu-id="a6e14-152">使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。</span><span class="sxs-lookup"><span data-stu-id="a6e14-152">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="a6e14-153">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="a6e14-153">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="a6e14-154">解决方法</span><span class="sxs-lookup"><span data-stu-id="a6e14-154">Workaround</span></span>
<span data-ttu-id="a6e14-155">通过将 `RestoreAdditionalProjectSources` 设置为无，禁用回退文件夹。</span><span class="sxs-lookup"><span data-stu-id="a6e14-155">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="a6e14-156">请谨慎使用 `<RestoreAdditionalProjectSources/>`，因为它会导致从 NuGet.org 下载许多包，否则将从回退文件夹中还原这些包。</span><span class="sxs-lookup"><span data-stu-id="a6e14-156">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
