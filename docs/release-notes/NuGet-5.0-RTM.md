---
title: NuGet 5.0 RTM 发行说明
description: 包括已知的问题、 bug 修复、 新功能和 Dcr NuGet 5.0 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 7e719a3bb5069c461820c6f884487af1eb04bf86
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610663"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="e42b7-103">NuGet 5.0 发行说明</span><span class="sxs-lookup"><span data-stu-id="e42b7-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="e42b7-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="e42b7-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e42b7-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="e42b7-105">NuGet version</span></span> | <span data-ttu-id="e42b7-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="e42b7-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e42b7-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e42b7-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e42b7-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="e42b7-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e42b7-109">Visual Studio 2019 版本 16.0</span><span class="sxs-lookup"><span data-stu-id="e42b7-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e42b7-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e42b7-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="e42b7-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="e42b7-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e42b7-112">Visual Studio 2019 版本 16.0.4</span><span class="sxs-lookup"><span data-stu-id="e42b7-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e42b7-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>， [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e42b7-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="e42b7-114"><sup>1</sup>随 Visual Studio 2019 一起安装.NET Core 工作负载</span><span class="sxs-lookup"><span data-stu-id="e42b7-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="e42b7-115"><sup>2</sup>作为可选安装随.NET Core 工作负载的 Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="e42b7-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="e42b7-116">摘要:什么是 5.0 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e42b7-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="e42b7-117">对还原的支持[筛选解决方案](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)在 Visual Studio 2019- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="e42b7-117">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="e42b7-118">`BuildTransitive` 文件夹允许包来间接地参与到宿主项目中的目标/属性[#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="e42b7-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="e42b7-119">更好地支持 NuGet Iv Api-中的 PackageReference 方案[#7005](https://github.com/NuGet/Home/issues/7005)， [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="e42b7-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="e42b7-120">`nuget.exe pack project.json` 已弃用- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="e42b7-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="e42b7-121">第 1 代凭据提供程序插件已被[第 2 代](https://aka.ms/nuget-cross-platform-authentication-plugin)并且将很快被弃用的[#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="e42b7-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e42b7-122">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="e42b7-122">Issues fixed in this release</span></span>

<span data-ttu-id="e42b7-123">**Bug**</span><span class="sxs-lookup"><span data-stu-id="e42b7-123">**Bugs**</span></span>

* <span data-ttu-id="e42b7-124">执行操作时 NoOp 还原，避免 \*。 在 obj 目录-dgspec.json 写[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="e42b7-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="e42b7-125">~/.Nuget 内创建的文件的权限是太打开- [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="e42b7-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="e42b7-126">`dotnet list package --outdated` 不使用需要身份验证-源[#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="e42b7-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="e42b7-127">NuGet.VisualStudio.IVsPackageInstaller-调用上使用的任何包的项目引用始终使用 packages.config，即使默认值设置为 PackageReference- [#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="e42b7-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="e42b7-128">PMC:更新包从列表去除包上重新安装失败 （"找不到包"）。</span><span class="sxs-lookup"><span data-stu-id="e42b7-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="e42b7-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="e42b7-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="e42b7-130">在我们的存储库和 VSIX 中-添加第三方通知[#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="e42b7-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="e42b7-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage 应安装最新版本时提供的任何版本[#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="e42b7-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="e42b7-132">-dotnet nuget push 交互式支持- [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="e42b7-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="e42b7-133">当还原锁定文件时，不应引发 NU1603 警告。</span><span class="sxs-lookup"><span data-stu-id="e42b7-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="e42b7-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="e42b7-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="e42b7-135">NuGet 应使用最小日志记录-还原期间无法打印项目路径[#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="e42b7-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="e42b7-136">-适用于 dotnet 的交互支持中删除程序包- [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="e42b7-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="e42b7-137">添加与 TypeForwardedTo attrs-备份 NuGet.Packaging.Core [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="e42b7-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="e42b7-138">plugins_cache 需要较短的路径来有效工作的[#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="e42b7-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="e42b7-139">如果用户未请求特定的 msbuild 版本-则更喜欢 msbuild 发现路径[#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="e42b7-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="e42b7-140">`nuget.exe /?` 应列出正确的 msbuild 版本- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="e42b7-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="e42b7-141">NuGet.targets(498,5)： 错误：找不到部分路径 / tmp/NuGetScratch-mono-上[#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="e42b7-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="e42b7-142">还原不必要地枚举在计算机缓存中的引用包的所有版本的内容[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="e42b7-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="e42b7-143">MSBuild 自动检测后安装与 2019年预览-始终选择 16.0 [#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="e42b7-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="e42b7-144">一种解决方案上的 dotnet 列表包输出的框架的重复条目[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="e42b7-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="e42b7-145">异常"空路径名称不是合法的"时调用 IVsPackageInstaller.InstallPackage 上旧项目和包文件夹不存在。</span><span class="sxs-lookup"><span data-stu-id="e42b7-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="e42b7-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="e42b7-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="e42b7-147">msbuild /t: restore 最低详细级别应为更少的[#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="e42b7-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="e42b7-148">VS 16.0 的 NuGet UI 具有不可读的选项卡颜色问题-由于[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="e42b7-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="e42b7-149">NuGet.Core 和 NuGet.Clients License.txt 澄清- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="e42b7-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="e42b7-150">还原不必要地枚举全局包文件夹中尝试确定类型- [#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="e42b7-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="e42b7-151">从锁定文件强制错误应显示在错误列表窗口- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="e42b7-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="e42b7-152">修复 NuGet.Configuration 问题- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="e42b7-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="e42b7-153">适应 MSBuild 更新其安装位置- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="e42b7-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="e42b7-154">NuGet.Build.Tasks.Pack 应该是开发依赖项- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="e42b7-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="e42b7-155">添加包扩展点包括调试符号的[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="e42b7-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="e42b7-156">`dotnet pack` 应保留在创建 nupkg 的依赖项版本范围 （即使使用浮动版本）- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="e42b7-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="e42b7-157">`dotnet restore` 失败时用户级配置还具有源-已经过身份验证的源上[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="e42b7-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="e42b7-158">包不应限制的内容文件-BuildActions 套[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="e42b7-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="e42b7-159">使用 ProjectReference，这要求 AssetTargetFallback 成功，应发出警告。</span><span class="sxs-lookup"><span data-stu-id="e42b7-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="e42b7-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="e42b7-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="e42b7-161">由于线程问题到 CPS (CommonProjectSystem) 的调用时的死锁[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="e42b7-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="e42b7-162">`dotnet add package` 不会从全局配置的凭据用于在本地配置-中指定的源[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="e42b7-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="e42b7-163">使用 MEF 上异步调用的线程问题的代码路径- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="e42b7-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="e42b7-164">签名： 报告两次，而无需调用堆栈的错误[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="e42b7-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="e42b7-165">使用不受信任的签名证书安装已签名的包应显示错误- [#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="e42b7-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="e42b7-166">NuGet 还原不正确 Noop 当 2 个项目共享 obj 目录- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="e42b7-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="e42b7-167">不能使用与 PAT `dotnet restore` Linux 上的使用经过身份验证源-中的包[#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="e42b7-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="e42b7-168">dotnet 还原由于已禁用计算机范围源-而失败[#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="e42b7-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="e42b7-169">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="e42b7-169">**DCRs**</span></span>

* <span data-ttu-id="e42b7-170">未来"dotnet 包 project.json"的删除，则发出警告[#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="e42b7-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="e42b7-171">添加对 Gen1 凭据插件-的弃用警告[#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="e42b7-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="e42b7-172">签名：已启用存储库，需要为存储库的客户端验证的每个包签名--通过 RepositorySignatures/5.0.0 资源- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="e42b7-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="e42b7-173">限制每个源通过 NuGet.Config 的 http 请求数目[#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="e42b7-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="e42b7-174">NuGet 应针对 Net472 （以帮助清理 16.0 生成的 VSIX）- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="e42b7-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="e42b7-175">PMC:删除 OpenPackagePage 命令- [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="e42b7-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="e42b7-176">请 NetCoreApp 3.0 映射到 NetStandard 2.1- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="e42b7-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="e42b7-177">将 netstandard2.0 支持添加到 NuGet.\* 包- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="e42b7-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="e42b7-178">允许程序包作者可定义生成资产可传递行为- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="e42b7-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="e42b7-179">支持 VS 2019 解决方案筛选器功能。</span><span class="sxs-lookup"><span data-stu-id="e42b7-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="e42b7-180">此外支持项目不在解决方案中或已卸载的项目。</span><span class="sxs-lookup"><span data-stu-id="e42b7-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="e42b7-181">需要首先还原完整的解决方案 （通过 CLI 或 VS） [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="e42b7-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="e42b7-182">NuGet 5.0 程序集 （通过 TFM 更改） 的要求.NET 4.7.2 [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="e42b7-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="e42b7-183">从 NuGet.Packaging NuGetLicenseData 应为公共类型。</span><span class="sxs-lookup"><span data-stu-id="e42b7-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="e42b7-184">更新许可证元数据从 spdx 引入。</span><span class="sxs-lookup"><span data-stu-id="e42b7-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="e42b7-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="e42b7-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="e42b7-186">删除过时设置 Api- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="e42b7-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="e42b7-187">解决方法 1 的系统上还原超时 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="e42b7-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="e42b7-188">NuGet 首选 NTLM 身份验证，即使有 NuGet.config 中凭据-将配置选项添加到筛选器身份验证类型的凭据- [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="e42b7-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="e42b7-189">Packagereference （匹配 Packages.Config 功能）-启用 EmbedInteropTypes [# 2365年](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="e42b7-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="e42b7-190">**[在此版本中-5.0 RTM 中已解决所有问题的列表](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="e42b7-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="e42b7-191">摘要:什么是 5.0.2 版中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e42b7-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="e42b7-192">（当通过 dotnet.exe 或 mono.exe 运行） 的安全性-应使用正确的权限创建 obj 文件夹[#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="e42b7-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="e42b7-193">在 mono/MacOS 上的 nuget.exe 还原失败，并自定义 nuget.config 并`PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span><span class="sxs-lookup"><span data-stu-id="e42b7-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="e42b7-194">已知问题</span><span class="sxs-lookup"><span data-stu-id="e42b7-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="e42b7-195">FallbackFolders 中由 .NET Core SDK 安装的包是自定义安装的，无法通过签名验证。</span><span class="sxs-lookup"><span data-stu-id="e42b7-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="e42b7-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="e42b7-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="e42b7-197">问题</span><span class="sxs-lookup"><span data-stu-id="e42b7-197">Issue</span></span>
<span data-ttu-id="e42b7-198">使用 dotnet.exe 2.x 还原多重定位 netcoreapp 1.x 和 netcoreapp 2.x 的项目时，回退文件夹被视为文件源。</span><span class="sxs-lookup"><span data-stu-id="e42b7-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="e42b7-199">也就是说，在还原时，NuGet 将从回退文件夹中选取包，并尝试将它安装到全局包文件夹，再执行失败的常规签名验证。</span><span class="sxs-lookup"><span data-stu-id="e42b7-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="e42b7-200">解决方法</span><span class="sxs-lookup"><span data-stu-id="e42b7-200">Workaround</span></span>
<span data-ttu-id="e42b7-201">通过设置来禁用回退文件夹的使用情况`RestoreAdditionalProjectSources`为 nothing:</span><span class="sxs-lookup"><span data-stu-id="e42b7-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="e42b7-202">因为现在会从 NuGet.org 下载包将从回退文件夹中还原，请谨慎使用此。</span><span class="sxs-lookup"><span data-stu-id="e42b7-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
