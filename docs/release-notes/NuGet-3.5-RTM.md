---
title: NuGet 3.5 Beta 发行说明
description: 包括已知的问题、 bug 修复、 增加的功能，以及 DCRs NuGet 3.5 的发行说明。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cdb540229cae0e6e952ac2a0c00c8801ccbbb28d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822586"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="7b2e0-103">NuGet 3.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="7b2e0-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="7b2e0-104">[NuGet 3.5 RC 发行说明](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="7b2e0-105">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="7b2e0-105">Bug Fixes</span></span>

* <span data-ttu-id="7b2e0-106">包不 mono-上使用 MSBuild 14.1 [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="7b2e0-107">更新选项卡上不会选择最新可用版本更新改为选择的当前已安装的版本- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="7b2e0-108">对专用 v2 MyGet 源进行身份验证，并单击"显示更多结果 x"后修复崩溃的[#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="7b2e0-109">日志消息按相反的顺序可能的 UI-纳入[#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="7b2e0-110">"不支持给定的路径的格式"-v3.4.4-Nuget 还原引发[#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="7b2e0-111">NuGet 命令行 3.6 beta 不会遵循-Prop Configuration = 释放- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="7b2e0-112">在大型项目-上安装 Nuget IKVM 慢速[#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="7b2e0-113">nuget.exe-自助保留在自我更新-更新[#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="7b2e0-114">从 UNC 共享的 3.5 安装/还原已从 3.4.4-性能回归[#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="7b2e0-115">错误时从包管理 UI net451 项目-安装 Moq [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="7b2e0-116">在解决方案级别的安装选项卡不会显示包的版本- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="7b2e0-117">xproj`project.json`从已安装选项卡上的更新丢失状态- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="7b2e0-118">上的 NuGet 包`.csproj`忽略空文件中的元素`.nuspec`文件- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="7b2e0-119">在 IIS 中承载的网站项目不应导致还原失败- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="7b2e0-120">凭据未检索到从 Nuget.Config 当 v3 终结点重定向到 v2- [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="7b2e0-121">NuGet 包未能检索可移植程序集元数据的时解析程序集[#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="7b2e0-122">找不到 Nuget`msbuild.exe`上 Mono- [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="7b2e0-123">nuget.exe 包不允许的预发行标记开头号- [# 1743年](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="7b2e0-124">在 VS2015E-上 nuget 包安装失败[# 1298年](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="7b2e0-125">allowedVersions 筛选不在解决方案级别的工作[#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="7b2e0-126">还原随机将失败并具有相同的项已添加了键。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="7b2e0-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="7b2e0-128">无法安装在 Nuget.Common `.csproj`  -  [# 2635年](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="7b2e0-129">当使用 UI 搜索 V2 源，为每个 ID-两次调用 FindPackagesById [# 2517年](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="7b2e0-130">包不能依赖于项目- [# 2490年](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="7b2e0-131">nuget.exe 包-记录排除但不是支持- [# 2284年](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="7b2e0-132">问题的错误消息时的文件部分`.nuspec`无效- [# 1686年](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="7b2e0-133">请求始终发送整个包两次通过身份验证包源- [# 1501年](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="7b2e0-134">时调用 nuget.exe 更新 \*.csproj 而项目没有指定任何信息`packages.config`  -  [# 1496年](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="7b2e0-135">`packages.config` 从 V2 源-5xx 状态代码，还原不重试[# 1217年](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="7b2e0-136">在文件中的 src 双点`.nuspec`不起作用- [# 2947年](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="7b2e0-137">CoreCLR 还原需要忽略与加密-馈送[# 2942年](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="7b2e0-138">nuget.exe 推送 403 处理的错误会提示输入凭据- [# 2910年](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="7b2e0-139">程序包管理器通过 NuGet 更新中删除属性从`project.json`  -  [# 2888年](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="7b2e0-140">尝试加载"NuGet.TeamFoundationServer14"，但 DLL 名称更改为"NuGet.TeamFoundationServer"-NuGet.PackageManagement.VisualStudio [# 2857年](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="7b2e0-141">程序包管理器用户界面不显示新更新版本- [# 2828年](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="7b2e0-142">更新包尝试使用 packageid，而不是 package.version-版本[# 2771年](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="7b2e0-143">如果项目不使用 nuget，nuget 还原 csproj 应错误 (`packages.config`或`project.json`)- [# 2766年](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="7b2e0-144">TFS 错误"[文件] 不能在工作区中，找到或您没有权限访问该"期间升级或卸载解决方案/项目绑定到 TFS 源代码管理- [# 2739年](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="7b2e0-145">更新包不获取非目标包的依赖关系[# 2724年](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="7b2e0-146">没有任何方法可设置为 Nuget 包管理器 UI 操作的日志详细级别[# 2705年](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="7b2e0-147">nuget 配置无效-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="7b2e0-148">中的 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 不起作用- [# 2653年](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="7b2e0-149">nuget 3.4.3 释放-获取值不能为包生成的 null [# 2648年](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="7b2e0-150">还原时未使用存储的凭据从 Nuget.Config VSTS 馈送- [# 2647年](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="7b2e0-151">[dotnet 还原]-configfile 是相对于项目目录，而不是 cmd 目录中- [# 2639年](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="7b2e0-152">在版本常量代码-过度分配[# 2632年](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="7b2e0-153">Nuget.exe 尝试安装相同的多个实例中并行原因 double 的写入-打包[# 2628年](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="7b2e0-154">依赖项信息尚未缓存的多项目操作- [# 2619年](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="7b2e0-155">安装和更新下载包，而不首先-检查包文件夹[# 2618年](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="7b2e0-156">如果包源列表为空，无法添加包源通过 UI (NuGet 3.4.x)- [# 2617年](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="7b2e0-157">具有误导性错误，当试图安装包依赖于设计时外观- [# 2594年](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="7b2e0-158">从 PackageManager 控制台中设置"全部"安装包尝试仅第一个源- [# 2557年](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="7b2e0-159">不解压缩的最新 beta ModernHttpClient- [# 2518年](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="7b2e0-160">在使用自生成 NuGet 3.4.1-启动 VS2015 崩溃[# 2419年](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="7b2e0-161">更新命令可能是更详细如果 i 询问其成为...- [# 2418年](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="7b2e0-162">本地生成的 VSIX 应作为 CI 生成具有相同的 Dll 和文件。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="7b2e0-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="7b2e0-164">在生成的修复 NuGet 降级警告[# 2396年](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="7b2e0-165">无法进行身份验证的包源 （3 次） 永久的阻止[# 2362年](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="7b2e0-166">从 nuget v3.3 + 安装的包源具有自变量时，不正确还原包内容-NoCache 当包包含`.nupkg`文件- [# 2354年](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="7b2e0-167">Nuget 安装的所有包源，但包缺少 1 从源失败- [# 2322年](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="7b2e0-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="7b2e0-169">如果单个源失败授权-安装块[# 2034年](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="7b2e0-170">`.nuspec` 版本范围应重写-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="7b2e0-171">更新包非常缓慢-"尝试收集依赖项信息"- [# 1909年](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="7b2e0-172">NuGet 隐形降级包时批处理更新及其依赖项- [# 1903年](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="7b2e0-173">nuget.exe 更新中删除程序集强名称和私有特性。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="7b2e0-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="7b2e0-175">相对文件路径"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="7b2e0-176">提高冲突解决程序失败消息- [# 1373年](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="7b2e0-177">在 v3 的更新包将失败并不在指定的源的包[# 1013年](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="7b2e0-178">对于包源使用相对路径会产生问题，若要使用- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="7b2e0-179">缺少的 NUPKG 文件如果间接的依赖关系已存在具有较低的版本要求-生成从项目中的依赖项[#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="7b2e0-180">删除项目关闭相应 UI 窗口时，但是，重命名项目不是重命名用户界面窗口。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="7b2e0-181">请注意 PMC 侦听项目重命名和项目删除事件数- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="7b2e0-182">[Willow Web 工作负荷]创建 Razor v3 WSP 挂起- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="7b2e0-183">特定包的安装/还原失败，"包包含多个 nuspec 文件。"</span><span class="sxs-lookup"><span data-stu-id="7b2e0-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="7b2e0-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="7b2e0-185">小写 Id （& a)`packages.config`方案- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="7b2e0-186">[3.5 beta2 之前]程序包还原失败后还原"传统"程序包- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="7b2e0-187">nuget 包强制将.tt 文件添加到内容文件夹无论- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="7b2e0-188">ASP.NET web 应用的更新包将生成与文件相关的警告： 源- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="7b2e0-189">nuget 包 csproj (与`project.json`) 发生崩溃，如果没有 packOptions 和在 JSON 文件的所有者[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="7b2e0-190">适用于的 nuget 包`project.json`忽略摘要、 作者、 所有者等-之类的 packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="7b2e0-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="7b2e0-192">NuGet 包将忽略输出中的依赖关系`.nuspec`为`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="7b2e0-193">使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="7b2e0-194">在任何下的文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="7b2e0-195">无法打包面向.Net 库标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="7b2e0-196">文件-> 新建项目-> 类库 （可移植） VS2015 和 Dev15-中的项目失败[#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="7b2e0-197">nuGet 错误-1.0.0-\* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="7b2e0-198">查找包无法显示，但安装包工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="7b2e0-199">错误时 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="7b2e0-200">nuget 包的 xproj 默认为无效的目标路径的[#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="7b2e0-201">当已安装的 VS 2015 update 3 上使用的 NuGet 版本 3.5.0 错误发生的 VS [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="7b2e0-202">的"被 packages.config" `project.json` (UWP，即生成集成) 项目- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="7b2e0-203">更新安装到 preview2-003121，这是官方 preview2 生成的生成脚本的 dotnet cli。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="7b2e0-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="7b2e0-205">包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="7b2e0-206">-ApiKey delete 命令行上不是读取/以发送 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="7b2e0-207">不正确的字符串： 稳定程序包版本不应具有在预发布的依赖项。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="7b2e0-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="7b2e0-209">OptimizedZipPackage 缓存离开空文件夹- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="7b2e0-210">创建 （net46 和 windows 10） 的 PCL 项目 get NullRef 异常。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="7b2e0-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="7b2e0-212">Nuget 更新应提供信息性消息的 allowedVersions 约束的限制更高版本时[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="7b2e0-213">Nuget v3 还原问题- [# 2891年](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="7b2e0-214">凭据插件退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="7b2e0-215">`project.json` nuget 还原会导致重新编译时执行任何操作更改- [# 2817年](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="7b2e0-216">符号包不应在安装或更新-中使用[# 2807年](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="7b2e0-217">VS 中 repositoryPath 不支持环境变量 （nuget.exe 一样）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="7b2e0-218">使用的辅助功能--标签在程序包管理器用户界面中未标记的 UIElements [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="7b2e0-219">使用连字符连接的配置文件的可移植框架会被拒绝。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="7b2e0-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="7b2e0-221">NuGet 包管理器应使它清楚该详细信息不适用于的包中的选项列表`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="7b2e0-222">nuget.exe 推送/删除不会使用 API 密钥- [# 2627年](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="7b2e0-223">从锁定文件的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="7b2e0-224">NuGet 3.3.0 更新失败，出现...的其他约束中定义 packages.config 会阻止此操作。</span><span class="sxs-lookup"><span data-stu-id="7b2e0-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="7b2e0-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="7b2e0-226">从本地源中不存在将引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="7b2e0-227">"可用的升级"筛选器以显示与版本约束中的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="7b2e0-228">无法更新本地程序包- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="7b2e0-229">功能</span><span class="sxs-lookup"><span data-stu-id="7b2e0-229">Features</span></span>

* <span data-ttu-id="7b2e0-230">引用添加的 NuGet 的支持为 false 的设置 CopyLocal [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="7b2e0-231">MSBuild 15-nuget.exe 支持[# 1937年](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="7b2e0-232">包的支持。`csproj`</span><span class="sxs-lookup"><span data-stu-id="7b2e0-232">Pack support for .`csproj`</span></span><span data-ttu-id="7b2e0-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="7b2e0-234">禁用用户执行任何操作，正在执行的用户操作时- [# 1440年](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="7b2e0-235">NuGet 应添加对支持`runtimes/{rid}/nativeassets/{txm}/`  -  [# 2782年](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="7b2e0-236">添加 NuGet 中缺少的 framework 兼容性 （它们已处于 3.x） 的 2.x- [# 2720年](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="7b2e0-237">对回退包文件夹的支持[# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="7b2e0-238">设计和实现包类型的概念，以支持工具包- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="7b2e0-239">将 API 来获取到的全局包文件夹的路径添加[# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="7b2e0-240">启用包中的 SemVer 2.0.0 [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="7b2e0-241">DCR</span><span class="sxs-lookup"><span data-stu-id="7b2e0-241">DCRs</span></span>

* <span data-ttu-id="7b2e0-242">nuget.exe 推送的超时参数不起作用- [# 2785年](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="7b2e0-243">包描述文本应为可选择- [# 1769年](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="7b2e0-244">启用 nuget.exe 生成`.props`和`.targets`文件`.nuproj`项目[# 2711年](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="7b2e0-245">添加扩展性 API 进行比较导入的框架[# 2633年](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="7b2e0-246">使用时隐藏依存关系选项`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="7b2e0-247">打印出 nuget.exe 版本标头中详细输出- [# 1887年](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="7b2e0-248">NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="7b2e0-249">错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="7b2e0-250">为更新-使用 ReShaper 和 NuGet 修复性能问题[#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="7b2e0-251">添加 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="7b2e0-252">利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="7b2e0-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
