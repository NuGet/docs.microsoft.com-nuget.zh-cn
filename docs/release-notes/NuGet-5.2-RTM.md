---
title: NuGet 5.2 RTM 发行说明
description: NuGet 5.2 的发行说明, 包括新功能、bug 修复和 Dcr。
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471180"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="e80ae-103">NuGet 5.2 发行说明</span><span class="sxs-lookup"><span data-stu-id="e80ae-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="e80ae-104">NuGet 分发车辆：</span><span class="sxs-lookup"><span data-stu-id="e80ae-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="e80ae-105">NuGet 版本</span><span class="sxs-lookup"><span data-stu-id="e80ae-105">NuGet version</span></span> | <span data-ttu-id="e80ae-106">适用于 Visual Studio 版本</span><span class="sxs-lookup"><span data-stu-id="e80ae-106">Available in Visual Studio version</span></span>| <span data-ttu-id="e80ae-107">适用于 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e80ae-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="e80ae-108">**5.2.0**</span><span class="sxs-lookup"><span data-stu-id="e80ae-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="e80ae-109">Visual Studio 2019 版本16。2</span><span class="sxs-lookup"><span data-stu-id="e80ae-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="e80ae-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="e80ae-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="e80ae-111"><sup>1</sup>随 Visual Studio 2019 with .NET Core 工作负载一起安装</span><span class="sxs-lookup"><span data-stu-id="e80ae-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="e80ae-112"><sup>2</sup>可用作 Visual Studio 2019 with .NET Core 工作负载的可选安装</span><span class="sxs-lookup"><span data-stu-id="e80ae-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="e80ae-113">摘要:5.2 中的新增功能</span><span class="sxs-lookup"><span data-stu-id="e80ae-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="e80ae-114">修复了由于 Linux & Mac 上的路径问题而导致不定期 NuGet 操作失败的严重 bug [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="e80ae-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="e80ae-115">提高了使用 Visual Studio 中的 NuGet 包管理器 UI 浏览包时的 UI 响应能力, 尤其是对于慢速源而言, [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e80ae-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e80ae-116">用于锁定文件的大量可靠性修补程序 ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) 和身份验证插件 ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845))</span><span class="sxs-lookup"><span data-stu-id="e80ae-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="e80ae-117">此版本中已修复的问题</span><span class="sxs-lookup"><span data-stu-id="e80ae-117">Issues fixed in this release</span></span>

<span data-ttu-id="e80ae-118">**Bug**</span><span class="sxs-lookup"><span data-stu-id="e80ae-118">**Bugs**</span></span>

* <span data-ttu-id="e80ae-119">性能程序包管理器控制台:UI 延迟更新 "默认项目" combobox 选定的值- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="e80ae-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="e80ae-120">性能PM UI 中的性能改进- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="e80ae-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="e80ae-121">性能在 PMC 中读取默认项目时的 UI 延迟- [#6824](https://github.com/NuGet/Home/issues/6824)</span><span class="sxs-lookup"><span data-stu-id="e80ae-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="e80ae-122">Perf: [vsfeedback] 针对本地包源的 "NuGet 更新" 选项卡冻结- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="e80ae-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="e80ae-123">插件如果插件无法启动或提前终止, NuGet 将等待完全握手超时[#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="e80ae-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="e80ae-124">插件: 提高诊断插件启动故障- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="e80ae-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="e80ae-125">插件内置插件的 nuget.exe 发现问题- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="e80ae-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="e80ae-126">插件: 缓存文件不是只读的[#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="e80ae-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="e80ae-127">插件"任务已取消。"</span><span class="sxs-lookup"><span data-stu-id="e80ae-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="e80ae-128">在还原过程中具有身份验证插件的错误- [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="e80ae-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="e80ae-129">无法在 linux 平台上间歇地发现插件缓存- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="e80ae-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="e80ae-130">LockFile: 使用 ATF 时, 由于目标 framework 相等性检查错误, 它具有 false NU1004 [#8187](https://github.com/NuGet/Home/issues/8187)</span><span class="sxs-lookup"><span data-stu-id="e80ae-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="e80ae-131">LockFile: 如果锁定文件为空或格式不正确, 则不遵循 "--锁定模式" 还原标志[#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="e80ae-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="e80ae-132">LockFile:不包含包中的自定义程序集名称的小写项目锁定文件- [#8114](https://github.com/NuGet/Home/issues/8114)</span><span class="sxs-lookup"><span data-stu-id="e80ae-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="e80ae-133">LockFile:在锁定文件中使项目引用小写[#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="e80ae-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="e80ae-134">还原: 安装篡改后的签名包将导致多次失败的安装尝试 (使用重复输出)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="e80ae-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="e80ae-135">VS: 解决方案用户选项在 NuGet 更新后未能反序列化- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="e80ae-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="e80ae-136">UnitTest 项目中的 dotnet 包返回错误- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="e80ae-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="e80ae-137">为 VS 安装程序创建 NuGet 包组-修复某些 VSIX 安装问题- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="e80ae-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="e80ae-138">GeneratePackageOnBuild 不应设置 NoBuild。</span><span class="sxs-lookup"><span data-stu-id="e80ae-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="e80ae-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="e80ae-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="e80ae-140">当 nuspec 文件包含显式程序集引用元素[#7638](https://github.com/NuGet/Home/issues/7638)时, 新选项 "-SymbolPackageFormat snupkg" 将生成错误。</span><span class="sxs-lookup"><span data-stu-id="e80ae-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="e80ae-141">NuGet (498, 5): 错误:找不到路径 "/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)</span><span class="sxs-lookup"><span data-stu-id="e80ae-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="e80ae-142">**DCR：**</span><span class="sxs-lookup"><span data-stu-id="e80ae-142">**DCR:**</span></span>

* <span data-ttu-id="e80ae-143">添加一个 msbuild 属性, 该属性指示支持 PackageDownload- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="e80ae-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="e80ae-144">FrameworkReference 通过 FrameworkReference 禁用依赖项流- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="e80ae-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="e80ae-145">用于在包外提供 runtime [#7351](https://github.com/NuGet/Home/issues/7351)的机制</span><span class="sxs-lookup"><span data-stu-id="e80ae-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="e80ae-146">**[此版本中已修复的所有问题的列表-5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="e80ae-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


