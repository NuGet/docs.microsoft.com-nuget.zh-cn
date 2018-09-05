---
title: NuGet 3.5 测试版发行说明
description: 包括已知的问题、 bug 修复、 新增的功能和 Dcr NuGet 3.5 的发行说明。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550679"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="1116f-103">NuGet 3.5 发行说明</span><span class="sxs-lookup"><span data-stu-id="1116f-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="1116f-104">[NuGet 3.5 RC 发行说明](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC 发行说明](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="1116f-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="1116f-105">Bug 修复</span><span class="sxs-lookup"><span data-stu-id="1116f-105">Bug Fixes</span></span>

* <span data-ttu-id="1116f-106">包不在 mono-使用 MSBuild 14.1 [#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="1116f-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="1116f-107">更新选项卡上不会选择最新可用版本更新改为选择的当前已安装的版本- [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="1116f-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="1116f-108">MyGet 源的专用 v2 进行身份验证，并单击"显示更多结果 x"之后修复故障- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="1116f-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="1116f-109">日志消息似乎是按相反的顺序为 UI- [#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="1116f-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="1116f-110">v3.4.4-Nuget 还原将引发"不支持给定的路径的格式"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="1116f-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="1116f-111">NuGet 命令行 3.6 beta 不会遵循-Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="1116f-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="1116f-112">在大型项目-上安装的 Nuget IKVM 慢速[#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="1116f-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="1116f-113">nuget.exe 更新-自不断在更新本身- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="1116f-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="1116f-114">从 UNC 共享的 3.5 安装/还原已从 3.4.4-性能回归[#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="1116f-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="1116f-115">错误时从包管理 UI net451 项目-安装 Moq [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="1116f-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="1116f-116">在解决方案级别的安装选项卡不会显示包的版本- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="1116f-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="1116f-117">xproj`project.json`从已安装选项卡上的更新将失去状态- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="1116f-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="1116f-118">上的 NuGet 包`.csproj`会忽略空文件中的元素`.nuspec`文件- [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="1116f-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="1116f-119">在 IIS 中承载的网站项目并不会导致还原失败- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="1116f-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="1116f-120">凭据时 v3 终结点将重定向到 v2-不检索从 Nuget.Config [#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="1116f-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="1116f-121">NuGet 包未能解析程序集时检索可移植程序集元数据- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="1116f-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="1116f-122">找不到 Nuget `msbuild.exe` Mono-上[#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="1116f-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="1116f-123">nuget.exe 包不允许预发布标记开头数字- [# 1743年](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="1116f-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="1116f-124">在上 VS2015E-nuget 包安装失败[# 1298年](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="1116f-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="1116f-125">allowedVersions 筛选不在解决方案级别的工作[#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="1116f-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="1116f-126">还原失败，随机并具有相同的项已添加密钥。</span><span class="sxs-lookup"><span data-stu-id="1116f-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="1116f-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="1116f-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="1116f-128">不能安装在 Nuget.Common `.csproj`  -  [# 2635年](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="1116f-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="1116f-129">为每个 ID-两次时使用用户界面来搜索 V2 源，调用 FindPackagesById [# 2517年](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="1116f-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="1116f-130">包不能依赖于项目- [# 2490年](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="1116f-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="1116f-131">nuget.exe 包-排除是记录，但不是支持- [# 2284年](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="1116f-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="1116f-132">出现错误问题的消息时的 contentFiles 部分`.nuspec`无效- [# 1686年](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="1116f-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="1116f-133">推送始终发送整个包两次使用进行身份验证包源- [# 1501年](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="1116f-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="1116f-134">时调用 nuget.exe 更新 \*.csproj 项目时没有提供任何信息`packages.config`  -  [# 1496年](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="1116f-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="1116f-135">`packages.config` 从 V2 源-5xx 状态代码，还原不重试[# 1217年](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="1116f-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="1116f-136">在文件中的 src 两点`.nuspec`不起作用- [# 2947年](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="1116f-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="1116f-137">CoreCLR 还原需要忽略与加密-源[# 2942年](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="1116f-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="1116f-138">nuget.exe 推送 403 处理的错误会提示输入凭据- [# 2910年](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="1116f-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="1116f-139">NuGet 更新通过包管理器中删除属性从`project.json`  -  [# 2888年](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="1116f-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="1116f-140">尝试加载"NuGet.TeamFoundationServer14"，但 DLL 名称更改为"NuGet.TeamFoundationServer"-NuGet.PackageManagement.VisualStudio [# 2857年](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="1116f-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="1116f-141">包管理器 UI 不会显示新更新版本- [# 2828年](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="1116f-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="1116f-142">更新包尝试使用包 id，而不是 package.version-版本[# 2771年](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="1116f-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="1116f-143">如果项目不使用 nuget，nuget 还原 csproj 应错误 (`packages.config`或`project.json`)- [# 2766年](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="1116f-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="1116f-144">TFS 错误"[文件] 不是位于工作区中，或您没有权限访问该"期间升级或卸载解决方案/项目绑定到 TFS 源代码管理- [# 2739年](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="1116f-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="1116f-145">更新包不会为非目标包的依赖项[# 2724年](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="1116f-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="1116f-146">没有任何方法可设置 Nuget 包管理器 UI 操作的日志详细级别[# 2705年](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="1116f-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="1116f-147">nuget 配置无效-VS 2015 VSIX (v3.4.3)- [# 2667年](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="1116f-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="1116f-148">在 DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) 不起作用- [# 2653年](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="1116f-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="1116f-149">nuget 3.4.3 发行版-获取值不能为 null 上包内部版本- [# 2648年](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="1116f-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="1116f-150">还原时未使用存储的凭据从 Nuget.Config VSTS 源- [# 2647年](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="1116f-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="1116f-151">[dotnet 还原]-configfile 是相对于项目而不是 cmd 目录中-dir [# 2639年](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="1116f-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="1116f-152">版本比较代码-的过多分配[# 2632年](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="1116f-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="1116f-153">Nuget.exe 尝试安装相同的多个实例包中并行原因双的写入- [# 2628年](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="1116f-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="1116f-154">依赖关系信息不会缓存的多项目操作- [# 2619年](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="1116f-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="1116f-155">安装和更新下载包，而不首先检查包文件夹[# 2618年](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="1116f-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="1116f-156">如果包源列表为空，无法添加包源通过 UI (NuGet 3.4.x)- [# 2617年](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="1116f-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="1116f-157">如果试图安装包依赖于设计时外观的误导性错误[# 2594年](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="1116f-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="1116f-158">将包安装从 PackageManager 控制台中设置"All"会尝试仅第一个源- [# 2557年](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="1116f-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="1116f-159">最新测试版不解压缩 ModernHttpClient- [# 2518年](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="1116f-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="1116f-160">在启动时使用自生成 NuGet 3.4.1-VS2015 崩溃[# 2419年](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="1116f-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="1116f-161">更新命令可能是更详细，如果 i 要求它是这样...- [# 2418年](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="1116f-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="1116f-162">本地生成的 VSIX 应作为 CI 生成具有相同的 Dll 和文件。</span><span class="sxs-lookup"><span data-stu-id="1116f-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="1116f-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="1116f-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="1116f-164">修复 NuGet 降级警告中生成- [# 2396年](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="1116f-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="1116f-165">无法进行身份验证包源 （3 次） 被永久-阻止[# 2362年](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="1116f-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="1116f-166">从 nuget v3.3 + 安装的包源具有参数时，不正确还原包的内容时包中包含的-NoCache`.nupkg`文件- [# 2354年](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="1116f-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="1116f-167">与所有包源，但包缺少从 1 源，Nuget 安装失败- [# 2322年](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="1116f-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="1116f-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="1116f-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="1116f-169">如果单个源失败授权-安装块[# 2034年](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="1116f-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="1116f-170">`.nuspec` 版本范围应重写-IncludeReferencedProjects 版本- [# 1983年](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="1116f-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="1116f-171">更新包非常缓慢-"尝试收集依赖项信息"- [# 1909年](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="1116f-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="1116f-172">隐藏降级 NuGet 包时批处理更新及其依赖项- [# 1903年](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="1116f-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="1116f-173">nuget.exe 更新中删除程序集强名称和专用属性。</span><span class="sxs-lookup"><span data-stu-id="1116f-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="1116f-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="1116f-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="1116f-175">相对文件路径"DefaultPushSource"- [# 1746年](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="1116f-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="1116f-176">提高冲突解决程序失败消息- [# 1373年](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="1116f-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="1116f-177">v3 中的更新包失败，并不在指定的源的包[# 1013年](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="1116f-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="1116f-178">对于包源中使用相对路径会产生问题，若要使用- [#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="1116f-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="1116f-179">缺少 NUPKG 文件的间接依赖关系已存在具有较低的版本要求-如果从项目生成中的依赖项[#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="1116f-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="1116f-180">删除项目关闭相应 UI 窗口中，但重命名项目不会重命名 UI 窗口。</span><span class="sxs-lookup"><span data-stu-id="1116f-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="1116f-181">请注意 PMC 侦听项目重命名和项目删除事件- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="1116f-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="1116f-182">[Willow Web 工作负荷]创建 Razor v3 WSP 挂起- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="1116f-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="1116f-183">为特定包的安装/还原失败，出现"包包含多个 nuspec 文件。"</span><span class="sxs-lookup"><span data-stu-id="1116f-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="1116f-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="1116f-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="1116f-185">小写 Id &`packages.config`方案- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="1116f-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="1116f-186">[3.5-beta2]无法还原"传统"包的包还原[#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="1116f-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="1116f-187">nuget 包强制将.tt 文件添加到 content 文件夹，无论什么- [#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="1116f-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="1116f-188">更新包的 ASP.NET web 应用的生成与文件相关的警告： 源- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="1116f-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="1116f-189">nuget 包 csproj (使用`project.json`) 如果没有 packOptions 和在 JSON 文件的所有者将崩溃[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="1116f-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="1116f-190">适用于 nuget 包`project.json`将忽略摘要、 作者和所有者等-packOptions 标记[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="1116f-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="1116f-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="1116f-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="1116f-192">NuGet pack 忽略输出中的依赖关系`.nuspec`有关`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="1116f-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="1116f-193">使用回滚更新多个包使项目处于中断状态- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="1116f-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="1116f-194">任何下的内容文件不会添加为 netstandard 项目- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="1116f-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="1116f-195">无法打包库面向.Net 标准正确- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="1116f-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="1116f-196">文件-> 新建项目-> 类库 （可移植） 项目失败 VS2015 和 Dev15- [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="1116f-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="1116f-197">NuGet 错误-1.0.0-\* 不是有效的版本字符串- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="1116f-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="1116f-198">查找包失败到显示，但安装包的工作原理- [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="1116f-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="1116f-199">错误时在 dev15-上的"安装包 jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="1116f-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="1116f-200">nuget 包的 xproj 默认设置为无效的目标路径- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="1116f-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="1116f-201">当已安装的 VS 2015 更新 3 使用的 NuGet 版本 3.5.0 错误发生的对和[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="1116f-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="1116f-202">"阻止 packages.config" `project.json` (UWP，即生成集成) 项目- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="1116f-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="1116f-203">更新安装到 preview2-003121，这是官方 preview2 生成的生成脚本通过 dotnet cli。</span><span class="sxs-lookup"><span data-stu-id="1116f-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="1116f-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="1116f-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="1116f-205">包管理器 UI： 在更新包后不会显示新版本- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="1116f-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="1116f-206">-ApiKey delete 命令行上不读取/发送中 3.5.0-beta- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="1116f-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="1116f-207">不正确的字符串： 稳定的发行版的包不应具有在预发行版的依赖关系。</span><span class="sxs-lookup"><span data-stu-id="1116f-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="1116f-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="1116f-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="1116f-209">OptimizedZipPackage 缓存离开空文件夹- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="1116f-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="1116f-210">正在创建 PCL （net46 和 windows 10） 项目 get NullRef 异常。</span><span class="sxs-lookup"><span data-stu-id="1116f-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="1116f-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="1116f-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="1116f-212">Nuget 更新的 allowedVersions 约束的限制更高版本时应提供信息性消息[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="1116f-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="1116f-213">Nuget v3 还原问题- [# 2891年](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="1116f-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="1116f-214">凭据插件已退出，错误为-1 / 错误下载包时使用多个源的凭据提供程序[# 2885年](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="1116f-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="1116f-215">`project.json` nuget 还原导致重新编译时执行任何操作更改- [# 2817年](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="1116f-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="1116f-216">符号包不应在安装或更新-中使用[# 2807年](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="1116f-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="1116f-217">与不支持在 repositoryPath 中环境变量 （nuget.exe 执行）- [# 2763年](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="1116f-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="1116f-218">使用的可访问性的标签在包管理器用户界面中未标记的 UIElements [# 2745年](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="1116f-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="1116f-219">可移植框架使用连字符的由配置文件将被拒绝。</span><span class="sxs-lookup"><span data-stu-id="1116f-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="1116f-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="1116f-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="1116f-221">NuGet 包管理器应使它清楚该选项列表中包详细信息不适用于`project.json`  -  [# 2665年](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="1116f-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="1116f-222">nuget.exe 推送/删除不会使用 API 密钥- [# 2627年](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="1116f-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="1116f-223">从锁定文件中的删除锁定的属性[# 2379年](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="1116f-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="1116f-224">NuGet 3.3.0 更新失败，出现...更多约束中定义 packages.config 阻止此操作。</span><span class="sxs-lookup"><span data-stu-id="1116f-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="1116f-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="1116f-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="1116f-226">从本地源不存在，则会引发错误的邮件-安装包[# 1674年](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="1116f-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="1116f-227">"可用的升级"筛选器将显示与版本约束的冲突的升级[# 1094年](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="1116f-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="1116f-228">无法更新本机包- [# 1291年](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="1116f-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="1116f-229">功能</span><span class="sxs-lookup"><span data-stu-id="1116f-229">Features</span></span>

* <span data-ttu-id="1116f-230">引用添加 nuget-支持设置为 false 的 CopyLocal [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="1116f-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="1116f-231">MSBuild 15-nuget.exe 支持[# 1937年](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="1116f-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="1116f-232">对包支持。`csproj`</span><span class="sxs-lookup"><span data-stu-id="1116f-232">Pack support for .`csproj`</span></span><span data-ttu-id="1116f-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="1116f-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="1116f-234">禁用用户执行任何操作时没有用户正在执行的操作- [# 1440年](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="1116f-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="1116f-235">NuGet 应添加对的支持`runtimes/{rid}/nativeassets/{txm}/`  -  [# 2782年](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="1116f-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="1116f-236">添加 NuGet 中缺少的框架兼容性 （这已在 3.x） 的 2.x- [# 2720年](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="1116f-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="1116f-237">支持回退的包文件夹- [# 2899年](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="1116f-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="1116f-238">设计和实现包类型的概念，以支持工具的包- [# 2476年](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="1116f-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="1116f-239">添加一个 API 来获取全局包文件夹的路径[# 2403年](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="1116f-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="1116f-240">启用在包的 SemVer 2.0.0 [#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="1116f-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="1116f-241">DCR</span><span class="sxs-lookup"><span data-stu-id="1116f-241">DCRs</span></span>

* <span data-ttu-id="1116f-242">nuget.exe 推送-超时参数不起作用- [# 2785年](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="1116f-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="1116f-243">包描述文本应为可选择- [# 1769年](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="1116f-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="1116f-244">启用生成的 nuget.exe`.props`并`.targets`文件，以`.nuproj`项目[# 2711年](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="1116f-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="1116f-245">将可扩展性 API 进行比较与导入的框架添加[# 2633年](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="1116f-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="1116f-246">使用时隐藏依赖关系选项`project.json`  -  [# 2486年](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="1116f-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="1116f-247">打印出 nuget.exe 版本标头中详细输出- [# 1887年](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="1116f-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="1116f-248">NuGet 需要让用户知道，在基于 dotnet tfm 升级/安装 PCL 可能会导致问题- [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="1116f-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="1116f-249">错误安装/升级带 tfm 的项目，则发出警告 ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="1116f-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="1116f-250">修复性能问题与 ReShaper 和 NuGet 更新- [#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="1116f-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="1116f-251">添加了 netcoreapp11 和 netstandard17 支持- [# 2998年](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="1116f-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="1116f-252">利用 AssemblyMetadata 属性`.nuspec`令牌替换- [# 2851年](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="1116f-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
