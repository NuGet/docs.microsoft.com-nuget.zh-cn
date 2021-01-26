---
title: NuGet 5.0 RTM 发行说明
description: NuGet 5.0 的发行说明，包括已知问题、bug 修复、新增功能和 Dcr。
author: JonDouglas
ms.author: jodou
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 637db1ae128ce020c33e54e56148c848a5f905a5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776227"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="a2f00-103">NuGet 5.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="a2f00-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="a2f00-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="a2f00-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a2f00-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="a2f00-105">NuGet version</span></span> | <span data-ttu-id="a2f00-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="a2f00-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a2f00-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a2f00-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a2f00-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="a2f00-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a2f00-109">Visual Studio 2019 版本 16.0</span><span class="sxs-lookup"><span data-stu-id="a2f00-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a2f00-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a2f00-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="a2f00-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="a2f00-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a2f00-112">Visual Studio 2019 版本16.0。4</span><span class="sxs-lookup"><span data-stu-id="a2f00-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a2f00-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a2f00-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a2f00-114"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="a2f00-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a2f00-115"><sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装</span><span class="sxs-lookup"><span data-stu-id="a2f00-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="a2f00-116">摘要：5.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a2f00-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="a2f00-117">支持在 Visual Studio 2019 中还原 [筛选的解决方案](/visualstudio/ide/filtered-solutions?view=vs-2019) - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="a2f00-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="a2f00-118">`BuildTransitive` 文件夹使包可以向主机项目传递目标/属性- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="a2f00-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="a2f00-119">更好地支持 NuGet IVs Api 中的 PackageReference 方案- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="a2f00-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="a2f00-120">`nuget.exe pack project.json` 已弃用- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="a2f00-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="a2f00-121">第1代凭据提供程序插件已被 [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) 取代，即将弃用- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="a2f00-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a2f00-122">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="a2f00-122">Issues fixed in this release</span></span>

<span data-ttu-id="a2f00-123">**Bug**</span><span class="sxs-lookup"><span data-stu-id="a2f00-123">**Bugs**</span></span>

* <span data-ttu-id="a2f00-124">执行 NoOp 还原时，请避免 \* .dgspec.js在 obj 目录中写入 [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a2f00-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a2f00-125">在 ~/.nuget 中创建的文件的权限过于打开- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="a2f00-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="a2f00-126">`dotnet list package --outdated`不适用于需要身份验证[#7605](https://github.com/NuGet/Home/issues/7605)的源</span><span class="sxs-lookup"><span data-stu-id="a2f00-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="a2f00-127">VisualStudio。 IVsPackageInstaller-对没有包引用的项目调用始终使用 packages.config，即使默认值设置为 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="a2f00-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="a2f00-128">PMC： Update-Package 重新安装失败 ( 在 delisted 包上 "找不到包 ) "。</span><span class="sxs-lookup"><span data-stu-id="a2f00-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="a2f00-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="a2f00-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="a2f00-130">在我们的存储库和 VSIX 中添加第三方通知- [#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="a2f00-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="a2f00-131">如果未指定版本，则 VisualStudio 应安装最新版本 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="a2f00-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="a2f00-132">--交互式支持 dotnet nuget 推送 [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="a2f00-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="a2f00-133">当还原时，不应引发 NU1603 警告。</span><span class="sxs-lookup"><span data-stu-id="a2f00-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="a2f00-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="a2f00-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="a2f00-135">在还原过程中 NuGet 不应打印项目路径 [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="a2f00-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="a2f00-136">--交互式支持 dotnet 删除包- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="a2f00-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="a2f00-137">添加 back Nuget.exe with TypeForwardedTo attrs- [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="a2f00-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="a2f00-138">plugins_cache 需要更短的路径才能正常工作- [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="a2f00-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="a2f00-139">如果用户没有请求特定的 msbuild 版本，则首选 msbuild 发现的路径- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="a2f00-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="a2f00-140">`nuget.exe /?` 应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="a2f00-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="a2f00-141">NuGet (498，5) ：错误：找不到路径 "/tmp/NuGetScratch" 的一部分 [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="a2f00-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="a2f00-142">还原不必要地枚举计算机缓存中引用包的所有版本的内容- [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="a2f00-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="a2f00-143">在安装 VS 2019 Preview 后，MSBuild 自动检测始终会选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="a2f00-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="a2f00-144">解决方案中的 dotnet 列表包输出框架[#7607](https://github.com/NuGet/Home/issues/7607)的重复条目</span><span class="sxs-lookup"><span data-stu-id="a2f00-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="a2f00-145">在旧项目和包文件夹中调用 IVsPackageInstaller 时，异常 "空路径名称不合法"。</span><span class="sxs-lookup"><span data-stu-id="a2f00-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="a2f00-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="a2f00-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="a2f00-147">msbuild/t：还原最少详细级别应该更小- [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="a2f00-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="a2f00-148">VS 16.0 的 NuGet UI 由于颜色问题而无法读取选项卡- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="a2f00-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="a2f00-149">NuGet & NuGet。客户端 License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="a2f00-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="a2f00-150">还原不必要地枚举全局包文件夹，尝试确定类型 [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="a2f00-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="a2f00-151">锁定文件强制执行的错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="a2f00-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="a2f00-152">解决 NuGet.Configu 问题- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="a2f00-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="a2f00-153">适应 MSBuild 更新其安装位置- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="a2f00-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="a2f00-154">Nuget.exe 应为开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="a2f00-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="a2f00-155">添加包扩展点以包括调试符号- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="a2f00-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="a2f00-156">`dotnet pack` 应在创建的 nupkg (中保留依赖项版本范围，即使使用浮动版本) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="a2f00-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="a2f00-157">`dotnet restore`当用户级配置还具有源[#7209](https://github.com/NuGet/Home/issues/7209)时，已验证的源上的失败</span><span class="sxs-lookup"><span data-stu-id="a2f00-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="a2f00-158">包不应限制内容文件的 BuildActions 集- [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="a2f00-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="a2f00-159">使用需要 AssetTargetFallback 成功的 ProjectReference 会发出警告。</span><span class="sxs-lookup"><span data-stu-id="a2f00-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="a2f00-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="a2f00-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="a2f00-161">由于调用 CPS (CommonProjectSystem 时出现线程问题，导致死锁) - [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="a2f00-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="a2f00-162">`dotnet add package` 对于本地配置中指定的源，不使用全局配置的凭据 [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="a2f00-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="a2f00-163">在异步代码路径上调用 MEF 的线程问题- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="a2f00-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="a2f00-164">签名：错误报告了两次，没有调用堆栈- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="a2f00-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="a2f00-165">安装带有不受信任签名证书的签名包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="a2f00-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="a2f00-166">当2个项目共享 obj 目录时，NuGet 还原 Noop 错误- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="a2f00-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="a2f00-167">不能 `dotnet restore` 在 Linux 上将 PAT 与已通过身份验证的源中的包一起使用- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="a2f00-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="a2f00-168">dotnet restore 因禁用了计算机范围的源而失败- [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="a2f00-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="a2f00-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="a2f00-169">**DCRs**</span></span>

* <span data-ttu-id="a2f00-170">以后删除 "dotnet pack project.js" 时警告- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="a2f00-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="a2f00-171">为 Gen1 credential 插件添加弃用警告- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="a2f00-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="a2f00-172">签名：启用的存储库需要将每个包的客户端验证为签名[#7759](https://github.com/NuGet/Home/issues/7759)的存储库</span><span class="sxs-lookup"><span data-stu-id="a2f00-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="a2f00-173">限制每个源的 http 请求数，通过 NuGet.Config [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="a2f00-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="a2f00-174">NuGet 应面向 Net472 (以帮助清理 VSIX) 的16.0 内部版本- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="a2f00-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="a2f00-175">PMC：删除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="a2f00-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="a2f00-176">将 NetCoreApp 3.0 映射到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="a2f00-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="a2f00-177">将 netstandard 2.0 支持添加到 NuGet。 \* 包- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="a2f00-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="a2f00-178">允许包作者定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="a2f00-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="a2f00-179">支持 VS 2019 解决方案筛选器功能。</span><span class="sxs-lookup"><span data-stu-id="a2f00-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="a2f00-180">还支持不在解决方案中的项目或已卸载的项目。</span><span class="sxs-lookup"><span data-stu-id="a2f00-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="a2f00-181">需要通过 CLI 或 VS) first [#5820](https://github.com/NuGet/Home/issues/5820)还原完整的解决方案 (</span><span class="sxs-lookup"><span data-stu-id="a2f00-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="a2f00-182">NuGet 5.0 程序集需要 .NET 4.7.2 (通过 TFM 更改) - [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="a2f00-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="a2f00-183">从 NuGet NuGetLicenseData。打包应为公共类型。</span><span class="sxs-lookup"><span data-stu-id="a2f00-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="a2f00-184">从 spdx 更新许可证元数据引入。</span><span class="sxs-lookup"><span data-stu-id="a2f00-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="a2f00-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="a2f00-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="a2f00-186">删除过时的设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="a2f00-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="a2f00-187">具有1个 cpu [#6742](https://github.com/NuGet/Home/issues/6742)的系统上的解决方法还原超时</span><span class="sxs-lookup"><span data-stu-id="a2f00-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="a2f00-188">即使 NuGet.config-add config 选项中有凭据用于筛选凭据的身份验证类型，NuGet 也优先于 NTLM 身份验证- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="a2f00-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="a2f00-189">启用 EmbedInteropTypes for PackageReference (匹配 Packages.Config 功能) - [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="a2f00-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="a2f00-190">**[此版本中已修复的所有问题的列表-5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="a2f00-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="a2f00-191">摘要：5.0.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="a2f00-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="a2f00-192">通过 dotnet.exe 或 mono.exe) 运行时的安全 (-应创建具有正确权限的 obj 文件夹 [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="a2f00-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="a2f00-193">Mono/MacOS 上 nuget.exe 还原失败，并出现自定义 nuget.config 和 `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="a2f00-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="a2f00-194">已知问题</span><span class="sxs-lookup"><span data-stu-id="a2f00-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="a2f00-195">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="a2f00-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="a2f00-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="a2f00-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="a2f00-197">问题</span><span class="sxs-lookup"><span data-stu-id="a2f00-197">Issue</span></span>
<span data-ttu-id="a2f00-198">使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。</span><span class="sxs-lookup"><span data-stu-id="a2f00-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="a2f00-199">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="a2f00-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="a2f00-200">解决方法</span><span class="sxs-lookup"><span data-stu-id="a2f00-200">Workaround</span></span>
<span data-ttu-id="a2f00-201">通过将设置为 nothing 来禁用回退文件夹的使用 `RestoreAdditionalProjectSources` ：</span><span class="sxs-lookup"><span data-stu-id="a2f00-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="a2f00-202">请谨慎使用这一点，因为现在将从 NuGet.org 下载从回退文件夹还原的包。</span><span class="sxs-lookup"><span data-stu-id="a2f00-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>